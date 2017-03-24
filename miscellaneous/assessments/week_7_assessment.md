## The Twitter Challenge
This is the challenge that the coach should Slack the student. Time: 20 - 30 (tops) Advise the student to write his methods in an editor and paste them into irb or pry.  Also, the student needs to communicate what they are doing.


Today we want to assess your ability to read documentation, research and make use of gems and use third party services. We want you to use of a gem called “twitter”  and use it to access the TwitterAPI in order to get the 5 last tweets from Amber.

### Resources

* The twitter gem can be found on [https://github.com/sferik/twitter](https://github.com/sferik/twitter)
* The user name you want to search for is @heyamberwilkie
* you need to register an application with Twitter here: [https://apps.twitter.com/](https://apps.twitter.com/)
* If you are facing a choice what method to use you should go with the “REST Client” (you’ll understand when you’ve read the gem documentation)


## Coach guide
**Not to be shared with students!**

There are many ways to retrieve the tweets for a user but here’s the simplest one using `.search`. 
In order for it to work you need to have configured a `client` That is the main part of the challenge. ```

In order for it to work you need to have configured a `client` That is the main part of the challenge. 

```shell
$ gem install twitter

```
Open up `irb` and make sure to `require 'twitter'`

Set up a client
```ruby
client = Twitter::REST::Client.new do |config|
  config.consumer_key        = "YOUR_CONSUMER_KEY"
  config.consumer_secret     = "YOUR_CONSUMER_SECRET"
  config.access_token        = "YOUR_ACCESS_TOKEN"
  config.access_token_secret = "YOUR_ACCESS_SECRET"
end
```

Search for tweets
```ruby
client.search("from:heyamberwilkie", result_type: "recent").take(5).each do |tweet|
  puts tweet.text
end

```

And the result should look something like this:

```shell
#100DaysOfCode 46 - more work on Snack forums. https://t.co/tHu8dWVwza Learned some SASS today! @diraulo was happy (and helpful)
.@thredded guys I am so impressed with this engine. Everything works *exactly* the way I expect it to. Love being able to guess. So good!
Data visualization GIFs: Political polarization in the American public, 1994 - 2015 https://t.co/1cPyod4R20 via @flowingdata
In my previous life, I was a professional photographer. Here's round two of my photos from Morocco: https://t.co/YprxuTqc0Z
#100DaysOfCode 45: Forums for user interaction. Used @thredded engine - *amazing* out-of-box functionality. https://t.co/tHu8dWVwza #webdev
 => [#<Twitter::Tweet id=838824221530783744>, #<Twitter::Tweet id=838790390778068992>, #<Twitter::Tweet id=838777070360662016>, #<Twitter::Tweet id=838419042935373825>, #<Twitter::Tweet id=838403883051405314>] 
```
