# mlFinalYelp
Machine Learning Final Project using the yelp dataset 

##Data Wrangling

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
- review_id (string, 22 character unique review id)
- user_id (string, 22 character unique user id, maps to the user in user.json)
- business_id (string, 22 character business id, maps to business in business.json)
- stars (integer, star rating)
- date (string, date formatted YYYY-MM-DD)
- text (string, the review itself)

### SyncUserAndReview.ipynb

*NO NEED TO TOUCH it*

Sync userDfFile.csv wiht all reviewDfFile parsed from ParseUserJson and ParseReviewJson by counting the number of available reviews for each user, and collecting all available review_id. Users with *<=80%* reviews available are dropped. The result is stoed in UserWithReviewDf.pkl

UserWithReviewDf.pkl contains the following data fileds:

- average_stars (float64, same as average_stars in the original user dataset)
- review_count (int64, same as review_count in the original user dataset)
- user_id (object, same as user_id in the original user dataset)
- yelping_since (object, same as yelping_since in the original user dataset)
- AvailPct (float64, review_count/AvailReviewCount)
- AvailReviewCount (int64, the length of the set stored in Reviews)
- Reviews (object, a set containing all available review_id that corresponding to the current user in the review datasets)

length: 388904

### FPIII_user.ipynb

Load UserWithReviewDf.pkl as userDf and drop users with *review_count<AvailReviewCount*

Subset users with review_count==1 as inactive users and export the data frame as inactiveUserDf.pkl

Subset users with review_count>=90 as active users and export the data frame as activeUserDf.pkl

Load all reviewDfFile and subset all reviews with review_id in inactiveUserDf.pkl and export the data frame as inactiveReviewDf.pkl
The length is 214054.

Load all reviewDfFile and subset all reviews with review_id in activeUserDf.pkl and export the data frame as activeReviewDf.pkl
The length is 210572.

Sample 80% of reviews in inactiveReviewDf and concat them with a random sample 0f 80% reviews in activeReviewDf to form the train set. Export the train set as train.pkl

The rest is exported as test.pkl

### ReviewClassification.ipynb

Apply tf-idf and run naive Bayes model and support vector machine model to predict whether a user is active or not with the text of review.

## Fetech dataset

To fetch large datasets (all .pkl) stored remotely with Git LFS, view instructions here:
https://git-lfs.github.com/

## Misc

Collaborators can view brainstorm docs at https://drive.google.com/drive/folders/10nvQvbiKhLKwC5BhrFXJ2bYQqTU79o2h?usp=sharing

To see full documentations of the original json files: https://www.yelp.com/dataset/documentation/json
