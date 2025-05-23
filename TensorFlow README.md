# Run TensorFlow Faster R-CNN w/ResNet50 Training
In order to run your own training for the Faster R-CNN model, some setup is required. This guide is created as a step-by-step instruction on how to run your own training.

## Prerequisites
1. Make sure you have downloaded the dataset and extract the content into a folder name ```dataset``` and place it in the root directory of the repository.
2. Download the base model (Faster R-CNN ResNet50 V1 640x640) for the training from [TensorFlow 2 Detection Model Zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2_detection_zoo.md), or download from [this link](http://download.tensorflow.org/models/object_detection/tf2/20200711/faster_rcnn_resnet50_v1_640x640_coco17_tpu-8.tar.gz). Extract the file and put it into the root directory of the repository.

## Setup
1. Install TensorFlow Object Detection API with TensorFlow 2, follow the guide to install at [TensorFlow Model Garden](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2.md). You are only required to follow the installation instruction.
2. Perform data transformation on the dataset by running [tf_data_load_and_transform.ipynb](tf_data_load_and_transform.ipynb). If successful, your train, validation, and test dataset folders will have ```dataset.record``` file and ```labels.csv``` file in each folder.
3. Create two folders in the root directory of the repository named ```saved_model_checkpoint``` and ```saved_model_build``` for training and model building purpose.

## Run Training and Model Building
1. In your terminal, change your current directory to this repository.
2. Run training, change ```<TensorFlow Model Garden Path>``` into the path to your [TensorFlow Model Garden](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2.md) repository.
```bash
python <TensorFlow Model Garden Path>\models\research\object_detection\model_main_tf2.py --pipeline_config_path=.\pipeline.config --model_dir=.\saved_model_checkpoint --alsologtostderr
```
3. Build the model
```bash
python <TensorFlow Model Garden Path>\models\research\object_detection\exporter_main_v2.py --input_type=image_tensor -- pipeline_config_path=.\pipeline.config --trained_checkpoint_dir=.\saved_model_checkpoint --output_directory=.\saved_model_build
```
Your ```saved_model_build``` folders should now have the built model

## Model Inference
You can run model inference by running Jupyter Notebook [tf_model_inference](tf_model_inference.ipynb)