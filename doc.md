#### Search anchor by kmeans 
The anchor boxes is searched by kmeans. The number of cluster is defined as number of anchors. 

- steps of determining anchors 
    1. check if the predefined anchors meet the recall 
        - if best possible recall > 0.98, use the predefined anchors, else use kmeans to search anchors(Step 2)  
    2. use kmeans to search anchors
        - clusters of width and hight pairs
    3. fine tune the searched anchors to have best possible recall 
        - genetic algorithm
- Metrix
    - Recall of best anchor ratio
        - for each label, find its relative ratio of label's width and hight over each anchor's width and hight respectively
        - for each label, find the maximal relative ratio among its anchors
        - the recall = the number of labels which best relative ratio is larger than (1/threshold) / total of lablels

