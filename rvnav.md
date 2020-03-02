---
layout: writeup
title: RV Nav
subtitle: https://www.rvnav.com/
image: /img/rvnav_logo.PNG
gh-repo: https://github.com/Labs17-RVNav
---
Empowered by a comprehensive data set of U.S. bridges and tunnels, RV Nav allows users to safely reach their destination without opening up their vehicle like a tin can. Plan your trip ahead of time with our turn-by-turn directions. We'll also try to notify you of potholes along the way!

**Language:** Python(pandas) **Frameworks:** Fast.ai **Services:** AWS

### Intro and Onboarding
RV Nav was an 8-week endeavor into the product development cycle, allotting a team of developers a window of time to onboard an agile but flexible product strategy while meaningfully contributing to an unseen codebase. For me, this meant immersing myself in a new mindset and being willing to openly collaborate with a talented team of web, UX, and data science developers.

The data science team took on three separate tasks: increase the number of bridges in the database, prototype an image classification neural network to identify road hazards, and build an in-house pipeline that provided RV related insights from reviews on the web. 

### The Data
**Bridges and Tunnels**<br/>
Our sole source was decided to be [The U.S. Department of Transportation: Federal Highway Administraion](https://www.fhwa.dot.gov/bridge/nbi/ascii2018.cfm). They have a robust and current public database for both bridges and tunnels. We restricted the clearnaNce window from a lower bound at 7 feet to an upper bound of 20 feet, reformatted the GPS coordinates to a decimal format to be compatible with ARCGIS, and dropped the remaining unused columns. In total, roughly 80,000 new bridges were added.

![](/img/regex-to-decimal.PNG)
![](/img/bridge_clearance_df.PNG)

**Roadway Images**<br/>
Images of varying roadway content were gathered from the web including pictures of potholes, animals, oil spills, traffic, and unoccupied streets. 

![](/img/roads-and-potholes.PNG)

**Buisness Reviews**<br/>
Roughly 500 items of text related to RV's and travel were collected from popular app distribution sites.
![](/img/scrape-code.PNG)

### Backend API
Using Amazons Elastic Beanstalk to host our API, we redeployed the updated source package to include the new bridge data.

### Classification Neural Net
Following along with tutorial videos and notebooks from [Fast.ai](https://www.fast.ai/), we were able to quickly produce a trained convolutional neural net that boasted a ~95% accuracy score on the test data for images containing road hazards. Additional layers were trained on top of the resnet18 model and validated against a data set of 200 images unseen in training.

![](/img/resnet18-cnn-train-cycle.PNG)
![](/img/resnet18-cnn-confusion-matrix.PNG)

### NLP pipeline
Sentiment analysis was performed and visualized on the review data.<br/>
(Scattertext by teammate George Hou) [Link](https://gyhou.com/RV-Parks-Campgrounds-Yelp-Reviews-Scattertext.html) to interactive.

![](/img/george_hou_scatter_text.PNG)

### Retrospective and TO-DO's
I'm glad to have had the opportunity to work in a production environment. Almost every deliverable we produced here I would like to take to the next level. For the neural net, it would be cool to make the jump to object detection in near real-time from mounted hardware and apply more extensive testing and evaluation. Building an automated bot to crawl troves of street image cataloging bridge heights would be a fun challenge. Deploying a generalized tool for text analysis and visualization is something I'd like to work on as well.

Here's a rv-navi-GATOR for posterity
![](/img/rv_navigator.png)



  



[Web App](https://www.rvnav.com/)---[Github repo](https://github.com/Labs17-RVNav)
