#workflow:
snscrape
snscrape is a scraper for social networking services (SNS). It scrapes things like user profiles, hashtags, or searches and returns the discovered items, e.g. the relevant posts.

The following services are currently supported:

Facebook: user profiles, groups, and communities (aka visitor posts)
Instagram: user profiles, hashtags, and locations
Mastodon: user profiles and toots (single or thread)
Reddit: users, subreddits, and searches (via Pushshift)
Telegram: channels
Twitter: users, user profiles, hashtags, searches, tweets (single or surrounding thread), list posts, and trends
VKontakte: user profiles
Weibo (Sina Weibo): user profiles
Requirements
snscrape requires Python 3.8 or higher. The Python package dependencies are installed automatically when you install snscrape.

Note that one of the dependencies, lxml, also requires libxml2 and libxslt to be installed.

Installation
pip3 install snscrape
If you want to use the development version:

pip3 install git+https://github.com/JustAnotherArchivist/snscrape.git
Usage
CLI
The generic syntax of snscrape's CLI is:

snscrape [GLOBAL-OPTIONS] SCRAPER-NAME [SCRAPER-OPTIONS] [SCRAPER-ARGUMENTS...]
snscrape --help and snscrape SCRAPER-NAME --help provide details on the options and arguments. snscrape --help also lists all available scrapers.

The default output of the CLI is the URL of each result.

Some noteworthy global options are:

--jsonl to get output as JSONL. This includes all information extracted by snscrape (e.g. message content, datetime, images; details vary by scraper).
--max-results NUMBER to only return the first NUMBER results.
--with-entity to get an item on the entity being scraped, e.g. the user or channel. This is not supported on all scrapers. (You can use this together with --max-results 0 to only fetch the entity info.)
Examples
Collect all tweets by Jason Scott (@textfiles):

snscrape twitter-user textfiles
It's usually useful to redirect the output to a file for further processing, e.g. in bash using the filename twitter-@textfiles:

snscrape twitter-user textfiles >twitter-@textfiles
To get the latest 100 tweets with the hashtag #archiveteam:

snscrape --max-results 100 twitter-hashtag archiveteam
Library
It is also possible to use snscrape as a library in Python, but this is currently undocumented.

Issue reporting
If you discover an issue with snscrape, please report it at https://github.com/JustAnotherArchivist/snscrape/issues. If possible please run snscrape with -vv and --dump-locals and include the log output as well as the dump files referenced in the log in the issue. Note that the files may contain sensitive information in some cases and could potentially be used to identify you (e.g. if the service includes your IP address in its response). If you prefer to arrange a file transfer privately, just mention that in the issue.

License
This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program. If not, see https://www.gnu.org/licenses/.





#Execution:-
#Use this code to scrape the datas from the twitter account , that will be effectively been read as data frames using the pandas
#package,pandas package is used for dataframe, tqdm is for the progress bar,snscrape for scraping of the data , for converting the
#json file and reading a json file,pymongo is for the mongodb insertion,also to establish the connection between the python juypter to 
#the mongodb,and reading the csv file,
#create a empty list,scraper variable is assumed to the search scraper module with #puthon keyword, then loop it with th headers of the scraper variable
#create the list with the scraper object variable,then append the data and store it in tweets and extract 1000 records and print,convert the tweets in to dataframe 
#using pandas and tweets list with tweets_df variable,convert in to the csv file and establish the connection with the mongodb,mongodb reads the csv file in to the 

#dayabase installation and collections books1.



import pandas as pd
from tqdm.notebook import tqdm
import snscrape.modules.twitter as snstwitter
import json
from pymongo import MongoClient
import pymongo
import csv
import streamlit as st
import numpy as np




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
df1=pd.DataFrame(np.random.randn(20,3),columns=["id","username","retweet"])

#st.line_chart(df1,x="date",y=["id","content","username","retweet"])

st.line_chart(df1)
st.write("""# My First App Hello * World!*""")
