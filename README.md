# Franklin University - DATA-611 Applied Machine Learning Final Project

Notebooks and model byproducts created for the Franklin University DATA-611 final project for Fall of 2023. This repository represents my contributions to the group work.

## Notebook Architecture

This ML Project uses several different notebooks in sequence to fully process its data. This was partially done for efficiency so the entire notebook wouldn't need to be re-run, but ultimately wound up being helpful to isolate Python dependencies.

``` mermaid
flowchart TD
    csvCredit[/credit_default.csv/] --> nbClean
    nbClean[DataCleaningAndExploration.ipynb] --> csvCleaned
    csvCleaned[/cleaned.csv/] --> nbSplit
    nbSplit[TrainTestSplit.ipynb] -->|80%| csvTrain
    nbSplit[TrainTestSplit.ipynb] -->|20%| csvTest
    csvTrain[/train.csv/] --> nbAutoML
    csvTest[/test.csv/] --> nbMetrics
    nbAutoML[AutoML.ipynb] --> model
    model([model.pkl]) --> nbMetrics
    csvCleaned -->|Bias Detection Columns| nbMetrics
    nbMetrics[ModelMetrics.ipynb]
```

These notebooks were originally created in Azure Machine Learning Studio on a `Linux STANDARD_E4DS_V4` compute instance. This was important because auto-sklearn requires a Linux instance.

Ultimately, the notebooks were executed in two separate kernels to separate different Python dependencies, with the `Python 3.8 - AzureML` kernel being used for cleaning and splitting (including SMOTE) and a `Python 3 (ipykernel)` kernel used for model training and evaluation.

``` mermaid
flowchart TD
    subgraph Python 3.8 AzureML Kernel
      nbClean[DataCleaningAndExploration.ipynb]
      nbSplit[TrainTestSplit.ipynb]
    end
    subgraph Python 3 ipython Kernel
      nbAutoML[AutoML.ipynb]
      nbMetrics[ModelMetrics.ipynb]
    end

    nbClean --> nbSplit
    nbSplit --> nbAutoML
    nbAutoML --> nbMetrics
```
