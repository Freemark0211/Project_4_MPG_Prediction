# Project_4_MPG_Prediction

Web Link to Tableau Presentation: https://public.tableau.com/app/profile/albert.dudek/viz/Project_4_MPG_Prediction/MPGbyYear?publish=yes

Predictive Model:

The code for constructing and testing our predcitive model can be found in the file "Reg_model_poly.ipynb". The model is a polynomial regression using the sklearn function PolynomialFeatures, which transforms the input variables into a polynomial function of highest order n (we used n=3) including interaction terms. 

The following steps were taken to format our data and constuct and test our model:

1. After inspecting the data, we made the following changes
    a. Remove vehicles made before the year 2000 as these datapoints include outliers in the mpg dimension due to unknown factors we could not identify in our dataset
    b. Transform the cylinder displacement using the natural logarithm to make the realtionship between it and the vehicle mpg approximately linear
2. One-hot encode the categorical variables vehicle class, drive, and transmission, and set the drop first option to "true" to eliminate colinear categorical input variables
3. Create the features (X) and response (y) data, then use train_test_split and StandardScaler to create scaled training and testing datasets (scaling omits the categorical features)
4. Create a regression pipeline with the PolynomialFeatures and LinearRegression functions, then train the model with the training data
5. Create predictions with the testing data and calculate model performance metrics
6. Manually calculate the residuals and look for predictions that underestimate the gas mileage by more than 10 mpg
7. Perform residual analysis to check for heteroscedasticity and normality, and plot the predictions versus the actual y_test values to visualize the model performance
8. Export/import the model and scaler using the Pickle library
9. Randomly sample the original dataframe and generate a new prediction with the imported .pkl files, then, check for agreement bewteen the estimate and the actual gas milage
10. Generate and test the code need to deploy the model with our FLask API 
    a. Generate "fake" input
    b. Encode categories from string inputs
    c. Format the vector
    d. Generate new prediction

Model Performance:

Model Deployment with Flask API:

The model was implemented using a Flask API, which routes to an HTML document that is used to collect input data from the user and display the corresponding mpg prediction. Item 10 above outlines the steps to implement the model, which only needed slight modifications in the Flask API. The follwing steps can be taken to run the model o a local device:

1. Clone the git repository
2. Open the "app.py" program in a command prompt after navigating to the main directory
    a. The main diectory should have the "app.py" file, a "static" directory which contains the .css file to set the style for the HTML file, and a "template" directory which contains the file "index.html" which is referenced in "app.py"
    b. The files "model.pkl" and "scaler.pkl" should also be int he main directory. These files apply the StandardScaler and regression pipelines to the input data, respectively.
3. Navigate to the http://127.0.0.1:5000/ url in a web browser to display the dashboard
4. Enter the vehicle specifications and click the "Predict car's MPG" button. The estimated gas mileage will appear below the button.