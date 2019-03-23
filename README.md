# DCU_project-01-Competition-MediaEval

Task: Predicting Media Memorability
(http://www.multimediaeval.org/mediaeval2018/)

As part of the MediaEval 2019 Benchmarking Initiative for Multimedia Evaluation, I was expected to design systems that automatically **predict memorability scores for videos**, which reflect the **probability** of a video being remembered. 

> An important motivation for **video memorability (VM) prediction** derives from the need for new techniques that can help to organize and retrieve digital content, to make it more useful in our daily lives. Like other cues of video importance, such as aesthetics or interestingness, **memorability** can be regarded as useful to help make a choice between comparable videos. Consequently, a large number of applications, e.g., education and learning, content retrieval and search, content summarization, storytelling, targeted advertising, content recommendation and filtering, would benefit from **our computational models** capable of ranking videos according to their memorability. Despite its potential of being an active area of reseach in the computer vision community, VM prediction suffers from two main obstacles:
 - No clear definition of VM has been established, nor does a common and unified protocol for its measurement exist, contrary to what can be found in the literature for image memorability.
 - No large-scale dataset is available, for the community to build our models. The purpose of this task is therefore to propose a public benchmark to assess the memorability of videos, based on a publicly released large-scale dataset and on an objective and clear measurement protocol.
 - [Task]
   - Goal: Build systems that are capable of predicting how memorable a video is, by computing for each video a **memorability score**. Participants are required to train computational models capable of inferring **memorability from visual content**. 
   - A. Dataset Fields:
     - __0.video file names:__ 10,000 short soundless videos shared under a license that allows their use and redistribution in the context of MediaEval 2018. These 10,000 videos were split into 8,000 videos for the development set and 2,000 videos for the test set. They were extracted from raw footage used by professionals when creating content. Of 7s-duration each, they are varied and contain different scenes types. 
     - __1.Annotations:__ the dataset comes with both **"short-term"** and **"long-term"** memorability "annotations" (expecting long-term memorability annotations to be more representative of the performance, and more relevant in many applications).
     - __2.Descriptive titles:__ Each video also comes with its original title. These titles can often be interpreted as a list of tags (textual metadata) that might be useful to infer the memorability of the videos. Participants are free to use them or not.
     - __3.pre-computed content descriptors:__ 
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

   - B. Ground Truth dataset
     - 1. Protocol to measure video memorability(recognition tests)
       - Participants viewed a sequence of 180 various videos they were unfamiliar with, 40 of which being targets videos, i.e., repeated videos, and the other being fillers, i.e., videos that occurred only once. Their task was to press the space bar whenever they detected a repetition. After 24 to 72 hours, participants viewed a new sequence of videos consisting of 40 targets, which were videos randomly chosen from the fillers of the first part, and 120 new fillers. memory performance was therefore measured twice: a few minutes after memorization and again (on different items) 24-72 hours later. Thus, the dataset comes with both short-term and long-term annotations. These two scores will allow a comparison of the participants’ systems for both short and long term memorability prediction. However, because of the difficulty to collect data after a long delay through crowdsourcing, the number of annotations is bigger for short-term memorability scores than for long-term ones. On average, each video received 38 and 13 annotations in the short-term and long-term recognition task, respectively. For each video in the development set, we provide the number of annotations for both tasks.
     - 2. Memorability scores calculation
       - We assigned an initial memorability score to each video, defined as the percentage of correct detections by participants, for both short-term and long-term memory performances. The percentage scores are presented as floats in the interval [0,1].


It consists of
 - the video's name given as videoX.webm 
 - its short-term memorability score.
 - No.of annotations which was used to calculate its short-term memorability score.
 - its long-term memorability score.
 - No.of annotations which was used to calculate its long-term memorability score.










































