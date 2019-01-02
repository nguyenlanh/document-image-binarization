## Binarize

The `binarize.py` script performs the binarization of an input image using a trained model. The parameters of this script are the following:


| Parameter    | Default | Description                      |
| ------------ | ------- | -------------------------------- |
| `-int`   |         | path to the image to process     |
| `-out` |         | path to save the output image        | 

For example, to binarize the image `img01.png` using the model trained, you have to run the following command:


```
$ python binarize.py -in img01.png -out img01_binarization.png
```

The `MODELS` folder includes the trained models for the datasets evaluated.



## Train

The `train.py` script performs the training of the proposed network from a dataset of images and a series of input parameters that allow to configure both the training process and the network topology. 
The parameters of this script are the following:


| Parameter    | Default | Description                      |
| ------------ | ------- | -------------------------------- |
| `-path`      |         | Base path to datasets            | 
| `--aug`      |         | Load augmentation folders        |
| `-w`         |  256    | Input window size                |
| `-s`         |  -1     | Step size. -1 to use window size |
| `-f`         |  64     | Number of filters                |
| `-k`         |  5      | Kernel size                      |
| `-drop`      |  0      | Dropout percentage               |
| `-stride`    |  2      | Convolution stride size          |
| `-every`     |  1      | Residual connections every x layers |
| `-th`        |  0.5    | Selectional threshold. -1 to evaluate from 0 to 1  |
| `-page`      |  -1     | Page size to divide the training set. -1 to load all |
| `-start_from`|  0      | Start from this page             |
| `-super`     |  1      | Number of super epochs           |
| `-e`         |  200    | Number of epochs                 |
| `-b`         |  10     | Mini-batch size                  |
| `-esmode`    |  p      | Early stopping mode: g='global', p='per page' |
| `-espat`     |  10     | Early stopping patience          |
| `-verbose`   |  1      | 1=show batch increment, other=mute | 


The folders of each dataset must have a specific name (see table in section "Datasets" or consult the source code). Within each folder there must be two subfolders, one with the suffix `\_GR` with the images in gray scale, and another with the suffix `\_GT` for the ground truth.

Option `--aug` activates the data augmentation, in this case the system will load the images stored in the folder with prefix `aug_`.

For example, to train a network for the dataset, you have to run the following command:


```
$ python -u train.py -dbp 6 --aug -w 256 -s 128 -f 64 -k 5 -e 200 -b 10 -th -1 -stride 2 -page 64
```


Once the script finishes, it will save the learned weights and the binarized images resulting from the validation partition in a folder with the prefix `_PR-` followed by the name of the model. It will also show the mean squared reconstruction error and the obtained F-m.
