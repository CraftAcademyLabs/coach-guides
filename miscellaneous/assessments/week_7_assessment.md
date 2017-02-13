## The Twitter Challenge
This is the challenge that the coach should Slack the student. 
Time: 20 - 30 (tops) 
Advise the student to write his methods in an editor and paste them into irb or pry.  
Also, the student needs to communicate what they are doing.

### Introduction
Today we want to assess your ability to read documentation, research and make use of gems and use third party services. We want you to use of a gem called “twitter”  and use it to access the TwitterAPI in order to get the 5 last tweets from The President of the United States.

Resources:

* The twitter gem can be found on https://github.com/sferik/twitter
* The user name you want to search for is `@POTUS`
* You need to register an application with Twitter here: https://apps.twitter.com/
* If you are facing a choice what method to use you should go with the “REST Client” (you’ll understand when you’ve read the gem documentation)

There are many ways to retrieve the tweets for a user but here’s the simplest one using `.search`. In order for it to work you need to have configured a `client` That is the main part of the challenge. 

Setting up the `client` requires the student to have hers/his Twitter App credentials and use the REST method:
```
client = Twitter::REST::Client.new do |config|
  config.consumer_key        = "YOUR_CONSUMER_KEY"
  config.consumer_secret     = "YOUR_CONSUMER_SECRET"
  config.access_token        = "YOUR_ACCESS_TOKEN"
  config.access_token_secret = "YOUR_ACCESS_SECRET"
end
```

Getting the tweets is as simple as: 
```
client.search("from:potus", result_type: "recent").take(5).each do |tweet|
  puts tweet.text
end
``` 

### Twitter credentials
If the user **can not** create an app on Twitter we can provide him with credentials to our own Twitter application. We want however the student to demonstrate the ability to research and respond to documentation. Meaning we want her/him to try go through the necessary steps. 


