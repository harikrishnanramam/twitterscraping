import pandas as pd
from tqdm.notebook import tqdm
import snscrape.modules.twitter as snstwitter
import json
from pymongo import MongoClient
import pymongo
import csv



tweets=[]
scraper = snstwitter.TwitterSearchScraper("#python")
for i,tweet in enumerate(scraper.get_items()):
  data = [tweet.date,tweet.id,tweet.renderedContent,tweet.user.username,
          tweet.retweetCount,tweet.replyCount,tweet.lang,tweet.likeCount,tweet.source]

  tweets.append(data)

  if i>1000:
    break
     

      
tweets

tweets_df=pd.DataFrame(tweets,columns=['date','id','content','username','retweet'
,'replycount','language','likecount','source'])

tweets_df
tweets_df.to_csv(r'C:\Users\USER\Desktop\StudyMaterial\python36.csv',index=False,header=True)
tweets_df.to_json(r'C:\Users\USER\Documents\python37.json')


pdf= pd.read_csv(r'C:\Users\USER\Desktop\StudyMaterial\python36.csv')


print(pdf)

dict_from_csv = pd.read_csv(r'C:\Users\USER\Desktop\StudyMaterial\python36.csv', header=None, index_col=0, squeeze=True).to_dict()
print(dict_from_csv)


myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["Installation"]
mycol = mydb["books1"]
mylist = [
  { "name": "Amy", "content": "Apple st 652"},
  { "name": "Hannah", "content": "Mountain 21"},
  { "name": "Michael", "content": "Valley 345"},
  { "name": "Sandy", "content": "Ocean blvd 2"},
  { "name": "Betty", "content": "Green Grass 1"},
  { "name": "Richard", "content": "Sky st 331"},
  { "name": "Susan", "content": "One way 98"},
  { "name": "Vicky", "content": "Yellow Garden 2"},
  { "name": "Ben", "content": "Park Lane 38"},
  { "name": "William", "content": "Central st 954"},
  { "name": "Chuck", "content": "Main Road 989"},
  { "name": "Viola", "content": "Sideway 1633"}
]




mycol.insert_many(mylist)
