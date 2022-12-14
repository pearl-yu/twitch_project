# twitch_project

This is a currently a public repository. I might change it to private this week. I could add your accounts as collaborators, or think of other ways to share these (maybe a link to the notebook on my drive/ pdf). 
- Link to the initial [proposal](https://docs.google.com/document/d/1NeULev_u3fpf7Zrn_sOdR7k33qzWW9lFx29LEjeLb14/edit?usp=sharing)
- Literature [notion page](https://www.notion.so/pearlyu/Working-on-a-research-question-f4e889d8cad645428feae3a91dd3e873)
- Writeup [overleaf](https://www.overleaf.com/project/632876ce63765e6f8f6fcff5)
 
Collecting the api meta data: data_collection
Merge in other variables: independent_varaible_exploration 
Processing raid data and merge: raid_data 
processing videos and transcripts: vidtot_processing  streamer_action
interaction: interaction_variable
model: modeling

 
***  
[Week 1](#week1)
[Week 2](#week2)
[Week 3](#week3)
[Week 4](#week4)
[Week 5](#week5)
[Week 6](#week6)
[Dec 7th](#dec7)
[Dec 14th](#dec14)
[Dec 15th](#dec15)

[Data Construction](#data) [Other Random Thoughts](#random)

<ins>Dec 15th meeting<ins>   <a name="dec15"></a>.   
Done this week: 
 - Downloading sample audios.(Want to write a better script for future 60thou downloads).
 - Tried to manually label interaction from audio files to get intuition. Re-read the two papers discussing interaction patterns. 
   Q in meeting: Complicated ones - complicated. Simple measure? 
   respond to chat. 
   dialogue.
   stricter.(seeking / respond /obviously not interacting.) Threshold.

Tasks:
- Task of Thursday: Write up. (literature part, data part, especially modeling part). Need to read the papers with HMM. 
- Task 1: Getting that intereaction variable. Mostly deal with the engineering stuff this week. 
- Task 2: Simulation.

<ins>Dec 14th <ins>   <a name="dec14"></a>
When videos are invovled, there would be quite some technical work:
- It's not possible to transcribe the videos without downloading them. 
  - So we gotta find a way to download the vids faster. The GUI doesn't work the best. So I think we need to find a script and run it parrallelly.
- Having the video files, which are large on a harddrive, next step is to trascibe. 
  - It takes 6m to convert an 1-hour video to audio. 
  - Accuracy: Simple wav2text model gives out gibberish word. 
  - Need to find a way to extract audios faster, and also something to correct for gibberish word. (Google caption service charges a fee. The Facebook wav2vec doesn't. We may need finetuning in the future, but not now.)
- With the transcript, we need to construct an 'interaction variable'. 
  - There could be gaming background voice. 
  - How do we define interaction, or interaction levels? Is there any literature that classify it?
  - Attend to viewer chats./ Attend to the game itself. 
 
 Task of this week 1 (priority): It's slow. Try to parallel the process, ask Joao for some help.   
 Task of this week 2: The specification of the second and third term could be improved. Look up content creators literature, empirical/modeling/analytical models. 
 Task of this week 3: Write things up. I've got the doc here, but after the meeting, I plan to further clarify the story we want to tell, simple literature review, model-free evidence, and the modeling part, write up the likelihood, data parts too. Will share the doc again next Monday.    
 Task of this week 4: Try to code up a toy model, get intuition of how it's done.    

<ins>Dec 7th <ins>   <a name="dec7"></a>
- Variable construction with ML: 
   - Compiled the code to download and transcribe videos - to get the streamer response variable. Maybe enough to try estimation. 
- Modeling: 
  - Further understanding of the modeling components, and the estimation procedures with the continuous decision variable.  
  - U_interaction = \beta Chat_intensity + the benefit from responding + the cost of responding. 
  - Single-agent dynamic model, with a HMM. (The story makes sense with latent mental states. ) (Will share the list of references/helpful modeling papers with the writeup as in task 3 below. )

<ins>Week 6 <ins>   <a name="week6"></a>
- More sampling points: 
  - Initial idea: Use the [TwitchTracker](https://sullygnome.com/channels/30/followergrowth) to select a sample of streamers, and check on [raid finder](https://streamscharts.com/tools/raid-finder) 
  - Problem: Still, how to select a 'random sample'? Let me google this. / Also, is it ok to focus on some variable 
  - Think about identification and the model.

<ins>Week 5  <ins>   <a name="week5"></a>
- Raid:
  - Eyeballing the viewership pattern: 
    - A bump of viewership by a large raid, but most people leave after a while. Many small raids don't matter a lot. 
    - I can't see the real-time chat stats, but just the viewership on the website interface. 
    - It's my guess that we'll need to **find large raid that might impact chat intensity.**
  - Collected raids data for the sample dataset. 
    - If exogenous: 
      - Checking on the incoming raids, if it's reapeated from someone (ruling out raiding streamers systematically choosing whom to raid, trying to form bond etc).
      - They usually raid smaller streamers playing the same game live when my own stream ends. Or look for advice from the audience. Somep people check if the other streamer is engaging the viewers, so maybe there is some selection that they generally choose streamers who engage with the audience. I don't think this hurts our study that much tho. 
  - Constructed number of total raiders into the dataset.
    - Video level correlation about 0.2. **But maybe we should just look at large raids?**
    - **Maybe I should run regressions too, but what regression?** 
    - I think the sample is too small. We need more videos got raided big. Maybe I should collect some of that dataset. 
- Interaction types: 
  - Get back on it tonight. Should be fun. 
  - To do: Add the streamer responses as a dependent variable too. (chat features -> streamer responses -> burnout?)  
  - To do: Apply ML to identify interactions and interaction types. Try captioning with timestamps. Don't overcomplicate this tho. Continue on these.

<ins>Week 5 - Nov 10th Meeting <ins> 
Still studying identification with twitch raids:
- The number of raiders directly increases viewership, and seems to be positively correlated with chat intensity. But regression of [chat_intensity ~. #raiders] is not significant even without including other controls. We think this is because the sample is not enough to have many live streams with a large number of raiders (A large percentage never got raided), hence little variation. 
- Basically not enough variation n correlation. Need more data points that got raided big. 

<ins>Week 4 <ins>   <a name="week4"></a>
- Added in another measure of #messages_per_minute. Add in quadratic terms. 
- Identify responses: in the work. Here's the workflow:
  - automatic transcription (speech-to-text, open AI API.) (Talked to Joao, there is a way to identify usernames, but looking for out-of-the-box solutions.)
  - Manual label a few. 
  - Finetune maybe a RobertaBert model (hugging face is helpful. I think I'm gonna switch to that. The only downside, but helps everything later, is to figure out the I/O, also procedures. They have tutorisl. https://huggingface.co/course/chapter1/4?fw=pt) 
- Furether identify chat labels: in the work. need to get familiar with the conversational act stuff. 
- Identification strategies: I read the Raluca suprise and suspense paper. Severals confusing things. 
  - Viewers usually see something the streamer is doing, then send chats. Reversed causality. 
  - raid: [how raid works](https://help.twitch.tv/s/article/how-to-use-raids?language=en_US) [helpful tool](https://streamscharts.com/tools/raid-finder) 

<ins>Week 4 - Nov 3rd meeting: <ins>   
- Raid could be conditional random, random within a range. (There gotta be randomness, but need to tease it out.) Like the big streamer might be choosing from a group of othere streamers to raid. Are these streamers similar? Check on that.
- The idea is to find something that causes an increase in viewership, then number of messages for example. 
- Reverse causality might be taken care of by raids. Any confounders?
  
  
<ins>Week 3 <ins>   <a name="week3"></a>
- From regressing streaming time on chat features (controlling for streamer and date fixed effect.): #messages_per_minute negative sign. This crudely measures 'the roar of the crowd' (chat intensity), which suggests that if suddenly there appears a waterfall of chat messages, it might increase the streamers' cognitive load. There're other posisble explanations, need to add in more variables and check the results again. positive_sentiment_proportion, positive sign. #messages, positive sign. 
- From the literature review: One stream studies communication patterns under live streaming: interview frame (where streamers are having conversations with the viewers), commentator frame (where streamers mostly talk about gameplay), 'roar of the crowd' (waterfall of viewer chats, hard to process.) / Other helpful papers: The notion of the sync between video and chat; (Some ideas: One possible thing is that shifting patterns or trying to mix patterns increases the streamers' workload. ) 
- On quantifying interactions/ streamer engagement: Downloaded the videos and transcribed them. Simple methods to extract interactions don't seem to work. Might need some ML methods to identify, for example, the number of times that a streamer interacts with viewers. Also want to try captioning with timestamps.
  
<ins>Week 3 - Oct 27th meeting: <ins>   
- Continue on technical stuff. 
- Think about identification. Does the raid thing can work?
- Research question again (Runshan's summary):
  > the current research question is how does viewer engagement intensity affect streamer decisions. The hypothesis is that if viewer engagement is too low, the streamer would be discouraged to stream (which is obvious), but if viewer engagement is too high (and disorganized), streamers may feel overwhelmed. They may choose to decrease the interactions (e.g. not respond to questions, not react to comments, etc.), or if they not choose to decrease the interactions, they may get burnout and decrease streaming time or frequency. Either would be bad for the platform. Potential remedy includes to put better structure on viewer engagement (e.g. group chat messages, extract key words, allow votes, etc.)
  > The more general idea is that streamer-viewer interaction is the key to live-streaming and what differentiate it from VOD. Previous literature has focused on how to increase viewer engagement, and we can study what affect streamer decisions, because interaction is by definition two-way. 
    
<ins>Week 2 <ins> <a name="week2"></a>
- About dependent variable: Plotted average weekly streaming time of 90 randomly selected streamers. Looks binormal.Using 30-hour to classify part-time and full-time sounds like the initial plan. 
- About features from chat files: Fit topic models on 90 videos, checked on correlation including lag 1 to guide theory building. 

<ins>Week 2 - Oct 20th meeting:<ins>
- Today we thought about **what's the interesting question** again: The idea is that streamers can experience burnout from managing interactions, unique to content creators in live streaming. Too many interactions/engagements with viewers might be too heavy of a workload. This might in a long term impact the streamers' streaming decisions. 
  - We think this question has a larger scope than the previous direction (which is to see if something in the chat impacts the streamers' decisions). 

<ins>Week1 <ins> <a name="week1"></a>
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
- Made the **research questions** more clear: Take perspective of the platform, that cares about incentivizing the streamers to stay and grow on the platform. They???d want more ???full time??? streamers as the content is delivered live. 
  - Hence we model the streamers??? decisions.
- Dependent variables:
  - Staying, or leaving the platform. 
  - Streaming time ??? part time/ full time.
  - Content choices: number of game categories. 
- Independent variables:
  - Aside from e.g. views, follows, number of chat messages, first we want to dig in the chat files:
  - Meta data includes the status of user who comments (if subscriber, VIP, prime subscriber, if streamer..)
  - From the text,  LDA, sentiments, emotions are easy to extract. But it should start with what could be the interesting story. We talked about a few ideas.  
 
 
<ins>Dataset construction progress (keep updating) <ins>    <a name="data"></a>
  
The focus was basic chat features, and measurement of engagment between streamer and viewer.    
Measure engagement level: The number of times a streamer responds to a chat? The number of times that a streamer asks questions to the viewers? Check on the literature to get more ideas. (working on this. I think simplest is to get transcripts and fine tune a model. )
  - Simple measure: The number of times a streamer asks the viewers a question? 
  - Simple measure: The number of times a streamer responds to a chat message?
  - how deep the loop of interaction is?
  
Videos and chats:
- Collected sample: 100 videos. downloaded 30 videos. downloaded all chats. (Have the script.)
- Action items:
  - Think about the random sampling again, what data variation we need to have. The script is ready, but need to store and scale. 

Chat features:
- Done: number of messages, number of messages per minute (intensity measure), aaverage number of messages per minute, average message length,message sentiments (pre-trained, can fine tune later).
- Action items: 
  - Portion of meaningful messages. 
    - What's meaningful? We want to identify structures, test if dumb things only add on workload and burnout streamers, so some ratio. This is where theory comes from. Search for papers!
    - Simplest: count the number of messages that have certain keywords. Won't be accurate, but easy. Or, filter out things like yay, hi?
  - Can use conversational act algos to get labels automatically: emotion/ statement/ question
  - If that is responded by the streamer. -> proortion of chats that got responses. 
  
Video features:
- Done: transcript.
- Action items: 
  - label the transcript, use bert to classify if that sentence is a response. 
  
***

<ins>Other random things: <ins> <a name="random"></a>
- Organize raid data, check on similarities between viewers of raided vids, length etc. 
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
