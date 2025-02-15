## Voice_Multi-Label_Classification_DeepLearning

Msc in Data Science 2020-21, NCSR 'Demokritos'. Deep Learning course. 2nd Semester.

This is a project with domain voice gender and language recognition. We have to extract some features from our mp3 data and then with some deep learning methods to predict the gender and/or language of this voice record.


### Gender Recognition to each Language
Each below procedure is implemented for the languages: Spanish, English, French, German

•	1.1. Dataset and counplots                                                                                                                                        We used the Mozilla audio dataset(https://commonvoice.mozilla.org/en/datasets), we also performed data exploration to see our data to each language and the distribution of the attributes of interest.

•	1.2. Convert mp3 to wav                                                                                                                                           To feed the CNN’s that we used, we converted the .mp3 audio files using the library.

•	1.3. Example of audio file                                                                                                                                          In this section is an example of an audio file and it’s spectogram

•	1.4. Fix length with adding silence                                                                                                                             Each audio file had a different size, but the audio files were very small that is why we used zero padding to adjust all files to a specific size.

•	1.5. Features extraction from audio data                                                                                                                            We implemented short term feature extraction using the: 
“https://github.com/tyiannak/pyAudioAnalysis/blob/master/pyAudioAnalysis/ShortTermFeatures.py”,
“https://github.com/tyiannak/pyAudioAnalysis/blob/master/pyAudioAnalysis/audioBasicIO.py”                                                                            and we extracted 68 feature to each 68 frames of every audio file.

•	1.6. Undersampling and scaling                                                                                                                                      With the data exploration we spotted that the data were imbalanced and to deal with it we implemented under-sampling to feed the CNN balanced data.

•	1.7. Split data and create model                                                                                                                                  We splited the data to train and test with percentages 70% and 30% respectively.

•	1.8. Results                                                                                                                                                      We used the min max scaler before feeding the data to the CNN.                                                                                                      Below are the details of our custom CNN model:                                                                                                                      1st layer was a Conv2d with filter 16, kernel size 3x3, input size(68,68,1) , the activation function was relu                                                       Next we added a Batch Normalization and MaxPooling2D with 2x2 kernel and Dropout(0.25)                                                                               2nd layer as a Conv2d with filter 32, kernel size 3x3, input size(68,68,1) , the activation function was relu.                                                        Next we added a Batch Normalization and MaxPooling2D with 2x2 kernel and Dropout(0.25)                                                                               3rd layer as a Conv2d with filter 64, kernel size 3x3, input size(68,68,1) , the activation function was relu.                                                    Next we added a Batch Normalization and MaxPooling2D with 2x2 kernel and Dropout(0.25)                                                                               4th layer as a Conv2d with filter 128, kernel size 3x3, input size(68,68,1) , the activation function was relu.                                                   Next we added a Batch Normalization and MaxPooling2D with 2x2 kernel and Dropout(0.25)                                                                               Then we flattened the model and used a Dense layer with filter 128 and relu activation function.                                                                   Then, we use  another Dense layer with filter 64 and relu activation function and another Dense layer with 32 and relu again, and in the last layer with sigmoid activation function and 1.                                                                                                                                       Finally, we compiled with the adam optimizer and we used as a loos function the binary_crossentropy.                                                                  Also we used Early Stopping to get the best model.                                                                                                                The results represented the loss, the accuracy, the F1 score and the ROC AUC.

•	1.9. Create spectrograms                                                                                                                                        For each dataset we tried to create spectograms.

•	1.10. Preparing spec data

•	1.11. Run model for spectograms and results



### Lauguage Recognition to all dataset( all 4 languages combined)
•	5.1. Summary and concatenation                                                                                                                                 
We concatenated all the 4 language data in a single dataframe and did the sum.

•	5.2. Create y values and split                                                                                                                                   
We performed under-sampling using the one sided selection and we reshape the dataframe to an array of (5953,68,68,1) but also we used the label encoder to turn each 
language to a numeric value. We splited the data to train and test with percentages 70% and 30% respectively.

•	5.3. Create model for multiclass in locale                                                                                                                        Below are the details of our custom CNN model:                                                                                                                    1st layer was a Conv2d with filter 16, kernel size 3x3, input size(68,68,1) , the activation function was relu                                                    Next we added a Batch Normalization and MaxPooling2D with 2x2 kernel                                                                                              2nd layer as a Conv2d with filter 32, kernel size 3x3, input size(68,68,1) , the activation function was relu.                                                    Next we added a Batch Normalization and MaxPooling2D with 2x2 kernel                                                                                                 3rd layer as a Conv2d with filter 64, kernel size 3x3, input size(68,68,1) , the activation function was relu.                                                       Next we added a Batch Normalization and MaxPooling2D with 2x2 kernel                                                                                                 Then we flattened the model and used the last Dense layer with filter 128 and relu activation function, another Dense layer with filter 32 and relu and another      Dense layer with filter 4 and softmax activation function.                                                                                                          Finally, we compiled with the adam optimizer and we used as a loos function the categorical_crossentropy.                                                           Also we used Early Stopping to get the best model.

•	5.4. Results                                                                                                                                                    The results represented the loss, the accuracy and a confusion matrix.

### Multi-label classification to language (all 4) and gender combined
•	6.1. Summary and concatenation                                                                                                                                    We made data preperation to feed the model in the form of data it must have.                                                                                          We used undersampling for the gender and then a MinMax scaler to the X values and we concat the language and the gender to y values with a transformation to_categorical values (like hot-encoding)

•	6.2. Summary and concatenation                                                                                                                                    We run the model that we use in chapter 1, 2, 3, 4 for binary classification, but now with 5 as number of output, 4 for the languages and 1 for the gender.     Then, we make some predictions with the model and we plot the results with classifixation report and a heatmap of confusion matrix.

