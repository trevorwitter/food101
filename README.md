# PyTorch Image Classification with Food 101 dataset

Implementation of **Image Classification** models on [Food 101 Dataset](https://data.vision.ee.ethz.ch/cvl/datasets_extra/food-101/) in **PyTorch**

#### Table of Contents
- [Dataset](##Dataset)
- [Model Architechture](##Model-Architechture)
- [Results](##Results)
- [Quickstart](##Quickstart)
    - [Training](###Training)



## Dataset

![Food-101 Data Set](images/food-101.jpg)


The **Food-101 data set** consists of 101 food categories, with 101,000 images in total. Each category includes 750 training images and 250 test images. 

## Model Architecture

The model used is a [ResNet Convolutional Neural Network](https://arxiv.org/abs/1512.03385). For this task, a [PyTorch implementation of ResNet50 model](https://pytorch.org/vision/stable/models/resnet.html), pretrained on [ImageNet](https://image-net.org), was used, replacing the final fully-connected layer with a new 101 unit fully-connected layer. 

![ResNet50 Architecture](images/resnet50.jpg)

**Skip Connections** add the original input to the output of the convolutional block
![Skip Connection](images/skip_connection.jpg)

The final 1000-unit fully connected layer of the pretrained ResNet model is replaced with a 101-unit fully connected layer.

## Results
On the 25,250 image test set, the overall accuracy is **77%**. Accuracy varies by class and is shown below:

![Test Accuracy](images/test_acc_by_class.png)


## Quickstart

With [conda](https://docs.conda.io/en/main/miniconda.html) installed, create and activate environment with the following bash commands:
```bash
>>> conda env create -f environment.yml
>>> conda activate py310_torch
```

### Training

```bash
python train.py --model Resnet --workers 8 --gpu True --epochs 1 --warm_start True
```
Optional parameters: 
- `--model`
    - Specifies model to train: 
        - `ConvNet`: Vanilla CNN 
        - `Resnet`: Resnet 50, pretrained on Imagenet
        - Can specify any new model by adding to `model.py`
- `--workers`: specifies number of workers for dataloaders
- `--gpu`: 
    - `True`: Runs on CUDA or MPS
    - `False`: Runs on CPU
- `--epochs`: Number of training cycles through full dataset
- `--warm_start`:
    - `True`: Loads pretrained model if prior training was run
    - `False`: Trains new model
