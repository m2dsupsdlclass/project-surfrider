# project-surfrider

Instructions and code for the course project - based on ONG Surfrider detection of plastics in rivers

WIP. Todos

- [ ] Inlcude a Link to surfrider/mot trained model
- [x] Describe the project / context
- [x] Describe the objectives / grading
- [ ] Build a notebook with simple download / treatment of data
- [ ] Build evaluation procedure and metrics
- [x] List model references

## Surfrider - Plastic Monitoring on Rivers

This course project makes use of an ongoing open source project led by [Surfrider Europe](https://surfrider.eu/), which aims at quantifying plastic pollution in rivers through space and time.
Plastic Waste in oceans mostly comes from rivers (80%), and it is very difficult to
This will be used to monitor river banks to take local decisions, measure effectiveness of policies at local and global scales, and has thus a very concrete importance.

In practice, video streams are captured on river river banks from kayaks (with their geolocalisation), and then fed to a model which aims at quantifying the number and types of objects.
There are three types (classes) of plastic litter:
- ![Plastic Bottles](/imgs/bottle.png?raw=true "Plastic Bottles")
- ![Plastic Framents](/imgs/fragment.png?raw=true "Plastic Fragments")
- Other types of waste

## Organization / format

- Groups of 2 people
- The ouptut is a 5 minutes recording of you describing what you did over slides or a notebook
- Note that:
  - You should rehearse the recording so that it is easy to understands and fits strictly within the 5 minutes (fair comparison implies we will stop the recording at 5min)
  - Don't waste your time re-explaining the basis of the project, but rather what you decided to build, why it is relevant, what you achieved, what you would do if in future work.
  - Try to be original: don't stick with the simplest, test new models and be audacious! this is the best way to learn.
- The project will account for 1/3 of the final grade

## Baseline

You may use the notebook and scripts in this repository to download necessary resources.

You can download a training dataset on this [link](http://files.heuritech.com/raw_files/dataset_surfrider_cleaned.zip).

The actual ongoing project is open source

## What to do

Your goal is to build a plastic detection model as useful as possible.
To do so, you may optimize the following:
- Have the best performance in terms of average precision of detected objects
- Have the least amount of false positives when running on rivers that do not include garbage

 Pick up one idea from the list below:
 - Improving the data:
  - by using smart data augmentation schemes,
  - unlabeled data (from provided videos for instance), or newly labeled data
  - external data (for instance [TACO](http://tacodataset.org/))
 - Improving the model:
  - A more recent Object detection architecture is the most straightforward way to improve performances, see references below. You may reuse existing code and improve on it. Be warned, object detection models are rather hard to implement from scratch.
  - From Object detection to Segmentation (will probably require additional labels: masks)
 - Your own idea!

### Advanced possibilities

If you want to go further:
- Build a tracking system on sequential video frames
- Try and compress the network to make it usable within a mobile application (you may consider [TensorflowLite](https://www.tensorflow.org/lite/models/object_detection/overview))

### Model References

#### Single Stage Detectors

- YoloV3 with associated Tensorflow code: https://github.com/zzh8829/yolov3-tf2
- RetinaNet https://github.com/fizyr/keras-retinanet

#### Two Stage Detectors

- FasterRCNN [Tensorflow Object Detection](https://github.com/tensorflow/models/tree/master/research/object_detection) or [TensorPack](https://github.com/tensorpack/tensorpack)
- Any Faster-RCNN refinement, available for instance in [Detectron](https://github.com/facebookresearch/Detectron) (in Pytorch)
- Feel free to explore other methods and papers, be creative!

#### Other types of detection

As the goal is to count plastic waste, you may only want to detect the center of the object, corners or keypoints rather than the bounding box. It is possible to convert the dataset and try one of these approach:
- CenterNet [Paper](https://arxiv.org/abs/1904.07850)  [Github](https://github.com/xingyizhou/CenterNet)
- CornerNet [Paper](https://arxiv.org/abs/1808.01244) [Github](https://github.com/princeton-vl/CornerNet)

#### Tracking

As we will process the videos to get a few frames every second, the output of the detector on each frame will often detect the same plastic object. Using tracking it is possible to follow multiple objects and be able to count them.

- Kalman Filters, Particle Filters
- DeepSort: [Blog review](https://nanonets.com/blog/object-tracking-deepsort/) [Github](https://github.com/nwojke/deep_sort)

-
