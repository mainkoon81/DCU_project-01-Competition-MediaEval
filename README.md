# DCU_project-01-Competition-MediaEval

This challenge comes from the MediaEval conference. Every year academics propose new datasets for machine learning tasks, and teams compete against each other to see who can get the highest accuracy. This is done by providing a test-set where participants do not have access to ground truth. The participants upload predictions, and the organizers grade them on the results of this testset.

Task: Predicting Media Memorability
(http://www.multimediaeval.org/mediaeval2018/)

As part of the MediaEval 2019 Benchmarking Initiative for Multimedia Evaluation, I was expected to design systems that automatically **predict memorability scores for videos**, which reflect the **probability** of a video being remembered. 

> An important motivation for **video memorability (VM) prediction** derives from the need for new techniques that can help to organize and retrieve digital content, to make it more useful in our daily lives. Like other cues of video importance, such as aesthetics or interestingness, **memorability** can be regarded as useful to help make a choice between comparable videos. Consequently, a large number of applications, e.g., education and learning, content retrieval and search, content summarization, storytelling, targeted advertising, content recommendation and filtering, would benefit from **our computational models** capable of ranking videos according to their memorability. Despite its potential of being an active area of reseach in the computer vision community, VM prediction suffers from two main obstacles:
 - No clear definition of VM has been established, nor does a common and unified protocol for its measurement exist, contrary to what can be found in the literature for image memorability.
 - No large-scale dataset is available, for the community to build our models. The purpose of this task is therefore to propose a public benchmark to assess the memorability of videos, based on a publicly released large-scale dataset and on an objective and clear measurement protocol.

**In this memorability challenge,** the data was collected by showing participants 9-second videos. Then, a few minutes later the participants were shown a series of multiple videos. If they remembered the video, they were told to press a button. This was repeated for a number of participants, and the `memorability score was the average of the proportion of people who remembered the video`. For example, if the video was shown to 30 people, and 20 of them remembered the video, the memorabilility score was 0.6667. This experiment was then repeated 24-72 hours later. So each video has 2 memorability scores - one short term and one long term. Hence there were seperate tasks, predicting both the short term and long term memorability.
 
 - [Task]
   - Goal: Build systems that are capable of predicting how memorable a video is, by computing for each video a **memorability score**. Participants are required to train computational models capable of inferring **memorability from visual content**. These 10,000 videos were split into 8,000 videos for the development set and 2,000 videos for the test set. They were extracted from raw footage used by professionals when creating content. Of 7s-duration each, they are varied and contain different scenes types. We will get only 6,000 from the training set?????? 
   
   - A. Datasets Available  
       - __1.Caption dataset:__ (6000 x 2)
         - it has the video's `name` given as videoX.webm, and each video also comes with its original title. These titles can often be interpreted as a list of tags (textual metadata) that might be useful to infer the memorability of the videos. Participants are free to use them or not.
       
       - __2.pre-computed content descriptors:__ 
         - a) video-dedicated features
           - **C3D:** spatio-temporal visual features:
             - obtained by extracting the output of the final classification layer of the C3D model(3-dimensional convolutional network proposed for generic video analysis).
           - **HMP:** the histogram of motion patterns for each video.
         - b) Additional frame-based features:
           - For First/Middle/Last Frame for each video,
             - **HoG descriptors** (Histograms of Oriented Gradients) are calculated on 32x32 windows on a grey scale version of each frame; 
             - **LBP** (Local Binary Patterns) are calculated for patches of 8x15 pixels; 
             - **InceptionV3 features** correspond to the output of the fc7 layer of the InceptionV3 deep network; 
             - **ORB** features result from a fusion of FAST keypoint detector and BRIEF descriptor 
             - **Color histograms** are computed in the HSV space.
         - c) Aesthetic visual features:
           - Composed of **color, texture and object** based descriptors, aggregated through the computation of their mean and median values, AVF are extracted for each 10-frame of one single video.
           
       - __3.Ground Truth dataset:__ (6000 x 5)
         - a) Protocol to measure video memorability(recognition tests)
           - Participants viewed a sequence of 180 various videos they were unfamiliar with, 40 of which being targets videos, i.e., repeated videos, and the other being fillers, i.e., videos that occurred only once. Their task was to press the space bar whenever they detected a repetition. After 24 to 72 hours, participants viewed a new sequence of videos consisting of 40 targets, which were videos randomly chosen from the fillers of the first part, and 120 new fillers. memory performance was therefore measured twice: a few minutes after memorization and again (on different items) 24-72 hours later. Thus, the dataset comes with both short-term and long-term annotations. These two scores will allow a comparison of the participants’ systems for both short and long term memorability prediction. However, because of the difficulty to collect data after a long delay through crowdsourcing, the number of annotations is bigger for short-term memorability scores than for long-term ones. On average, each video received 38 and 13 annotations in the short-term and long-term recognition task, respectively. For each video in the development set, we provide the number of annotations for both tasks.
           
         - b) Memorability scores calculation
           - We assigned an initial memorability score to each video, defined as the percentage of **correct detections by participants**, for both short-term and long-term memory performances. The percentage scores are presented as floats in the interval [0,1]. 
           - The short-term raw scores are further refined by applying a linear transformation that takes into account the memory retention duration to correct/normalize the scores. ????
           - Indeed, in our measurement protocol, the second occurrence (i.e., repetition) of a video happens after variable time intervals. Using a similar approach for images, it has been shown that memorability scores change as a function of the time interval between repeats **while memorability ranks are largely conserved**. We were able to prove the same relation for videos.
           - we use this information to apply a correction to our raw memorability scores to explicitly account for the difference in interval lengths, with the objective for our short-term memorability scores to be the most representative of the typical memory performance after the max interval (i.e., 100 videos). Because we observed that memorability decreases linearly when the retention duration increases, we decided to apply a linear correction. Nevertheless, note that the applied correction only has a little effect on the memorability scores both in term of absolute and relative values. On the contrary, we did not apply any correction for long-term scores. Indeed, we observed no specific relationship between retention duration and long-term memorability from our collected scores. This was expected from what can be found in the literature: according to our protocol, the second measure was carried out 24 to 72 hours after the first measure. After such a long retention duration, it is expected that the memory performance is no more subjected to substantial decrease due to the retention duration.
           
         - c) Annotations
           - the dataset comes with both **"short-term"** and **"long-term"** memorability "annotations" (expecting long-term memorability annotations to be more representative of the performance, and more relevant in many applications).
           
         - d) In sum, it consists of
           - the video's `name` given as videoX.webm 
           - `its short-term memorability score`.
           - No.of annotations which was used to calculate its short-term memorability score.
           - `its long-term memorability score`.
           - No.of annotations which was used to calculate its long-term memorability score.

   - B. Run
     - 10 runs, i.e. 5 per subtask
       - Short-term memorability subtask – required run: Any information (extracted from the content, the provided features, the short-term memorability scores or external data) is allowed to build the systems, except the use of the long-term memorability scores which is not allowed.
       - Long-term memorability subtask – required run: Any information (extracted from the content, the provided features, the long-term memorability scores or external data) is allowed to build the systems, except the use of the short-term memorability scores which is not allowed. 
       - Apart from these required runs, any additional run for each subtask will be considered as a general run, i.e., anything is allowed, both from the method point of view and the information sources.
     
   - C. Evaluation for this regression
     - For both subtasks, the official evaluation metric will be the Spearman’s rank correlation between the `predicted memorability scores` and the `ground-truth memorability scores` computed over all test videos. Although the task remains a prediction task, only the ranking of the different videos will be evaluated by the official metric.
     - The choice of the **Spearman’s rank correlation** as official measure indeed corresponds to a desire of normalizing the output of the different systems and making the comparison easier. For this reason, participants are encouraged to really consider the task as a prediction task. Other classic metrics (i.e., Pearson correlation and Mean squared error) will also be computed and provided to the participants for the sake of comparison between the different runs and systems.








































