## TREND ANALYSIS

# Load requred Packages
library(tm)
library(ggplot2)
library(twitteR)
library(stringr)
library(wordcloud)
library(lubridate)
library(data.table)
library(ROAuth)

# Connect with twitter API
consumer_key <- ("gfngHNlOlH5Bio1rM3N36euSh")
consumer_secret <- ("BMt8rY8MAXdGUHT28vIf19Nj2zJUk8Hp7b74TWra6kZwcgPzF8")
access_token <- ("1255538298-Cumr8B0wJZ6ljWVYNL1Fcky2oQMuZCDmwhcI9QM")
access_secret <- ("2V0bT64ceSXEp7bsf9ETbAuMQoDL9HBrItJOR7oYMOdpg")
setup_twitter_oauth(consumer_key,consumer_secret,access_token,access_secret)
 

# Extract tweets based on the Hashtag #FreeErickKabendera
st="#FreeErickKabendera"
trendingtweets=searchTwitter(st,1000)

# Perform clean up
trendingtweetsdf= twListToDF(trendingtweets)
trendingtweetsdf$text=sapply(trendingtweetsdf$text,
                             function(x) iconv(x, to="UTF-8"))
trendingtweetsdf$created=ymd_hms(trendingtweetsdf$created)
View(trendingtweetsdf)

# Visualization
# Ploting a Histogram
# Time on X-axis
# Color coding blue for low green towards high

ggplot(data=trendingtweetsdf, aes (x=trendingtweetsdf$created))+ 
  geom_histogram(aes(fill=..count..))+
  theme(legend.position = "none")+
  xlab("Time")+ylab("Number of tweets")+
  scale_fill_gradient(low="midnightblue", high="Aquamarine4")


