#### Search anchor by kmeans 
The anchor boxes is searched by kmeans. The number of cluster is defined as number of anchors. 

- How to evaluate if a anchor is good enough?
    - the relative size of label over anchor is larger than the threshold.
        - w(label)  / w(anchor) 
        - w(anchor) / w(label)
        - h(label)  / h(anchor) 
        - h(anchor) / h(label)

- steps of determining anchors 
    1. check if the predefined anchors meet the recall criterion
        - if best possible recall > 0.98, use the predefined anchors 
        - if not, use kmeans to search anchors(Step 2)  
    2. use kmeans to search anchors
        - find the clusters of width and height pairs
    3. fine tune the searched anchors to have a better best possible recall 
        - genetic algorithm

- Metrix
    - Recall of best anchor ratio
        - for each label, find its relative ratio of label's width and height over each anchor's width and height respectively
        - for each label, find the maximal relative ratio among its anchors
        - the recall = the number of labels which best relative ratio is larger than (1/threshold) / total of lablels
    - anchors above threshold: average # of anchors which is above threshold for a label


