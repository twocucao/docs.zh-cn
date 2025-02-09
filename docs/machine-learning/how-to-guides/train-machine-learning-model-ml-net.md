---
title: 训练和评估模型
description: 了解如何使用 ML.NET 生成机器学习模型、提取已学习的参数以及测量性能。 虽然此示例训练回归模型，但这些概念适用于大部分其他算法。
ms.date: 06/11/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc, how-to, title-hack-0612
ms.openlocfilehash: b7799d19f5ad51ce509cc6872d9053cad1158552
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2019
ms.locfileid: "67025591"
---
# <a name="train-and-evaluate-a-model"></a>训练和评估模型

了解如何使用 ML.NET 生成机器学习模型、提取已学习的参数以及测量性能。 虽然此示例训练回归模型，但这些概念适用于大部分其他算法。

## <a name="split-data-for-training-and-testing"></a>拆分数据用于训练和测试

机器学习模型旨在识别训练数据中的模式。 这些模式用于使用新数据进行预测。

给定以下数据模型：

```csharp
public class HousingData
{
    [LoadColumn(0)]
    public float Size { get; set; }

    [LoadColumn(1, 3)]
    [VectorType(3)]
    public float[] HistoricalPrices { get; set; }

    [LoadColumn(4)]
    [ColumnName("Label")]
    public float CurrentPrice { get; set; }
}
```

将数据加载到 [`IDataView`](xref:Microsoft.ML.IDataView) 中：

```csharp
HousingData[] housingData = new HousingData[]
{
    new HousingData
    {
        Size = 600f,
        HistoricalPrices = new float[] { 100000f ,125000f ,122000f },
        CurrentPrice = 170000f
    },
    new HousingData
    {
        Size = 1000f,
        HistoricalPrices = new float[] { 200000f, 250000f, 230000f },
        CurrentPrice = 225000f
    },
    new HousingData
    {
        Size = 1000f,
        HistoricalPrices = new float[] { 126000f, 130000f, 200000f },
        CurrentPrice = 195000f
    },
    new HousingData
    {
        Size = 850f,
        HistoricalPrices = new float[] { 150000f,175000f,210000f },
        CurrentPrice = 205000f
    },
    new HousingData
    {
        Size = 900f,
        HistoricalPrices = new float[] { 155000f, 190000f, 220000f },
        CurrentPrice = 210000f
    },
    new HousingData
    {
        Size = 550f,
        HistoricalPrices = new float[] { 99000f, 98000f, 130000f },
        CurrentPrice = 180000f
    }
};
```

使用 [`TrainTestSplit`](xref:Microsoft.ML.DataOperationsCatalog.TrainTestSplit*) 方法将数据拆分为训练集和测试集。 结果将是一个 [`TrainTestData`](xref:Microsoft.ML.DataOperationsCatalog.TrainTestData) 对象，其中包含两个 [`IDataView`](xref:Microsoft.ML.IDataView) 成员，一个用于训练集，另一个用于测试集。 数据拆分百分比由 `testFraction` 参数确定。 下面的代码片段让测试集占用 20% 的原始数据。

```csharp
DataOperationsCatalog.TrainTestData dataSplit = mlContext.Data.TrainTestSplit(data, testFraction: 0.2);
IDataView trainData = dataSplit.TrainSet;
IDataView testData = dataSplit.TestSet;
```

## <a name="prepare-the-data"></a>准备数据

在训练机器学习模型之前，需要对数据进行预处理。 有关数据准备的详细信息，请参阅[数据准备操作说明文章](prepare-data-ml-net.md)以及[`transforms page`](../resources/transforms.md)。

ML.NET 算法对输入列类型存在约束。 此外，如果未指定任何值，则默认值会用于输入和输出列名。

### <a name="working-with-expected-column-types"></a>使用预期的列类型

ML.NET 中的机器学习算法预期使用大小已知的浮点向量作为输入。 当所有数据都已经是数字格式并且打算一起处理（即图像像素）时，将 [`VectorType`](xref:Microsoft.ML.Data.VectorTypeAttribute) 属性应用于数据模型。 

如果数据不全为数字格式，并且想要单独对每个列应用不同的数据转换，请在处理所有列后使用 [`Concatenate`](xref:Microsoft.ML.TransformExtensionsCatalog.Concatenate*) 方法，以将所有单独的列合并为一个特征向量并将特征向量输出到新列。 

以下代码片段将 `Size` 和 `HistoricalPrices` 列合并为一个特征向量，该特征向量输出到名为 `Features` 的新列。 由于比例存在差异，将 [`NormalizeMinMax`](xref:Microsoft.ML.NormalizationCatalog.NormalizeMinMax*) 应用于 `Features` 列来规范化数据。

```csharp
// Define Data Prep Estimator
// 1. Concatenate Size and Historical into a single feature vector output to a new column called Features
// 2. Normalize Features vector
IEstimator<ITransformer> dataPrepEstimator =
    mlContext.Transforms.Concatenate("Features", "Size", "HistoricalPrices")
        .Append(mlContext.Transforms.NormalizeMinMax("Features"));

// Create data prep transformer
ITransformer dataPrepTransformer = dataPrepEstimator.Fit(trainData);

// Apply tranforms to training data
IDataView transformedTrainingData = dataPrepTransformer.Transform(trainData);
```

### <a name="working-with-default-column-names"></a>使用默认列名

未指定列名时，ML.NET 算法会使用默认列名。 所有训练程序都有一个名为 `featureColumnName` 的参数可用于算法的输入，并且在适用情况下，它们还有一个用于预期值的名为 `labelColumnName` 的参数。 默认情况下，这些值分别为 `Features` 和 `Label`。 

通过在预处理期间使用 [`Concatenate`](xref:Microsoft.ML.TransformExtensionsCatalog.Concatenate*) 方法创建名为 `Features` 的新列，无需在算法的参数中指定特征列名，因为它已存在于预处理的 `IDataView` 中。 标签列为 `CurrentPrice`，但由于数据模型中使用了 [`ColumnName`](xref:Microsoft.ML.Data.ColumnNameAttribute) 属性，ML.NET 将 `CurrentPrice` 列重命名为 `Label`，因而无需向机器学习算法估算器提供 `labelColumnName` 参数。 

如果不想使用默认列名，请在定义机器学习算法估算器时将特征和标签列的名称作为参数传入，如以下代码片段所示：

```csharp
var UserDefinedColumnSdcaEstimator = mlContext.Regression.Trainers.Sdca(labelColumnName: "MyLabelColumnName", featureColumnName: "MyFeatureColumnName");
```

## <a name="train-the-machine-learning-model"></a>训练机器学习模型

对数据进行预处理后，使用 [`Fit`](xref:Microsoft.ML.Trainers.TrainerEstimatorBase`2.Fit*) 方法通过 [`StochasticDualCoordinateAscent`](xref:Microsoft.ML.Trainers.SdcaRegressionTrainer) 回归算法训练机器学习模型。

```csharp
// Define StochasticDualCoodrinateAscent regression algorithm estimator
var sdcaEstimator = mlContext.Regression.Trainers.Sdca();

// Build machine learning model
var trainedModel = sdcaEstimator.Fit(transformedTrainingData);
```

## <a name="extract-model-parameters"></a>提取模型参数

训练模型后，提取已学习的 [`ModelParameters`](xref:Microsoft.ML.Trainers.ModelParametersBase%601) 用于检查或重新训练。 [`LinearRegressionModelParameters`](xref:Microsoft.ML.Trainers.LinearRegressionModelParameters) 提供经过训练的模型的偏差和已学习的系数或权重。 

```csharp
var trainedModelParameters = trainedModel.Model as LinearRegressionModelParameters;
```

> [!NOTE]
> 其他模型具有特定于其任务的参数。 例如，[K-Means 算法](xref:Microsoft.ML.Trainers.KMeansTrainer)基于形心将数据放入群集中，[`KMeansModelParameters`](xref:Microsoft.ML.Trainers.KMeansModelParameters) 包含存储这些已学习的形心的属性。 若要了解详细信息，请访问 [`Microsoft.ML.Trainers` API 文档](xref:Microsoft.ML.Trainers)并查找名称中包含 `ModelParameters` 的类。 

## <a name="evaluate-model-quality"></a>评估模型质量

若要帮助选择性能最佳的模型，必须评估其在测试数据中的性能。 使用 [`Evaluate`](xref:Microsoft.ML.RegressionCatalog.Evaluate*) 方法测量经过训练的模型的各种指标。

> [!NOTE]
> `Evaluate` 方法根据执行的机器学习任务生成不同的指标。 有关更多详细信息，请访问 [`Microsoft.ML.Data` API 文档](xref:Microsoft.ML.Data)并查找名称中包含 `Metrics` 的类。 

```csharp
// Measure trained model performance
// Apply data prep transformer to test data
IDataView transformedTestData = dataPrepTransformer.Transform(testData);

// Use trained model to make inferences on test data
IDataView testDataPredictions = trainedModel.Transform(transformedTestData);

// Extract model metrics and get RSquared
RegressionMetrics trainedModelMetrics = mlContext.Regression.Evaluate(testDataPredictions);
double rSquared = trainedModelMetrics.RSquared;
```

在上一代码示例中：  
1. 测试数据集使用之前定义的数据准备转换进行预处理。 
2. 经过训练的机器学习模型用于对测试数据进行预测。
3. 在 `Evaluate` 方法中，将测试数据集 `CurrentPrice` 列中的值与新输出预测的 `Score` 列进行比较，以计算回归模型的指标，其中之一是 R 平方，它存储在 `rSquared` 变量中。

> [!NOTE]
> 在这一小型示例中，由于数据大小存在限制，R 平方是一个不在 0-1 范围内的数字。 在实际方案中，应预期看到介于 0 和 1 之间的值。
