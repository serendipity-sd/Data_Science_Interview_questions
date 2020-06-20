1. Why do you need to shuffle the dataframe??

Ans .1.1  If your data comes from different sources (different sensors, stores...) and you want to split it into train/validation sets, yes it is generally safer to shuffle it, as the partitions you will create will come from different sources.

Say some patients come from various hospitals and you want to predict if they have a specific disease from the following variables : age, sex, location. You gathered data from various hospitals and one of them, hospital i, is specialized in treating this disease. Then, if you just stacked the lines, you will see that lines between 100 and 150 (corresponding to the observations of hospital i) are more likely to be affected that other and treat it as a relevant predictor. You don't want this to happen. Even worse could be to train your model on this specific hospital data set and test it on another.

Ans 1.2 Shuffling data serves the purpose of reducing variance and making sure that models remain general and overfit less.

The obvious case where you'd shuffle your data is if your data is sorted by their class/target. Here, you will want to shuffle to make sure that your training/test/validation sets are representative of the overall distribution of the data.

For batch gradient descent, the same logic applies. The idea behind batch gradient descent is that by calculating the gradient on a single batch, you will usually get a fairly good estimate of the "true" gradient. That way, you save computation time by not having to calculate the "true" gradient over the entire dataset every time.

You want to shuffle your data after each epoch because you will always have the risk to create batches that are not representative of the overall dataset, and therefore, your estimate of the gradient will be off. Shuffling your data after each epoch ensures that you will not be "stuck" with too many bad batches.

In regular stochastic gradient descent, when each batch has size 1, you still want to shuffle your data after each epoch to keep your learning general. Indeed, if data point 17 is always used after data point 16, its own gradient will be biased with whatever updates data point 16 is making on the model. By shuffling your data, you ensure that each data point creates an "independent" change on the model, without being biased by the same points before them.


Q2.
