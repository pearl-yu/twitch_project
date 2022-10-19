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

By Oct 11th:
- Uploaded 10122020 notebook. 

Oct 12th meeting: 
1.	Made the research questions more clear: Take perspective of the platform, that cares about incentivizing the streamers to stay and grow on the platform. They’d want more ‘full time’ streamers as the content is delivered live. 
- Hence we model the streamers’ decisions.
2.	Dependent variables:
- Staying, or leaving the platform. 
- Streaming time – part time/ full time.
- Content choices: number of game categories. 
3.	Independent variables:
- Aside from e.g. views, follows, number of chat messages, first we want to dig in the chat files:
- Meta data includes the status of user who comments (if subscriber, VIP, prime subscriber, if streamer..)
- From the text,  LDA, sentiments, emotions are easy to extract. But it should start with what could be the interesting story. We talked about a few ideas. 
 
Plan of this week:
- We talked about the operationalization of the dependent variables. Construct those, and plot the distribution to see if there’s obvious (full-time, part-time) pattern. 
- With independent variables, we talked about a few interesting stories and ideas. Think about it again, and try to run regressions to test on those. 
- Continue on literature search relevant to content creators/streamers/digital entrepreneurship. 


By Oct 19th:
- Plotted average weekly streaming time of 90 randomly selected streamers. Looks binormal.
- Fit topic models on 90 videos, checked on correlation including lag 1. 
Things to do: 
- Check on some hypothesis: 
  - Balance of sentiments.
  - Look at the comments of people who paid.
- Sample selection
- Panel regression
  - Dependent variable (video level or weekly level?) ~ a bunch of controls + topic_distribution of lagged one.

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
