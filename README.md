# ASHRAE---Great-Energy-Predictor-III_Project
In this Project , I developed an lstm model to predict metered building energy usage.

This project was built using these different libraries:
pandas :for data manipulation and analysis
matplotlib : for plotting
numpy :for tools to work with arrays
math :for the square mean and std function
seaborn :for data visualization
sklearn.impute import SimpleImputer : filling missing values with another value

For modeling we used keras and these different 
keras.models import Sequential
keras.layers import Dense, Activation, Dropout 
keras.layers import LSTM

    The data preparation part:
- weather_data : I started by dealing with missing values , using SimpleImputer and I chose to fill them with the most frequent value 
for each column.Since I used an RNN model (LSTM) I thought that non scaled values could affect the result so i scaled all the features in 
the weather_data using mean and std functions.
-Building_data : I started by dealing with missing values , using SimpleImputer and I chose to fill them with the most frequent value 
for each column.I did the scaling for the non categorical features using mean and std functions.Since we have one categorical feature
(Primary_use) i applied the get_dummies function to add the different categories as columns to the dataframe.
-Train_data: Since the meter_reading attribut is not symetric , i applied log normalisation and also did scaling.
I also used the get_dummies function for the meter attribut since it's a categorical attribut.I also used the timestamp attribut to add
a day , month , year and hour attribut.

   The Merging the data:
- I applied a merge on the building_data and the train_data using the building_id.
- I applied a merge on the weather_data and the train_data using the timestamp and the site_id .

   The Modeling part :
 - To prepare the data we feeding to the network , i used a data_generator instance which is a class that help us in shaping the data 
 for the network.By fixing the features , the batch_size, the ids of the samples and the data it returns the data in the right shape to feed
 in the network .
 - I built a LSTM model with one hidden layer with 100 units and relu as activation function.
 
  The test part :
- I saved the trained model as a json file to use later for prediction.
- For the weather_test data I did the same preprocessing as the weather train data .
- For the prediction , each step I used a part from the test data , I did the merging and the preprocessing ( the same steps we did 
for the train data ) and then I used the model with the function predict.After that I applied the expm1 which is the inverse of the log
function ( to undo the log normalisation we did in the preprocessing) and add it to the result.


 
 

