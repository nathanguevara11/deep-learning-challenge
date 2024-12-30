Module 21 Report
-----------------------
Purpose
The purpose of this assignment was to use data given to us to set up a program that would predict 
the likelyhood that a borrower would default on their loan. We were given a dataset contaning different parameters
such as application type, classification, amount borrowed, etc.


Preprocessing
-----------------------
- For some data points, such as for the application types and classification, we filtered elements in these rows (such as application types that had very low numbers of applicants, and classification types with very low numbers) and combined them into an "other" designation so that the neural network could process this imformtion more smoothly. 

- After filtering, we converted the dataframe into binary datapoints using pd.get_dummies. This allows the neural network to dstinguish true false pattens in the training phase and ultimately learn the patterns to look for in the testin phase. 

- We then split the dataframe gathered from the get_dummies function into X and y variables. For the y variable, we only added the "IS_SUCCESSFUL" column as this is our dependent variable. For the X variable, I decided to take out "STATUS", "IS_SUCCESSFUL", "SPECIAL_CONSIDERATIONS_N" becuase I felt status was not as important, is successful is the dependent variable, and special considerations N and special considerations y say that same thing but are opposites of each other, so I felt it better to just have one of those columns instead. 


Compiling, training, and evaluating the model
----------------------- 
- The final neural network consisted of 4 layers, 40 nodes in the input layer, 53 in hidden layer 1, 17 in hidden layer 2, and 1 unit in the output layer. I made the activation function a sigmoid function. I did these things because I had run a hyperparameter search before running the neural network and combined some of the suggestions given to me to setup my neural network configuration. 

-At first I was unable to achieve above a 75% accuracy rate, however, the changes made over time got me to over 75%. Initally, I only had two hidden nodes, but I later started playing around with the amount of layers (and various unit configurations for each layers), even getting up to ten hidden layers, but that did not help, so I used keras tuner and ran a hyperparameter search to see what would be the optimal configuration of my neural network. Within this hyperparameter search I initally was only using relu and tanh functions as possible activation functions, but a tutor I was working with suggested adding a sigmoid function to the activation function possbilities, and when running the hyperparameter tuner, the activation most effective for the model ended up being sigmoid. I attempted multiple manipulations of the dataframe such as dropping rows with "other" (my argument was that "other" is too ambiguous) and dropping up to ten columns from the dataframe but what ultimately worked was including the names as part of the information fed into the model (suggested by a tutor). What I found was this significantly increased the accuracy of the model, and in investigating why, I discovered that the names (especially the names that hint at the specific job sector, type of business, etc.) can clue in the model on pattenns that can help it make more accurate decisions. 


Summary
----------------------
The assignment aimed at seeing whether specific entities would default on thier loans was a tough and fufilling assignment. It involved re-categorizing data, dropping, adding, and restructuring data, and using multiple tools to create the most accurate model possible. I would suggest another model that would be useful to answer this question would be a random forest model because there were many data points in this dataset, and the sigmoid activation siggusts that the data relationships may not be entirely linear. Overall, this was a fun and engaging assignment! 