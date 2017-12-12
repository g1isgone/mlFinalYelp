# mlFinalYelp
Machine Learning Final Project using the yelp dataset 

## Datasets

The following datasets are stored at: https://drive.google.com/open?id=165BtowOkCVpmIDeQlqj-JRLZBs2up2sS

- UserWithReviewDf.pkl 65MB
- train.pkl 247MB
- test.pkl  63MB
- inactiveUserDf.pkl  20MB
- inactiveReviewDf.pkl  120MB
- activeUserDf.pkl  5MB
- activeReviewDf.pkl  186MB

## Data Wrangling

### ParseUserJson.ipynb

Parsed the 1.57GB user.json and did data cleaning. The result data frame is stored locally as *userDfFile.csv* which contains the follwing fields:

- average_stars    float64
- review_count       int64
- user_id           object
- yelping_since     object

### ParseReviewJson.ipynb

Parse the 3.82GB review.json and does data cleaning. The result data frames are stored locally as *reviewDfFile1.csv, reviewDfFile2,csv, reviewDfFile3.csv, reviewDfFile4.csv*, which all contains the following data fields:

- review_id (string, 22 character unique review id)
- user_id (string, 22 character unique user id, maps to the user in user.json)
- business_id (string, 22 character business id, maps to business in business.json)
- stars (integer, star rating)
- date (string, date formatted YYYY-MM-DD)
- text (string, the review itself)

### SyncUserAndReview.ipynb

Sync userDfFile.csv wiht all reviewDfFile parsed from ParseUserJson and ParseReviewJson by counting the number of available reviews for each user, and collecting all available review_id. Users with *<=80%* reviews available are dropped. The result is stoed in *UserWithReviewDf.pkl*, which contains the following data fields:

- average_stars (float64, same as average_stars in the original user dataset)
- review_count (int64, same as review_count in the original user dataset)
- user_id (object, same as user_id in the original user dataset)
- yelping_since (object, same as yelping_since in the original user dataset)
- AvailPct (float64, review_count/AvailReviewCount)
- AvailReviewCount (int64, the length of the set stored in Reviews)
- Reviews (object, a set containing all available review_id that corresponding to the current user in the review datasets)

Then load UserWithReviewDf.pkl and drop users with *review_count<AvailReviewCount*

Subset users with review_count==1 as inactive users and export the data frame as *inactiveUserDf.pkl*

Subset users with review_count>=90 as active users and export the data frame as *activeUserDf.pkl*

Load *reviewDfFile1.csv, reviewDfFile2,csv, reviewDfFile3.csv, reviewDfFile4.csv* and subset all reviews with review_id in *inactiveUserDf.pkl* and export the data frame as *inactiveReviewDf.pkl*
The length is 214054.

Subset all reviews with review_id in activeUserDf.pkl and export the data frame as *activeReviewDf.pkl*
The length is 210572.

Sample 80% of reviews in inactiveReviewDf and concat them with a random sample 0f 80% reviews in activeReviewDf to form the train set. Export the train set as *train.pkl*

The rest is exported as *test.pkl*

length: 388904

## Modeling & Analysis

### ReviewClassification.ipynb

Apply tf-idf and run naive Bayes classifier and Support Vector Machine model to predict whether a user is active or not with review contents. SVM achieves an accuracy of 80%.

Visualize tf-idf of a subset of active users and a subset of inactive users.

### UserExploration.ipynb

Contains scatterplot of review_count and average_stars, and some random experimentations with user and review data.


## Misc

Collaborators can view brainstorm docs at https://drive.google.com/drive/folders/10nvQvbiKhLKwC5BhrFXJ2bYQqTU79o2h?usp=sharing

To see full documentations of the original json files: https://www.yelp.com/dataset/documentation/json
