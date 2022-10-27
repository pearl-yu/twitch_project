# twitch_project

This is a currently a public repository. I might change it to private this week. I could add your accounts as collaborators, or think of other ways to share these (maybe a link to the notebook on my drive/ pdf). 
- Link to the initial [proposal](https://docs.google.com/document/d/1NeULev_u3fpf7Zrn_sOdR7k33qzWW9lFx29LEjeLb14/edit?usp=sharing)
- Literature [notion page](https://www.notion.so/pearlyu/Working-on-a-research-question-f4e889d8cad645428feae3a91dd3e873)

<ins>Week1 - By Oct 8th:<ins> 
- Sample dataset construction and initial insights: Uploaded 10092022 notebook
- Archived dataset: [TwitchTracker](https://sullygnome.com/channels/30/followergrowth) This is a really impressive data collection. I'm using this to dig in, looking for patterns. As this site pulls the twitch API every 15 minutes since 2015, I'm thinking emailing the developer to collaborate, as he indicated no scraping please. But this site doesn't scrape viewer engagement (chats). 
- Uploaded 10102020 notebook:
  - Workflow:
    - Go to [TwitchTracker](https://sullygnome.com/channels/30/followergrowth) to select a sample, download the csv.  **Need to talk about sample selection. Currently it's stratified picking by fastest growth in last 30 days.**
    - Use the url there to retrieve broadcast id and info by calling the get_user endpoint.
    - Use the retrieved video id to get video info by calling the get_videos endpoint.
    - Use the retreived video url to get chat files using the [chatdownloader](https://github.com/xenova/chat-downloader/tree/master/docs) github project.  **remember to download it locally too.**
    - Examine the returned json chat files, think about what variables to construct. 

<ins>Week1 - Oct 12th meeting: <ins>
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
 
<ins>Week 2 - By Oct 19th: <ins> 
- About dependent variable: Plotted average weekly streaming time of 90 randomly selected streamers. Looks binormal.Using 30-hour to classify part-time and full-time sounds like the initial plan. 
- About features from chat files: Fit topic models on 90 videos, checked on correlation including lag 1 to guide theory building. 

<ins>Week 2 - Oct 20th meeting:<ins>
- Today we thought about **what's the interesting question** again: The idea is that streamers can experience burnout from managing interactions, unique to content creators in live streaming. Too many interactions/engagements with viewers might be too heavy of a workload. This might in a long term impact the streamers' streaming decisions. 
  - We think this question has a larger scope than the previous direction (which is to see if something in the chat impacts the streamers' decisions). 


<ins>Action items: <ins>  
- Download video files and chats. 
  - Chats all downloaded. Can also add another column of commenter status. 
  - Video manual download in progress. Large files! Need to think about scaling issues. 
- Basic chat features: number of messages, number of messages per minute, average message length, proportion of meaninful messages, message sentiments. (Runshan: I remember there are some techniques that allow you to separate texts are more emotional from those more factual (like objective comments, feedback, constructive suggestions), it would be useful to check this as well.)
  - Done: number of messages, number of messages per minute, average message length,message sentiments (pre-trained, can fine tune later).
  - Proportion of meaninful message: 
    - What's meaningful? We want to identify structures, test if dumb things only add on workload and burnout streamers, so some ratio. This is where theory comes from. Search for papers!
    - Simplest: count the number of messages that have certain keywords. Won't be accurate, but easy. Or, filter out things like yay, hi?
    - Sounds like classification task (more emotional, more factural, constructive suggestions). These sound like latent meanings. But do we want to manually label and train a model? Search for papers, like using embeddings and pretrained? Similar to sentiments I mean. Technical papers on live streaming chats. See if they have code publiclly available, or just papers where things can be improved technically. 
  - One thing: work on each message? or work on all messages as one document (I did this with LDA)? Document embedding?
  - Maybe just used pre-trained embeddings and train a linear regession?
- Measure engagement level: The number of times a streamer responds to a chat? The number of times that a streamer asks questions to the viewers? Check on the literature to get more ideas. 
  - Simple measure: The number of times a streamer asks the viewers a question? 
  - Simple measure: The number of times a streamer responds to a chat message?
  - how deep the loop of interaction is?
- Explore the relationship between chat features and engagement level.
  - Done: Streamingtime ~ chat messages. I think the roar of the crowd effect is promising. 

Literature reading:
- Communication patterns: interview frame, commentator frame, roar of a crowd frame. 
  - Roar of a crowed: like a chat waterfall. Good or bad? Create local meaning? Cognitive workload?
  - Interview frame: this is where conversation happens. 
  - Commentator frame: The streamer explaining the gameplay. Doesn't respond to chat that much. 
- Can map the transcript to the chat_df. 
***

<ins>Other random things: <ins>
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
- what's this? http://chatty.github.io/
- video captioning: https://github.com/Shreyz-max/Video-Captioning
- vidtotext: https://colab.research.google.com/gist/pszemraj/9678129fe0b552e114e3576606446dee/vid2cleantxt-minimal-example.ipynb#scrollTo=_wDj_xxXKapl
- https://codelabs.developers.google.com/codelabs/cloud-speech-text-python3#0
