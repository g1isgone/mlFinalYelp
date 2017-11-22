# mlFinalYelp
Machine Learning Final Project using the yelp dataset  

NO NEED TO TOUCH THE ParseUserJson.ipynb FILE!!!
The file is just for parsing a 1.57GB user.json file and has stored the data frame as 'userDfFile.pkl'.
To load the clean dataframe: 
userDf = panda.read_pickle('userDfFile.pkl')
It contains the following data fields:
review_count      int64
user_id          object
yelping_since    object

To see full documentations of the original json files: https://www.yelp.com/dataset/documentation/json
