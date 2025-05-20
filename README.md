NAME: duen michael chombo
ROLL: id24m803
NO: assignment 3
GITHUB:https://github.com/duenchombo/DA6401_ASSIGNMENT_3
WANDBI:https://api.wandb.ai/links/duenchombo1-indian-institute-of-technology-madras/az36zu2s




Seq_To_Seq_Model-kagglenotebooks.ipynb :

(Contains code for question 1)

 
 • Section : Processing training and validation data – Contains code for data pre-processing data must be present in kaggle/input.
 • Section : Preparing Encoder and Decoder Inputs – Contains code for creating encoder and decoder inputs (one-hot encoding) from the pre-processed data.
 • Section : Defining Seq2Seq Model – Contains code for building a sequence to sequence model which contains the following layers: 

         (i) input layer for character embeddings 
         (ii) encoder cell (RNN/GRU/LSTM) which sequentially encodes the input character sequence (English)
         (iii) decoder cell which takes the last state of the encoder as input and produces one output character at a time (Devanagari).

       - The model is defined in function “training” which gives flexibility in defining the model by passing the following parameters:
         (i) Input embedding size
         (ii) Dropout
         (iii) Cell type – RNN, GRU or LSTM
         (iv) Hidden layer size
         (v) Number of encoder layers
         (vi) Number of decoder layers

       - The model is built such that there is one-to-one correspondence between layers of encoder and decoder and thus number of encoder and decoder layers is equal.

       - The function return model and encoder and decoder layers which are used for fitting and reconstruction of the model respectively.

 • Section : Inference Model – Contains code for inference. It contains two functions:
       - inferencing() – which contains code for reconstruction of encoder and decoder models from the model built by training() function. It takes the following arguments:
         (i) Model
         (ii) Number of encoder layers
         (iii) Number of decoder layers
         (iv) Encoder layers – returned by training function
         (v) Decoder layers – returned by training function
         (vi) Cell type – RNN/GRU/LSTM
         (vii) Hidden layer size

       - decode_sequence() – which contains code for generating hindi sequence corresponding to the input given. It takes the following arguments:
         (i) Input sequence – which is the encoder input data computed in Section : Preparing Encoder and Decoder Inputs
         (ii) Encoder model – returned by inferencing function
         (iii) Decoder model – returned by inferencing function

 • Section : Fitting the model – Contains code for compiling and fitting the model and calculating the validation accuracy using the inferencing and decode sequence fucntions.



Seq_To_Seq_Sweep_Model-kagglenotebooks.ipynb :

(Contains code for question 2)

 • All sections till “Fitting the model” are same as in the Seq_To_Seq_Model-kagglenotebooks.ipynb .
 • Section : Hyperparameter Tuning – 
           - sweep configuration is defined with the following hyperparameters:
             (i) Input embedding size
             (ii) Hidden layer size
             (iii) Cell type
             (iv) Number of layers of encoder and decoder 
             (v) Batch size
             (vi) Dropout
           - train function is defined for sweeping
           - sweep_id is set using wandb.sweep function
           - sweep is run for 28 times using random search as there are a lot of hyperparameter combinations.


Seq_To_Seq_Best_Model-kagglenotebooks.ipynb :

(Contains code for question 4)

 • All sections till “Fitting the model” are same as in the Seq_To_Seq_Model-kagglenotebooks.ipynb .
 • Section : Predictions on test set – Contains code for calculating test accuracy on the best model obtained by setting parameters from the sweep with best validation accuracy. It also stores all the predictions of test set in a csv file with format ['Input', 'Prediction', 'Ground Truth'] which is present in the folder – “Predictions_vanilla”.
 • Section : Displaying grid– Contains code for presenting the grid of some sample inputs of test set and corresponding predictions.


Seq_To_Seq_with_attention-kagglenotebooks.ipynb :

(Contains code for question 5)

 • All sections till “Fitting the model” are same as in the Seq_To_Seq_Model-kagglenotebooks.ipynb .
 • While creating the model an attention layer is added in the decoder part and the inferencing and decode sequence functions are changed accordingly. In addition to returning corresponding Devnagari sequence of the input, it also return the attention weights which are further used in plotting the heatmaps.
 • Section : Hyperparameter Tuning – 
           - sweep configuration is defined with the following hyperparameters:
             (i) Input embedding size
             (ii) Hidden layer size
             (iii) Cell type
             (iv) Number of layers of encoder and decoder 
             (v) Batch size
             (vi) Dropout
           - train function is defined for sweeping
           - sweep_id is set using wandb.sweep function
           - sweep is run for number times using random search as there are a lot of hyperparameter combinations.
 • Section : Predictions on test set – Contains code for calculating test accuracy on the best model obtained by setting parameters from the sweep with best validation accuracy. It also stores all the predictions of test set in a csv file with format ['Input', 'Prediction', 'Ground Truth'] which is present in the folder – “Predictions_attention”.
 • Section : Attention heatmaps – Contains code for presenting a 3x3 grid of attention heatmaps of some samples of test set.
