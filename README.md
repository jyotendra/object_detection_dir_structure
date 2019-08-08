Suggested directory structure:
```
datasetName
|-- JPEGImages
     |-- 1.jpg
     |-- 2.jpg
|-- Annotations
     |-- 1.xml
     |-- 2.xml
|-- ImageSets
     |-- Main
          |-- train.txt
          |-- val.txt

```


train.txt and val.txt files, each line is the name indicated for training or validation files. To create these files use these commands:

```
# From the tensorflow/JPEGImages directory 
ls images | grep ".jpg" | sed s/.jpg// > annotations/train.txt 
```


Here's a short description on which folder must contain what:

1. Annotations - contains all .xml annotation files.
2. ImagesSets/Main - contains files like train.txt, val.txt etc which describes which files need to be used for what step.
3. JPEGImages - contains all the images that were annotated.


Here's description of all the op level files:

1. model_config_file.config: This is model config file specific to the model being used. For this example, we are demonstrating rfcn_resnet101_coco model whose configuration file is obtained from [here](https://raw.githubusercontent.com/tensorflow/models/master/research/object_detection/samples/configs/rfcn_resnet101_coco.config). Other config files are present [here](https://github.com/tensorflow/models/tree/master/research/object_detection/samples/configs).



Train.py and Eval.py are no longer part of updated repo. Need to use `model_main.py` for training model as given [here](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/running_locally.md)

Here's the training command for brevity:

```
# From the tensorflow/models/research/ directory
PIPELINE_CONFIG_PATH={path to pipeline config file}
MODEL_DIR={path to model directory}
NUM_TRAIN_STEPS=50000
SAMPLE_1_OF_N_EVAL_EXAMPLES=1
python object_detection/model_main.py \
    --pipeline_config_path=${PIPELINE_CONFIG_PATH} \
    --model_dir=${MODEL_DIR} \
    --num_train_steps=${NUM_TRAIN_STEPS} \
    --sample_1_of_n_eval_examples=$SAMPLE_1_OF_N_EVAL_EXAMPLES \
    --alsologtostderr
```

