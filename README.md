# twitch_project

This is a currently a public repository. I might change it to private this week. I could add your accounts as collaborators, or think of other ways to share these (maybe a link to the notebook on my drive/ pdf). 

By Oct 8th: 
- Link to the [proposal](https://docs.google.com/document/d/1NeULev_u3fpf7Zrn_sOdR7k33qzWW9lFx29LEjeLb14/edit?usp=sharing)
- Sample dataset construction and initial insights: Go to the notebook. I'm updating it regularly. 
- Archived dataset: [TwitchTracker](https://sullygnome.com/channels/30/followergrowth) This is a really impressive data collection. I'm using this to dig in, looking for patterns. As this site pulls the twitch API every 15 minutes since 2015, I'm thinking emailing the developer to collaborate, as he indicated no scraping please. But this site doesn't scrape viewer engagement (chats). 
- Literature review: Will post my database next week soon. 

By Oct 10th:
- Uploaded 10102020 notebook:
  - Workflow:
    - Go to [TwitchTracker](https://sullygnome.com/channels/30/followergrowth) to select a sample, download the csv.
    - Use the url there to retrieve broadcast id and info by calling the get_user endpoint.
    - Use the retrieved video id to get video info by calling the get_videos endpoint.
    - Use the retreived video url to get chat files using the [chatdownloader](https://github.com/xenova/chat-downloader/tree/master/docs) github project.  **remember to download it locally too.**
    - Examine the returned json chat files, see what variales to construct. 

Action items: 
- clean up the code. Loop it. (no need for separate scripts actually.)
- What variables to construct from chats? How to quantify the dependent variables?
