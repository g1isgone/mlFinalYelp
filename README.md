# mlFinalYelp
Machine Learning Final Project using the yelp dataset  

### ParseUserJson.ipynb

*NO NEED TO TOUCH it*

The file is just for parsing a 1.57GB user.json file and has stored the data frame as 'userDfFile.csv'.

To load the clean data frame: 
`userDf = panda.read_csv('userDfFile.csv',index_col=0)`

It contains the following data fields:
- average_stars    float64
- review_count       int64
- user_id           object
- yelping_since     object

### ParseReviewJson.ipynb

*NO NEED TO TOUCH it either*

The parsed csv files are stored locally and contains the following data fields:
- review_id
- user_id
- business_id
- stars
- date
- text

### FPII_user.ipynb

Create a way to measure user activity: 
`userDf['activity']=userDf.apply(lambda row: round(row.review_count*1000/((most_recent-row.yelping_since).days+1)),axis=1)`
Activity refers to the number of reviews the user writes per 1000 days.

Collaborators can view brainstorm docs at https://drive.google.com/drive/folders/10nvQvbiKhLKwC5BhrFXJ2bYQqTU79o2h?usp=sharing

To see full documentations of the original json files: https://www.yelp.com/dataset/documentation/json
