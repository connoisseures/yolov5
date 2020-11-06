Function Block in Detail 
---

#### Search anchor by kmeans 
The anchor boxes is searched by kmeans. The number of cluster is defined as number of anchors. 

- How to evaluate if a anchor is good enough?
    - the relative size of GT bounding box over anchor is larger than (1/threshold).
        - w(GT bounding box) / w(anchor) 
        - w(anchor) / w(GT bounding box)
        - h(GT bounding box)  / h(anchor) 
        - h(anchor) / h(GT bounding box)

- steps of determining anchors 
    1. check if the predefined anchors meet the recall criterion
        - if best possible recall > 0.98, use the predefined anchors 
        - if not, use kmeans to search anchors(Step 2)  
    2. use kmeans to search anchors
        - find the clusters of width and height pairs
    3. fine tune the searched anchors to have a better best possible recall 
        - genetic algorithm

- Metric
    - Recall of best anchor ratio
        - for each GT bounding box, find its relative ratio of GT bounding box's width and height over each anchor's width and height respectively
        - for each GT bounding box, find the maximal relative ratio among its anchors
        - the recall = the number of GT bounding boxs which best relative ratio is larger than (1/threshold) / total of GT bounding boxes
    - anchors above threshold: average # of anchors of a GT bounding box which are above threshold


#### Data Loader 
dataloader is used to grep data and to preprocess data for training and testing jobs 

1. data loading 
    - if the dataset is loaded before, load dataset from cache file
    - to load the dataset first time, load dataset from image and annotation file
2. foramt conversion
    - xmin, ymin, xmax, ymax
    - x_center, y_center, w, h

3. data process 
    - options
        - rectangular training
        - data augmentation
        - mosaic
            ```python
            mosaic_active = rectangular_training == False and data_augmentation == True
            ```
    - rectangular training: use "letterbox" function to resize image to a 32-pixel-multiple rectangle 
        - keep the aspect ratio and do padding efficiently
    - mosaic: combine 4 pairs of image and annotation into a single one

4. data augmentation
    - augmentation in image space 
    - augmentation in color space 
    - augmentation by flipping


