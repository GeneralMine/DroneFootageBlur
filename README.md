# Drone Footage Blur
This repository blurs human faces and license plates in drone images and videos with high resolution using a state-of-the-art object detection model, [YOLOv8 by Ultralytics](https://github.com/ultralytics/ultralytics), and is fine-tuned using images from the [OpenImagesDatasetV7](https://storage.googleapis.com/openimages/web/index.html).

Its based on this repo:
https://github.com/varungupta31/dashcam_anonymizer

## A Convenient Script Has Been Provided To Setup the Repository 👨🏽‍💻

Activate any Python Environment of Your Preference (`conda` recommended)

Preferably with `Python3.10+` 🐍

```
$ cd DroneFootageBlur
$ chmod +x setup.sh

# Always be careful runnning .sh files, feel free to browse the contents of setup.sh before running
# The setup.sh file downloads relevant libraries and download the custom YOLO model as well (an alternate link if provided below as well)

$ ./setup.sh
```

<h3> Blurring Images in a Directory  📷</h3>

To blur all images in a directory,

Update the `configs/img_blur.yaml` as required, and run the following command

```
python blur_images.py --config configs/img_blur.yaml
```
The resulting blur images will be stored in the directory specified in the YAML.
Note: `annot_txt` folder will contain the YOLO detections in `.txt` format, converted to the `VOC` bounding-box format.


<h3> Blurring Videos in a Directory 📹</h3>

Similar approach as above, now the command would be

```
python blur_videos.py --config configs/vid_blur.yaml
```
Note:
1. If you run into mysterious `libgc` errors, what worked for me was to also install the `opencv` via `Conda`. PIP installation, leaves out some `libgc` libraries, which causes issues in the videowriter codecs.
2. The configuration files are slightly different for videos and images. Make sure to choose and edit the correct ones depending upon the modality.
3. This is designed to process all the contents in a given directory at once. If the blurring is to be re-run, make sure to delete the `runs` directory, as it may lead to new file names within the runs, which will cause errors.
4. <strike>The `blur_videos.py` script currently expects the videos to be named numerically [1.mp4, 111.mp4]</strike> [Updates 2024, not anymore - name file as you wish]

<hr>

## Please Note 📝
* Will this do a 100% perfect job? --> Maybe not.
  - Some specific angles pose a challenge in perfect detections - especially with faces!
* Is there scope for improvement in terms of optimization? --> There always is.
  - _Good_ to question it and call out, even _better_ to help me improve it :)
* This project has aged somewhat, but I still feel it does a pretty decent job compared to what's out there.
  - If you feel the implementation is outdated, you may still benefit from the model I trained :)
  - If you end up improving the YOLO model, please raise an issue and I'll be glad to incorporate it with due credits.
