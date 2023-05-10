# Galaxy-Classification-ANN

The classification of galaxies as spirals or ellipticals is a crucial task in understanding their formation and evolution. With the arrival of large-scale astronomical surveys, such as the Sloan Digital Sky Survey (SDSS), astronomers now have access to images of a vast number of galaxies. However, the visual inspection of these images is an impossible task for humans due to the sheer number of galaxies to be analyzed. To solve this problem, the Galaxy Zoo project was created to engage thousands of citizen scientists to classify the galaxies based on their visual features. In this paper, we present a machine learning model for galaxy classification using numerical data from the Galaxy Zoo project. This model utilizes a convolutional neural network architecture to extract features from galaxy images and classify them into spirals or ellipticals. We demonstrate the effectiveness of our model by comparing its performance with that of human classifiers using a subset of the Galaxy Zoo dataset. Our results show that our model achieves high accuracy in classifying galaxies and has the potential to significantly enhance our understanding of the formation and evolution of galaxies.

Input : 

* OBJID - SDSS PhotoObjID for the galaxy
* RA - right ascension (HH:MM:SS.ss)
* DEC - declination (sDD:MM:SS.s)
* NVOTE - total number of votes for this object
* P_EL - fraction of votes for elliptical
* P_CW - fraction of votes for clockwise spiral
* P_ACW - fraction of votes for anticlockwise spiral
* P_EDGE - fraction of votes for edge-on spiral
* P_DK - fraction of votes for star/don't know
* P_MG - fraction of votes for merger
* P_CS - fraction of votes for combined spiral (CW+ACW+EDGE)
* P_EL_DEBIASED - debiased fraction of votes for elliptical
* P_CS_DEBIASED - debiased fraction of votes for combined spiral (CW+ACW+EDGE)


Output : 

The below three categories of galaxies were combined into a single column known as - shape_of_galaxy

* SPIRAL - flag: 1 if identified as spiral by the "clean" criterion using the debiased results, 0 otherwise
* ELLIPTICAL - flag: 1 if identified as elliptical by the "clean" criterion using the debiased results, 0 otherwise
* UNCERTAIN - flag: 1 if identified as uncertain by the "clean" criterion using the debiased results, 0 otherwise

## Model : 

Shape_of_galaxy is a multi-class target variable that we have included in our network. There are three neurons in the output, and each is classified as Spiral, Elliptical, or Uncertain. We have used 10 characteristics to create 10 neurons for the input layer. Each layer also has an activation function, the activation function relates to the forward propagation of calculation and storage of intermediate variables through the network. This function forwards the output while ensuring that values are kept within a range that is acceptable and useful for following layers.

Utilizing the Sequential() function from the tensorflow.keras.models module, the neural network architecture was created. Three dense layers made up the network; the final output layer used a softmax activation function, while the preceding two layers used ReLU activation functions. The number of features in the training data was used to establish the input shape for the first layer.

A hyperparameter tuning process was performed using RandomizedSearchCV to search for the best combination of hyperparameters for a deep neural network model. The model was built using the KerasRegressor wrapper from the TensorFlow library. The search space was defined using a dictionary of hyperparameters including the number of hidden units, activation function, and optimizer. The best model was selected based on the mean squared error metric evaluated using a 3-fold cross-validation. The model was trained on the training data using the best hyperparameters identified from the search. The accuracy and loss metrics were recorded during training to assess the model's performance. The best model was selected based on the hyperparameters that produced the best performance on the validation set.

The model was trained and tested on a dataset of 60000 records, with an accuracy score of 0.89 achieved on the test set.
