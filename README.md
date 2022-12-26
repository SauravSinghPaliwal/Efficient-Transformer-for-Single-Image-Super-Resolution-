# Efficient-Transformer-for-Single-Image-Super-Resolution
# Efficient-Transformer-for-Single-Image-Super-Resolution
## Firstly download and extract the DIV2K X2 dataset
```
wget http://data.vision.ee.ethz.ch/cvl/DIV2K/DIV2K_train_LR_bicubic_X2.zip
wget http://data.vision.ee.ethz.ch/cvl/DIV2K/DIV2K_valid_LR_bicubic_X2.zip
wget http://data.vision.ee.ethz.ch/cvl/DIV2K/DIV2K_train_HR.zip
wget http://data.vision.ee.ethz.ch/cvl/DIV2K/DIV2K_valid_HR.zip
```

```
mkdir div2k
unzip -q DIV2K_valid_LR_bicubic_X2.zip -d div2k
unzip -q DIV2K_train_LR_bicubic_X2.zip -d div2k
unzip -q DIV2K_train_HR.zip -d div2k
unzip -q DIV2K_valid_HR.zip -d div2k
```

## Download the repo 
```
git clone
```
```
wget
```
## Changes to be made
##### I have already made the changes but for information I am just putting all the changes.
## ****Remember to changs the directory to your dataset
### After pulling the repo go to the train.py file and make the below given changes 
```
- Line no = 14 = Uncomment the line [ os.environ["CUDA_VISIBLE_DEVICES"] = '0’ ].
- Line no = 20 = change the batch size to 1 [ parser.add_argument("--testBatchSize", type=int, default=1,
                    help="testing batch size") ]
- Line no = 38 = Change the directory to your root dataset directory.
- Line no = 78 = Add your valid dataset directory.
- Line no = 147 = Uncomment the line [ scale = scale ]
- Line no = 215 = Comment out the line [ print("===> Valid. psnr: {:.4f}, ssim: {:.4f}".format(avg_psnr / len(testing_data_loader), avg_ssim /
len(testing_data_loader))) ]
```
### Than go to the DIV2K.py file  
```
Line no = 43 = Add your decoded dataset directory path.
```
### Lastly open utils.py and change the import to 
```
from skimage.measure import compare_psnr as psnr
from skimage.measure import compare_ssim as ssim
```
## to
```
from skimage.metrics import peak_signal_noise_ratio as psnr
from skimage.metrics import structural_similarity as ssim
```
## Prepare the Dataset
### convert png files in DIV2K to npy files
```
python3 scripts/png2npy.py --pathFrom /path/to/DIV2K/ --pathTo /path/to/DIV2K_decoded/
```
## Training
```
python3 train.py --scale 2 --patch_size 96
python3 train.py --scale 2 --patch_size 144
python3 train.py --scale 2 --patch_size 192
```


