# twitch_project

This is a currently a public repository. I might change it to private this week. I could add your accounts as collaborators, or think of other ways to share these (maybe a link to the notebook on my drive/ pdf). 
- Link to the initial [proposal](https://docs.google.com/document/d/1NeULev_u3fpf7Zrn_sOdR7k33qzWW9lFx29LEjeLb14/edit?usp=sharing)
- Literature [notion page](https://www.notion.so/pearlyu/Working-on-a-research-question-f4e889d8cad645428feae3a91dd3e873)

By Oct 8th: 
- Sample dataset construction and initial insights: Uploaded 10092022 notebook
- Archived dataset: [TwitchTracker](https://sullygnome.com/channels/30/followergrowth) This is a really impressive data collection. I'm using this to dig in, looking for patterns. As this site pulls the twitch API every 15 minutes since 2015, I'm thinking emailing the developer to collaborate, as he indicated no scraping please. But this site doesn't scrape viewer engagement (chats). 

By Oct 10th:
- Uploaded 10102020 notebook:
  - Workflow:
    - Go to [TwitchTracker](https://sullygnome.com/channels/30/followergrowth) to select a sample, download the csv.  **Need to talk about sample selection. Currently it's stratified picking by fastest growth in last 30 days.**
    - Use the url there to retrieve broadcast id and info by calling the get_user endpoint.
    - Use the retrieved video id to get video info by calling the get_videos endpoint.
    - Use the retreived video url to get chat files using the [chatdownloader](https://github.com/xenova/chat-downloader/tree/master/docs) github project.  **remember to download it locally too.**
    - Examine the returned json chat files, **see what variables to construct.** 

Oct 12th meeting: 
- Made the **research questions** more clear: Take perspective of the platform, that cares about incentivizing the streamers to stay and grow on the platform. They’d want more ‘full time’ streamers as the content is delivered live. 
  - Hence we model the streamers’ decisions.
- Dependent variables:
  - Staying, or leaving the platform. 
  - Streaming time – part time/ full time.
  - Content choices: number of game categories. 
- Independent variables:
  - Aside from e.g. views, follows, number of chat messages, first we want to dig in the chat files:
  - Meta data includes the status of user who comments (if subscriber, VIP, prime subscriber, if streamer..)
  - From the text,  LDA, sentiments, emotions are easy to extract. But it should start with what could be the interesting story. We talked about a few ideas. 
 
By Oct 19th:  
- About dependent variable: Plotted average weekly streaming time of 90 randomly selected streamers. Looks binormal.Using 30-hour to classify part-time and full-time sounds like the initial plan. 
- About features from chat files: Fit topic models on 90 videos, checked on correlation including lag 1 to guide theory building. 

Oct 20th meeting:  
Today we thought about **what's the interesting question** again: The idea is that streamers can experience burnout from managing interactions, unique to content creators in live streaming. Too many interactions/engagements with viewers might be too heavy of a workload. This might in a long term impact the streamers' streaming decisions. 
We think this question has a larger scope than the previous direction (which is to see if something in the chat impacts the streamers' decisions). 


<ins>Action items: <ins>  
- Download video files and chats. 
- Basic chat features: number of messages, number of messages per minute, average message length, proportion of meaninful messages, message sentiments. (Runshan: I remember there are some techniques that allow you to separate texts are more emotional from those more factual (like objective comments, feedback, constructive suggestions), it would be useful to check this as well.)
- Measure engagement level: The number of times a streamer responds to a chat? The number of times that a streamer asks questions to the viewers? Check on the literature to get more ideas. 
- Explore the relationship between chat features and engagement level.
 
***

Action items from before the meeting:  
- Sample selection? How to select the sample? (Currently it's stratified picking by fastest growth in last 30 days. Restricted to English steams. Can we use shorter streams only? Should it be stratified by dependent variables?)
- Dependent variables: 
  - Game category: I think we can download from https://sullygnome.com/channel/kaicenat/365/streams, and integrate it in once we know what sample. Cuz this would be manually done. 
  - Full time or par time: Need to think about how to operationalize this. By streaming length? 
- What variables to construct from chats? How to quantify the dependent variables?
  - from the messages themselves: 
    - the count of messages. 
    - Trying LDA, then use topic dummies as features. 
    - Or clustering/classification. (Maybe this is good when we have some theoretical concepts.)
    - Sentiments and emotions. 
  - from the rich message: emotes, badges. (cheermotes?) Cuz I think this kind of represent the weight of the message. 
- Variables videos + chats: ? 
- Questions:
  - User advice  ~ streamer strategy / streaming time choice?
  - If there's experimentation, state dependence? (How does the influence happen?)
- Amazon - twitch financial statement? I think this could be combined with the twitch tracker overall summary to generate some insights.
- Take a look at json and generator stuff.https://www.programiz.com/python-programming/json
- Explore the relationship between chat features and engagement level.
