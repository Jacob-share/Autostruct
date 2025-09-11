# AutoStruct

## 1. (5 skip)G+(Wavelet)D+P Model
(5 skip)G+(Wavelet)D+P is the optimal model. It has the highest performance.

### Training the Model
To train the model, run the `train.py` script. This will initiate the training process and generate model checkpoints. **Pre-trained models will be saved in `/AutoStruct_V1/Model/checkpoints` directory.**

### Generating Test Images
To generate test images, execute the `test.py` script. **The generated shear wall layouts will be saved in `/AutoStruct_V1/Model/results/archi2struct/test_latest/images` directory.**
### Post - processing Step
You can control whether to add a post - processing step by modifying the following line in `pix2pixHD_model_SWIN.py` (line 301):
```python
Post_process = True   # True  / False
```
Set `Post_process` to `True` to enable the post - processing step, or `False` to disable it.

## 2. Switching to Other Model Variants

### Ⅰ.(CNN)D
If you want to switch the discriminator to (CNN)D, follow these steps:

#### Step 1: Modify `models.py`
In `models.py`, replace the following line (line 5):
```python
from .pix2pixHD_model_SWIN import Pix2PixHDModel, InferenceModel
```
with
```python
from .pix2pixHD_model import Pix2PixHDModel, InferenceModel
```

#### Step 2: Modify `network.py`
In `network.py`, replace the following line (line 72):
```python
netD = Discriminator(1024,input_nc)
```
with
```python
netD = MultiscaleDiscriminator(input_nc, ndf, n_layers_D, norm_layer, use_sigmoid, num_D, getIntermFeat)
```

#### Step 3: Training
After making the above changes, you can start the training process.

### Ⅱ.(4skip)G
If you want to switch from (5 skip)G to (4 skip)G, follow these steps:

#### Step 1: Modify `vit_seg_configs.py`
In `vit_seg_configs.py`, on line 54 in `config.decoder_channels`, replace `(512, 256, 128, 64, 32, 16)` with `(512, 256, 64, 64, 16)`.
on line 54 in `config.skip_channels`, replace `[1024, 512, 256, 128, 64, 0]` with `[1024, 512, 256, 64, 0]`.
on line 57 in `config.n_skip`, replace `5` with `4`.

#### Step 2: Modify `vit_seg_modeling_resnet_skip.py`
In `vit_seg_modeling_resnet_skip.py`, comment out lines 147 to 150:
```python
# ('block4', nn.Sequential(OrderedDict(
#     [('unit1', PreActBottleneck(cin=width*16, cout=width*32, cmid=width*16, stride=2))] +
#     [(f'unit{i:d}', PreActBottleneck(cin=width * 32, cout=width * 32, cmid=width * 8)) for i in range(2, block_units[4] + 1)],
# ))),
```

## 3. Datasets
The dataset for the model is located at `AutoStruct_V1/Model/datasets/struct_design`. Please place the corresponding datasets in this directory according to the specified format. Here, `A` represents the label map, and `B` represents the target value. 
## 4. Evaluation
If you want to obtain the evaluation results, follow these steps:

### Step 1: Prepare the dataset
Place the dataset in `/AutoStruct_V1/Evaluation/images_eval`. Name the files according to the following example: `test (1).png` and `test (1)_synthesized_image.jpg`. Here, `test (1).png` is the target image, and `test (1)_synthesized_image.jpg` is the generated image.

### Step 2: Run the evaluation scripts
Run the 6 Python files under the `Evaluation` directory in sequence.

### Step 3: Obtain the evaluation results
The evaluation results will be saved in `/AutoStruct_V1/Evaluation/results` in 3 text files.


## Acknowledgments
This code borrows heavily from [pix2pixHD](https://github.com/NVIDIA/pix2pixHD),[TransUNet](https://github.com/Beckschen/TransUNet),[StyleSwin](https://github.com/microsoft/StyleSwin),[StructGAN_v1](https://github.com/wenjie-liao/StructGAN_v1).