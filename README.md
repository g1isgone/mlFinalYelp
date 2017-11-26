# mlFinalYelp
Machine Learning Final Project using the yelp dataset  

*NO NEED TO TOUCH THE ParseUserJson.ipynb FILE!!!*

The file is just for parsing a 1.57GB user.json file and has stored the data frame as 'userDfFile.pkl'.

To load the clean data frame: 
`userDf = panda.read_pickle('userDfFile.pkl')`

It contains the following data fields:
- review_count      int64
- user_id          object
- yelping_since    object

*NO NEED TO TOUCH ParseReivewJson.ipynb either !!!*

The parsed csv files are stored locally and contains the following data fileds:
- review_id
- user_id
- business_id
- stars
- date
- text

Collaborators can view brainstorm docs at https://drive.google.com/drive/folders/10nvQvbiKhLKwC5BhrFXJ2bYQqTU79o2h?usp=sharing

To see full documentations of the original json files: https://www.yelp.com/dataset/documentation/json
