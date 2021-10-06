# Recommender Systems: Matrix Factorization
In this project, I explore matrix factorization using singular value decomposition and its utility in designing simple recommender systems

## Data: Twitch Stream Viewers
Below is a dataset of users consuming streaming content on Twitch. We retrieved all streamers, and all users connected in their respective chats, every 10 minutes during 43 days. `100k.csv` is a subset of 100k users. For the purposes of this demonstration, we shall only use a subset of this data. It contains the following attributes:
- User ID (anonymized)
- Stream ID
- Streamer username
- Time start
- Time stop

Start and stop times are provided as integers and represent periods of 10 minutes. Stream ID could be used to retrieve a single broadcast segment from a streamer (not used in our work).

<b>Data citation:<br></b>
Recommendation on Live-Streaming Platforms: Dynamic Availability and Repeat Consumption<br>
Jérémie Rappaz, Julian McAuley and Karl Aberer<br>
RecSys, 2021

The dataset can be found here: https://drive.google.com/drive/folders/1BD8m7a8m7onaifZay05yYjaLxyVV40si/

## Recommendation Task
We wish to recommend new Twitch streamers to users from their Twitch stream video consumption habits. 

## Matrix Factorization with SVD
Suppose we have a (pivot table) sparse matrix `M` of all users and all contents and values are time spent. We can factorize that matrix `M` $(n \times m)$ into three matrices `u` $(n \times n)$, `s` $(n \times m)$, and `v` $(m \times m)$ using SVD. Implicitly, `u` contains generic features that describe users and `v` contains features describing streamers, while `s` contains feature weights along the diagonal.

We can then multiply any user row in `u` with its associated weight in `s` and any streamer column in `v` transpose to determine a score (1x1) for that streamer for said user. We can then use this score to determine and sort suggestions.

## Discussion
Matrix factorization is an alternative to content-based filtering where we decide explicitly the features of the content. Here, the features describing the users and streamers are implicit in the time spent watching the streams. This makes it very attractive as as a recommender system as it eliminates the feature engineering process.

However, This huge sparse matrix requires a lot of computing power and time to factorize. Parallelising this process is a necessity with large datasets.

Therefore, although matrix factorisation is one of the easiest ways to generate recommendations using some simple linear algebra concepts, it poses difficulties dealing with large amounts of data. 
