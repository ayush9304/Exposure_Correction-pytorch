# Exposure_Correction-pytorch
English | [简体中文](README-CN.md)

This project is the unofficial pytorch reproduction code of the CVPR2021 paper on the field of image illumination correction [Learning Multi-Scale Photo Exposure Correction.](https://arxiv.org/pdf/2003.11596.pdf);
    
I read this very interesting paper [Learning Multi-Scale Photo Exposure Correction.](https://arxiv.org/pdf/2003.11596.pdf) a few days ago. I wanted to modify it based on its source code, but the paper The official code of MATLAB is implemented by MATLAB. For a pytorch user, it is inevitable that it is a bit awkward. Therefore, I spent some time using the pytorch framework to reproduce this paper. When the [Bilateral Guided Upsampling (bgu)](Image_upsample_tools/run_bgu.m) upsampling method used in the original MATLAB code is not used, but the simple upsampling method is used to process the prediction results, the recurrence result is psnr: 19.756, ssim: 0.749; if adopted, the recurrence result is psnr: 20.313, SSIM: 0.863; ( Original paper in the same way: psnr: 20.205, ssim: 0.769)
    

## Folder structure
The project folder for this section should be placed in the following structure:
```
Exposure_Correction-pytorch
├── MultiExposure_dataset
│   ├── testing
│   ├── training
│   └── validation
├── log
├── run-out
├── tools
├── snapshots
│   ├── MSPECnet_woadv.pth # pretrained model
```
## Requirements

1. Python  3.8.0
2. Pytorch 1.9.1
3. numpy   1.21.0

If your cuda version is 11.1, you can also configure the environment directly by:
```
conda create -n mspec_env python==3.8
conda activate mspec_env
pip install -r requirements.txt
```
## prepare data
1. First download [Training](https://edef4.pcloud.com/cBZsMTq3hZN7kc8TZZZnC3VykZ2ZZn0JZkZMRnXCkZ4kZk0ZrZ9VZR5ZaXZg7ZiVZF5Z2kZI7ZjVZn0ZmXZxYmBZpcTsy4MBRjbYa2aOkB4ohVlGpQFk/training.zip)|[ Validation](https://edef2.pcloud.com/cBZAYvx3hZxjuI8TZZZxtaVykZ2ZZn0JZkZuHahJZK0ZaZD7ZBkZTVZcXZIXZIkZE7ZuXZmkZGXZV5ZEVZLHmBZAAyRGB0KJBRvL0y7FmCG7X7bGz37/validation.zip)|[Testing](https://ln2.sync.com/dl/098a6c5e0/cienw23w-usca2rgh-u5fxiex-q7vydzkp)from the [official github repository](https://github.com/mahmoudnafifi/Exposure_Correction)
2. Place the dataset in the root directory of the project according to the folder result
3. Run the following code to preprocess the data, and then a new Patchs folder will be generated in the ./MultiExposure_dataset/training directory
```
python ./tools/creat_patch.py
```
## train
1. Run the following command for training without adversarial loss:
```
python mspec_train.py
```

2. If you want to add an adversarial loss to training, run:
```
python mspec_train.py --use_advloss
```

## test
1. You can directly download the checkpoint that I trained without adversarial loss: [baidu clound password: 1234](https://pan.baidu.com/s/1GlXrhQfdasCPStcPp5ahyQ) or unzip snapshots.zip
2. You can also train the model yourself
3. Then run the following command for test verification:
```
python mspec_test.py
```

## bgu
In the testing phase, if you need to use bgu upsampling to replace the default interpolation resize in mspec_test, you need to run the [run_bgu.m](Image_upsample_tools/run_bgu.m) code for subsequent upsampling.

## Contact information
E-mail: 2443976970@qq.com
