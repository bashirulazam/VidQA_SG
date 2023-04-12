# SHG-VQA
Learning Situation Hyper-Graphs for Video Question Answering [CVPR 2023]

[Aisha Urooj Khan](https://scholar.google.com/citations?view_op=list_works&hl=en&hl=en&user=ceiuCp4AAAAJ), [Hilde Kuehne](https://hildekuehne.github.io/), [Bo Wu](https://scholar.google.com/citations?user=6ozI_ZMAAAAJ&hl=en), Kim Chheu, Walid Bousselhum, [Chuang Gan](https://people.csail.mit.edu/ganchuang/), [Niels Da Vitoria Lobo](https://www.crcv.ucf.edu/person/niels-lobo/), [Mubarak Shah](https://www.crcv.ucf.edu/person/mubarak-shah/)

[`Website`]() | [`Paper`](https://www.crcv.ucf.edu/wp-content/uploads/2018/11/2023072364-4.pdf) | [`BibTeX`](#citation)

Official Pytorch implementation and pre-trained models for Learning Situation Hyper-Graphs for Video Question Answering (coming soon).

## Abstract
Answering questions about complex situations in videos requires not only capturing the presence of actors, objects,
and their relations but also the evolution of these relationships over time. A situation hyper-graph is a representation that describes situations as scene sub-graphs for video frames and hyper-edges for connected sub-graphs and has been proposed to capture all such information in a compact structured form. In this work, we propose an architecture for Video Question Answering (VQA) that enables answering
questions related to video content by predicting situation hyper-graphs, coined Situation Hyper-Graph based Video Question Answering (SHG-VQA). To this end, we train a situation hyper-graph decoder to implicitly identify graph representations with actions and object/human-object relationships from the input video clip. and to use cross-attention between the predicted situation hyper-graphs and the question embedding to predict the correct answer. The proposed method is trained in an end-to-end manner and optimized by
a VQA loss with the cross-entropy function and a Hungarian matching loss for the situation graph prediction. The effectiveness of the proposed architecture is extensively evaluated on two challenging benchmarks: AGQA and STAR. Our results show that learning the underlying situation hypergraphs helps the system to significantly improve its performance for novel challenges of video question-answering task.

<p align="center">
<img src="shg.png" width=90% height=90% 
class="center">
</p>

### Proposed SHG-VQA Architecture
<p align="center">
<img src="architecture.png" width=100% height=100% 
class="center">
</p>


### Datasets
We report results on two reasoning-based video question answering datasets: [AGQA](https://cs.stanford.edu/people/ranjaykrishna/agqa/) and [STAR](https://bobbywu.com/STAR/). 

Instructions to preprocess AGQA and STAR (to be added)

#### AGQA
Download train and val split for the balanced version of AGQA 2.0 we used in our experiments from [here](https://drive.google.com/file/d/17_rqCnR9whlXRPd9RfubhPUP8oLCFD4b/view?usp=sharing).

###### Questions:
* We randomly sampled 10% of questions from the training set to be used for the validation set
* Train/Valid/Test files are formatted as a list of dictionaries, containing all information given by AGQA.
    * Format: [{"question": "Before starting to open a bag, what was the person taking?", "answer": "paper", "video_id": "3ZUVI", "global": ["obj-rel"], "local": "v023", "ans_type": "open", "steps": 4, "semantic": "object", "structural": "query", "novel_comp": 0, "more_steps": 0, ...}]

###### Answers:
* We iterated through all ground-truth answers in the training/validation set to get all answer choices.
* All possible answers are mapped to an index and stored in the answer vocab.
    * Format: {"answer1": 0, "answer2": 1, ...}


###### Video Frames:
* Download the videos and their frames from the Charades dataset.
* We randomly sampled a fixed clip-len from these frames.
    * trimmed_frame_ids.json file:
        * Contains pre-trimmed and sampled frames of clip length 16
        * Format: {vid_id1: [frame#, frame#,...], vid_id2: [frame#, frame#,...],...}

###### Triplets
* AGQA provides "scene graphs" and object/relationships/action classes.
* We iterated through the given scene graphs for each video's frame and created triplets in the form of: (person, relation, object)
    * frameTriplets.json:
        * Format: {vid_id: {frame#: [(triplet), (triplet)], frame#: [(triplet), (triplet)]}, ...}

* For the given action classes, we list all actions found in each video frame.
    * frameActions.json:
        * Format: {vid_id: {frame#: [(action), (action)], frame#: [(action)]}, ...} 

* All unique triplets and actions are mapped to an index for easy reference in the code.
    * relationship_triplets.json: {(triplet): 0, (triplet): 1, ...}
    * action_dictionaries.json: {action: 0, action: 1, ...}



### Citation
If this work and/or its findings are useful for your research, please cite our paper.

### Questions?
Please contact 'aishaurooj@gmail.com'
