# [CVPRW 2025] McByte official implementation code.

<i>H there, thank you for your interest! We are currently preparing the clean version of our codebase, including demo scripts and instructions. The repository will be updated shortly after CVPR25. Stay tuned!</i>

>**[No Train Yet Gain: Towards Generic Multi-Object Tracking in Sports and Beyond](https://arxiv.org/abs/2506.01373)**
>
>Tomasz Stanczyk, Seongro Yoon, Francois Bremond
>
>[*arxiv 2506.01373*](https://arxiv.org/abs/2506.01373)

## Abstract
Multi-object tracking (MOT) is essential for sports analytics, enabling performance evaluation and tactical insights. However, tracking in sports is challenging due to fast movements, occlusions, and camera shifts. Traditional tracking-by-detection methods require extensive tuning, while segmentation-based approaches struggle with track processing. We propose McByte, a tracking-by-detection framework that integrates temporally propagated segmentation mask as an association cue to improve robustness without per-video tuning. Unlike many existing methods, McByte does not require training, relying solely on pre-trained models and object detectors commonly used in the community. Evaluated on SportsMOT, DanceTrack, SoccerNet-tracking 2022 and MOT17, McByte demonstrates strong performance across sports and general pedestrian tracking. Our results highlight the benefits of mask propagation for a more adaptable and generalizable MOT approach.

<p align="center">
  <img src="media/CVPRW25_main_diagram.png" width="60%" alt="Pull Figure of CAMEL">
</p>


## Installation
Perform the following steps in the terminal in the exact order as below:
```
https://github.com/tstanczyk95/McByte.git
cd McByte
pip3 install -r requirements.txt
python3 setup.py develop
pip3 install cython; pip3 install 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'
pip3 install cython_bbox
```

## Datasets

Download [SportsMOT](https://github.com/MCG-NJU/SportsMOT), [DanceTrack](https://drive.google.com/drive/folders/1ASZCFpPEfSOJRktR8qQ_ZoT9nZR0hOea), [SoccerNet-tracking 2022](https://www.soccer-net.org/data) and [MOT17](https://motchallenge.net/), and place them inside the data/ folder.


## Detectors and detections

Download the YOLOX object detetor weights for [SportsMOT](https://github.com/MCG-NJU/MixSort?tab=readme-ov-file#model-zoo), [DanceTrack](https://github.com/DanceTrack/DanceTrack/blob/main/ByteTrack/README.md) and [MOT17](https://github.com/FoundationVision/ByteTrack#model-zoo), and place them inside the detection_models/ folder.

Place the [SoccerNet-tracking 2022](https://www.soccer-net.org/data) oracle detections as well as your own custom detections inside the custom_detections/ folder. Please use the same format as SoccerNet detections.

## Evaluation
Run the script the get the tracking output and then use [TrackEval]() to obtain the performance numbers.
```
./scripts/run_tracking.sh ${DATASET}
```
DATASET can be: <i>sportsmot, dancetrack, soccernet, mot17.</i>

## Demo 
```
./scripts/run_demo.sh ${DATA_PATH} ${DET_TYPE} ${DET_PATH}
```
DATA_PATH is the path to your data (frames). DET_TYPE can be <i>model</i> or <i>custom</i>/ DET_PATH is the path to your object detection model or a text file to your custom detections.

