# Time-series forecasting with Transformer Neural Network

This paper project is a research about how to use a Transformers Neural Networ (TNN from now) to predict failures in the main bearing of wind turbines. The strategy followed uses SCADA data available from a twelve-turbine wind farm to perform the task involved. The TNN model was trained and tested on each turbine data individually, showing satisfactory results since fault detection in a damaged machine was predicted, with several months of anticipation and low prediction errors.

## Python libraries required

- Keras - Tensorflow: As the source of each model layer and training methods.
- Numpy - Pandas: For data preprocessing (cleaning, normalization and split)
- Seaborn - Matplotlib: For data visualizations and plotting the results.

## Methodology

### Data preprocessing

On the first stage, before model definition, several steps were taken in order to prepare the data and the time-series into a supervised learning problem. These include:

- Outliers deletion and interpolation.
- Min-max normalization
- Time-based train and test split
- Sequence preparation (t-144 records before forecasted time t+1)

### Model definition

As we were working with numbers only, there was no reason to use the positional encoding nor the decoding block of the TNN architecture, instead we just implemented  the encoder for this task. The hyperparameters tunning was made based on different tests of the model's performance until we found an appropiate configuration. Briefly, we encountered that:

- Values of learning rate higher than 0.001 produced a loss increment.
- Regularization using dropout and early stopping are necessary as the model tend to overfit.
- Batch size of 64 showed the correct balance between good predictions and performance.

## Results

The model was trained and tested on eleven healthy wind turbines and one presenting the main bearing fault on May 21, 2018. The experiment consisted on predicting the main bearing temperature and, using the absolute residual between observations and predictions, detect the peak of its value which is distinctive when the mechanical component is about to fail. As you can see in the image bellow, the alarm on the damaged turbine was triggered with months in advance, exceeding the threshold defined as the residual mean plus six times its standard deviation.

<div align="center">

  ![imagen_2024-02-23_113559873](https://github.com/juasesan/temperature_forecasting_torvis/assets/51239155/5b803461-1501-413e-a14d-f9bcb5bdf445)

</div>
