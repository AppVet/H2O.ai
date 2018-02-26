For housing price prediction demo:

* Start H2O.ai by opening terminal and changing directory to /home/rockitlabai/h2o-3.18.0.2. Then run: 

  #java -jar h2o.jar

* Open browser to http://localhost:54321/flow/index.html to view H2O Flow (H2O IU)

* Select Data -> Upload Files. Under "Files", add path: (DO NOT USE IMPORT)

  /home/rockitlabai/git/H2O.ai/housing_price_prediction/all_house_data_utf-8.csv (H2O does not support UTF-16!)

  then select magnifying glass. Then select the all_house_data_utf-8.csv file.

* Edit first column name to remove garbled characters leaving 'sqft'.

* Check to make sure column names and data types are correct. Then select "Parse these files..." 
  followed by "Parse".

* Under 'Job -> key', select the "*.hex" link.

* Select "Split" to split the dataset into test and training data sets.

* Use default .75 and .25 ratios for training and test sets. Then select "Create".

* Under 'Split Frames', select the "frame_0.750" link and select "Build Model...".

* Under 'Build a Model', set the following parameters:
  - Select an Algorithm: "Gradient Boosting Machine"
  - training frame: frame_0.075
  - validation frame: frame_0.025
  - response column: sale_price
  - min rows: 10 (due to lack of data)

* Next, go to the bottom and select "Build Model" then select "View". Note that under 'Job -> key', an 
  ID is generated for your model. For a Gradient Boost model, the model ID will start with "gbm-*'.

* Next, to run predictions, go to the top of the page and select Score -> Predict...  Then, select 
  the model "gbm-*" and Frame as "frame_0.250". Here, we use the validation set for prediction but 
  should use another unused dataset if possible. Next, select "Predict".

* Under 'Prediction', select "Combine predictions with Frame" then select "View" to show 
  sample predictions side-by-side. Note that only some of the predictions will be shown. To view
  all predictions for the prediction dataset (in this case, the test set), select 'Download' from
  the 'combined prediction..." menu. Note that the file will be generated as an Excel CSV file.

* Save your H2O Flow by going to the top menu and selecting "Flow -> Save Flow" 
  and then select "Flow -> Download Flow" to download the flow file.

* To generate a Java POJO, scroll to the 'Model' section of the Flow and select 'Download POJO'.