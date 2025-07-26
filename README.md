# Introduction
This project presents the code for the paper _Integrated Cross-Camera Framework for Efficient Worker Tracking and Robust Re-Identification_.

In the paper, an approach for Worker Tracking and Robust Re-Identification is proposed, By integrating a YOLO-World detector fine-tuned on construction datasets with an optimized BoT-SORT tracker, the system achieves real-time intra-camera tracking. Additionally, a CLIP-ReID encoder enables robust cross-camera re-identification via Hungarian assignment and ratio-based verification.

- ![Overview of the Our Method](https://github.com/SuperCarry2001/Integrated-tracking-and-ReID/raw/main/figure1.png)

# Updates
- Setup instructions and pseudocode are released. (2025.7)
- [Tracking Gradio Demo](https://github.com/NirAharon/BoT-SORT) is released. (2025.7) 

# Setup instructions and pipeline
## Tracking
- Git clone [Bot-SORT](https://github.com/NirAharon/BoT-SORT) link for tracking.
- ![Overview of the Our Method](https://github.com/SuperCarry2001/Integrated-tracking-and-ReID/raw/main/figure2.png)
```
# pseudocode
Initialize BoT-SORT (without Re-ID)
For each frame:
    Run detector → dets, scores, classes
    Predict tracks via Kalman filter
    Perform GMC motion compensation (keypoint matching, global transformation)
    Compute association cost matrix (IoU, optionally fuse with appearance distance)
    Data association (Hungarian algorithm)
    Update tracks (matched, unmatched)
Output results
```

## Re-ID
- Git clone [CLIP-ReID](https://github.com/Syliz517/CLIP-ReID) link for Re-ID.
- ![Overview of the Our Method](https://github.com/SuperCarry2001/Integrated-tracking-and-ReID/raw/main/figure3.png)
```
# pseudocode
Initialize gallery and local-to-global ID mapping
For each frame:
    For each detection:
        Extract features
        If enough frames: compute avg_feature
        If not yet assigned global ID: perform batch matching (Hungarian or ratio)
After all frames:
    Evaluate global ID assignment and cross-camera matches
Output results 
```

# Reference
Here are some great resources we benefit:
- YOLO-WORLD for detecting workers is from [YOLO-WORLD](https://github.com/AILab-CVC/YOLO-World).
- MOCS for training detector is from [MOCS dataset](http://www.anlab340.com/Archives/IndexArctype/index/t_id/17.html).
- BOT-SORT for tracking worker is from [Bot-SORT](https://github.com/NirAharon/BoT-SORT).
- Konstantinou dataset for tracking worker is from [Konstantinou dataset](https://zenodo.org/records/1218695)
- CLIP-ReID is from [CLIP-ReID](https://github.com/Syliz517/CLIP-ReID).
- Konstantinou and Brilakis dataset for Re-ID task is from [Konstantinou and Brilakis dataset](https://zenodo.org/records/839674).
