# AutoStruct_V1
# paper name
Our paper has been published online:
# Dependencies

python                    3.8.8  
cudatoolkit               11.3  
pytorch                   1.12.1+cu113   
tensorflow                2.13.1  
numpy                     1.24.3  
opencv-python             4.10.0.84   
scipy                     1.10.1  

# AutoStruct
![img_1.png](img_1.png)
# Pre-trained models
Please download our pre-training model at ''. Our pre-trained model is a (5 skip)G+(Wavelet)D+P architecture, trained on the MIX dataset.
# Get the layout of shear wall
This is an introduction on how to obtain the layout of shear wall using AutoStruct.

### Step 1: Sketch the building layout
Open `Sketching Tools.html` in your browser and use the Sketching Tools to draw a sketch of the building layout. Click the "Instructions" button of the Sketching Tools to get detailed instructions on how to use the tool. After you've finished the sketch, click "Save Image" and save your sketch in the following path:
`/AutoStruct_V1/Model/datasets/struct_design/test_A`

### Step 2: Prepare the model and environment
Make sure you have downloaded the pre-trained model 'latest_net_G'&'latest_net_D' and placed them in the `/AutoStruct_V1/Model/checkpoints/archi2struct` directory. Also, install the corresponding environment according to the Dependencies.

### Step 3: Generate the shear wall layout
Run `test.py`. You will get the layout of the shear wall in the `/AutoStruct_V1/Model/results/archi2struct/test_latest/images` directory. <br>The model calculation process will take less than two minutes. 

# Training
To train a model at 1024 x 512 resolution
,run the `train.py` script. This will initiate the training process and generate model checkpoints. **Pre-trained models will be saved in `/AutoStruct_V1/Model/checkpoints` directory.**
Training the (5 skip)G+(Wavelet)D+P Model requires more than 35 gigabytes of video memory. 
<br>For more details on the training methods,please see the "RunGuidance.md" under the "AutoStruct_V1/Model/RunGuidance.md"
# Testing
To generate test images, execute the `test.py` script. **The generated shear wall layouts will be saved in `/AutoStruct_V1/Model/results/archi2struct/test_latest/images` directory.**


# Datasets
Our dataset is come from [StructGAN_v1](https://github.com/wenjie-liao/StructGAN_v1).The total dataset is located at `/AutoStruct_V1/Datasets`.We provide `data_add.py`, which you can use to perform data augmentation operations on the dataset.
<br>The dataset for the model is located at `AutoStruct_V1/Model/datasets/struct_design`. Please place the corresponding datasets in this directory according to the specified format. Here, `A` represents the label map, and `B` represents the target value. 
<br>If you want to train with your own dataset,please put your dataset in `AutoStruct_V1/Model/datasets/struct_design`,and make sure the picture size is at 2048 x 1024 resolution.

# Evaluation
The Evaluation is cite from [StructGAN_v1](https://github.com/wenjie-liao/StructGAN_v1).If you want to obtain the evaluation results, follow these steps:

### Step 1: Prepare the dataset
Place the dataset in `/AutoStruct_V1/Evaluation/images_eval`. Name the files according to the following example: `test (1).png` and `test (1)_synthesized_image.jpg`. Here, `test (1).png` is the target image, and `test (1)_synthesized_image.jpg` is the generated image.

### Step 2: Run the evaluation scripts
Run the 6 Python files under the `Evaluation` directory in sequence.

### Step 3: Obtain the evaluation results
The evaluation results will be saved in `/AutoStruct_V1/Evaluation/results` in 3 text files.


# Citation
If you have any problems, please do not hesitate to contact us! You are very welcome to cite our paper!
The BibTeX entries of related papers are as follows

# Acknowledgments
This code borrows heavily from [pix2pixHD](https://github.com/NVIDIA/pix2pixHD),[TransUNet](https://github.com/Beckschen/TransUNet),[StyleSwin](https://github.com/microsoft/StyleSwin),[StructGAN_v1](https://github.com/wenjie-liao/StructGAN_v1).
