# DeepAR Hyperparameters<a name="deepar_hyperparameters"></a>


| Parameter Name | Description | 
| --- | --- | 
| time\_freq |  The granularity of the time series in the dataset\. Required\. Use `time_freq` to select appropriate date features and lags\. The model supports the following basic frequencies\. It also supports multiples of these basic frequencies\. For example, `5min` specifies a frequency of 5 minutes\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/sagemaker/latest/dg/deepar_hyperparameters.html) Valid values: An integer followed by *M*, *W*, *D*, *H*, or *min*\.For example, `5min` Default value: \-  | 
| prediction\_length |  The number of time\-steps that the model is trained to predict, also called the forecast horizon\. The trained model always generates forecasts with this length\. It can't generate longer forecasts\. The `prediction_length` is fixed when a model is trained and it cannot be changed later\. Required\. Valid values: positive integer Default value: \-  | 
| context\_length |  The number of time\-points that the model gets to see before making the prediction\. The value for this parameter should be about the same as the `prediction_length`\. The model also receives lagged inputs from the target, so `context_length` can be much smaller than typical seasonalities\. For example, a daily time series can have yearly seasonality\. The model automatically includes a lag of one year, so the context length can be shorter than a year\. The lag values that the model picks depend on the frequency of the time series\. For example, lag values for daily frequency are previous week, 2 weeks, 3 weeks, 4 weeks, and year\. Required\. Valid values: positive integer Default value: \-  | 
| likelihood |  The model generates a probabilistic forecast, and can provide quantiles of the distribution and return samples\. Depending on your data, select an appropriate likelihood \(noise model\) that is used for uncertainty estimates\. The following likelihoods can be selected: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/sagemaker/latest/dg/deepar_hyperparameters.html) Valid values: One of *gaussian*, *beta*, *negative\-binomial*, *student\-T*, or *deterministic\-L1*\. Default value: `student-T`  | 
| epochs |  The maximum number of passes over the training data\. The optimal value depends on your data size and learning rate\. See also `early_stopping_patience`\. Typical values range from 10 to 1000\. Required\. Valid values: positive integer Default value: \-  | 
| num\_dynamic\_feat |  The number of `dynamic_feat` provided in the data\. For example, if two dynamic features are provided, set this to 2\. Set this to `auto` to use the `dynamic_feat` field if it is present in the data to extract the number from the dataset\. Set it to an empty string to disable using the `dynamic_feat` field even if it is present in the data\. Valid values: positive integer, empty string, or `auto` Default value: `auto`  | 
| cardinality |  When using the categorical features \(`cat`\), cardinality is an array specifying the number of categories \(groups\) per categorical feature\. Set this to `auto` to use the `cat` feature if it is present in the data and extract the cardinalities automatically from the dataset\. Set it to an empty string to disable use of the `cat` field even if it is present in the data\. If you include categorical features, `cardinality` specifies the number of categories \(groups\)\.  For a fixed array index `i` with `cardinality[i] = N`, for all time series the value of `cat[i]` must range between `0` and `N-1`\. Valid values: array of positive integers, empty string, or `auto` Default value: `auto`  | 
| embedding\_dimension |  Size of embedding vector learned per categorical feature \(same value is used for all categorical features\)\. Optional\. The DeepAR model can learn group\-level time series patterns when a categorical grouping feature is provided\. To do this, the model learns an embedding vector of size `embedding_dimension` for each group, capturing the common properties of all time series in the group\. A larger `embedding_dimension` allows the model to capture more complex patterns\. However, because increasing the `embedding_dimension` increases the number of parameters in the model, more training data is required to accurately learn these parameters\. Typical values for this parameter are between 10\-100\.  Valid values: positive integer Default value: 10  | 
| num\_cells |  The number of cells to use in each hidden layer of the RNN\. Typical values range from 30 to 100\. Valid values: positive integer Default value: 40  | 
| num\_layers |  The number of hidden layers in the RNN\. Typical values range from 1 to 4\. Valid values: positive integer Default value: 2  | 
| mini\_batch\_size |  The size of mini\-batches used during training\. Typical values range from 32 to 512\. Valid values: positive integer Default value: 128  | 
| learning\_rate |  The learning rate used in training\. Typical values range from 1e\-4 to 1e\-1\. Valid values: float Default value: 1e\-3  | 
| dropout\_rate |  The dropout rate to use during training\. The model uses zoneout regularization: for each iteration a random subset of hidden neurons are not updated\. Typical values are less than 0\.2\. Valid values: float Default value: 0\.1  | 
| early\_stopping\_patience |  If this parameter is set, training stops when no progress is made within the specified number of `epochs`\. The model that has the lowest loss is returned as the final model\. Valid values: integer Default value: \-  | 
| test\_quantiles |  Quantiles for which to calculate quantile loss on the test channel\. Valid values: array of floats Default value: \[0\.1, 0\.2, 0\.3, 0\.4, 0\.5, 0\.6, 0\.7, 0\.8, 0\.9\]  | 
| num\_eval\_samples |  Number of samples that are used per time\-series when calculating test accuracy metrics\. This parameter does not have any influence on the training or the final model\. In particular, the model can be queried with a different number of samples\. This parameter only affects the reported accuracy scores on the test channel after training\. Smaller values result in faster evaluation, but then the evaluation scores are typically worse and more uncertain\. When evaluating with higher quantiles, for example 0\.95, it may be important to increase the number of evaluation samples\. Valid values: integer Default value: 100  | 