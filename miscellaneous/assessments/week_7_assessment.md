## The Twitter Challenge
This is the challenge that the coach should Slack the student. Time: 20 - 30 (tops) Advise the student to write his methods in an editor and paste them into irb or pry.  Also, the student needs to communicate what they are doing.

## Instructions

“Today we want to assess your ability to read documentation, research and make use of gems and use third party services. We want you to use of a gem called “twitter”  and use it to access the TwitterAPI in order to get the 5 last tweets from CraftAcademy (@CraftAcademySE) or Thomas (@ThomasOchman).

As you work on this exercise, please 'think aloud.' That means verbally describing your mental process as it develops, including the doubts and questions you have, the solution strategies you consider, and the reasons that justify your decisions.”

### Resources
* The twitter gem can be found on [https://github.com/sferik/twitter](https://github.com/sferik/twitter)
* The user name you want to search for is @ThomasOchman or @CraftAcademySE
* you need to register an application with Twitter here: [https://apps.twitter.com/](https://apps.twitter.com/)
* If you are facing a choice what method to use you should go with the “REST Client” (you’ll understand when you’ve read the gem documentation)

## Think Aloud Clarification
The 'Think-aloud' protocol involve the participant thinking aloud as he are performing a set of specified tasks or working on an excercise. The participant are asked to say whatever comes into his mind as he complete the task. This might include what he is looking at, thinking, doing, and feeling. This gives the coach valuable insight into the participant's cognitive processes (rather than only their final product), to make thought processes as explicit as possible during task performance.  Sessions should be recorded so that coaches can go back and refer to what participants did and how they reacted.




## Coach guide
**Not to be shared with students!**

There are many ways to retrieve the tweets for a user but here’s the simplest one using `.search`. 
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
client.search("from:ThomasOchman", result_type: "recent").take(5).each do |tweet|
  puts tweet.text
end

```

And the result should look something like this:

```shell
@perborgen @Scrimba @scrimba_com Next time I'll get it right... 😜
@Scrimba That Twitter handle is apparently not the one I should have used. #embarrassing
The ppl at @scrimba are doing some awesome stuff. Will definitely look into integrating Scrimba into our workflow. #learntocode #bootcamp
Sensommarläsning/lyssning 😜 Ping @birgittaohlsson #liberal #feminism #bookworm https://t.co/TufmXOSeI4
Med Elliot i #Frederikshavn #Denmark. 🇩🇰 Scouting the neighborhood of our new #getaway #remote… https://t.co/HxHEHstcgu

 => [#<Twitter::Tweet id=895675400864624640>, #<Twitter::Tweet id=895673096048439302>, #<Twitter::Tweet id=895625498264576000>, #<Twitter::Tweet id=894868644756307968>, #<Twitter::Tweet id=894302424361512961>]
```
