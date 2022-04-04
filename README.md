# Super-Resolution Label-free Volumetric Vibrational Imaging
## Calculation of Pearson's correlation correlation
The Pearson correlation coefficient is calculated by `Pearson_correlation_coefficient.ipynb`
as:

<img src="https://render.githubusercontent.com/render/math?math=r=\frac{\sum(x-\bar{x})(y-\bar{y})}{\sqrt{\sum(x-\bar{x})^2\sum(y-\bar{y})^2}}">
between the pixel intensities of the model’s output, y, and independent ground-truth test images, x.

### Data
The input for calculating the Pearson's correlation coefficient is the prediction output of `pytorch_fnet`
(https://github.com/AllenCellModeling/pytorch_fnet/blob/release_1/README.md). Data path of the data should be in the directory `./data` with folder name `"label"_train`. For example, `./data/dapi_model_train`.

### Computing environment 

```shell
CPython 3.8.5
IPython 7.18.1

numpy 1.19.1
scipy 1.5.0
pandas 1.1.2
tqdm 4.50.0
bokeh 2.2.1
jupyterlab 2.2.6
```



## U-net model training and prediction
The method is based on the `release_1` of https://github.com/AllenCellModeling/pytorch_fnet

### System Requirements
Installing on Linux is recommended (we have used Ubuntu 16.04).

An nVIDIA graphics card with >10GB of ram (the authors have used an nVIDIA Titan X Pascal) with current drivers installed (we have used nVIDIA driver version 390.48).

### Installation
#### Environment setup
- Install [Miniconda](https://conda.io/miniconda.html) if necessary.
- Create a Conda environment for the platform:
```shell
conda env create -f environment.yml
```
- Activate the environment:
```shell
conda activate fnet
```
- Try executing the test script:
```shell
./scripts/test_run.sh
```
The installation was successful if the script executes without errors.

### Train a model with your data

Pair the directories of corresponding SRS images with ground truth images in a csv file. 

Place the directories of SRS images under path_signal and ground truth images under path_target columns.

Place the csv file in the folder data/csvs.

Modify the configuration in scripts/train_model_2d.sh for optimized parameters, shuch as patch size.

Activate the environment:
```shell
conda activate fnet

```shell
Command line: ./scripts/train_model_2d.sh <file name of the csv file> 0

```

You should see entries reporting the losses. Similar to this:

```shell
49991,0.25850439071655273
49992,0.2647261321544647
49993,0.283742755651474
49994,0.311653733253479
49995,0.30210474133491516
49996,0.2369609922170639
49997,0.2907244861125946
49998,0.23749516904354095
49999,0.3207407295703888
50000,0.3556152284145355
```

### Run predictions with the trained model
```
./scripts/predict.sh <file name of the csv file> 0
```
Predicted outputs will be in directories `results/dna/test` and `results/dna/train` corresponding to predictions on the training set and on the test set respectively. Each output directory will have files similar to this:
```shell
$ ls results/3d/dna/test
00  01  02  03  04  05  06  07  08  09  10  11  12  13  14  15  16  17  18  19  predict_options.json  predictions.csv
```
Each number above is a directory corresponding to a single dataset item (an image pair) and should have contents similar to:
```shell
$ ls results/3d/dna/test/00
prediction_dna.tiff  signal.tiff  target.tiff
```
`signal.tiff`, `target.tiff`, and `prediction_dna.tiff` correspond to the input image (SRS), the target image (real fluorescence image), and the model's output (predicted, "fake" fluorescence image) respectively.


### Citation
If you find this code useful in your research, please consider citing our pre-publication manuscript:
```
@article{Ounkomol2018,
  author = {Chawin Ounkomol and Sharmishtaa Seshamani and Mary M. Maleckar and Forrest Collman and Gregory R. Johnson},
  title = {Label-free prediction of three-dimensional fluorescence images from transmitted-light microscopy},
  journal = {Nature Methods}
  doi = {10.1038/s41592-018-0111-2},
  url = {https://doi.org/10.1038/s41592-018-0111-2},
  year  = {2018},
  month = {sep},
  publisher = {Springer Nature America,  Inc},
  volume = {15},
  number = {11},
  pages = {917--920},
}
```


### Allen Institute Software License
This software license is the 2-clause BSD license plus clause a third clause that prohibits redistribution and use for commercial purposes without further permission.   
Copyright © 2018. Allen Institute.  All rights reserved.

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:
1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.  
2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.  
3. Redistributions and use for commercial purposes are not permitted without the Allen Institute’s written permission. For purposes of this license, commercial purposes are the incorporation of the Allen Institute's software into anything for which you will charge fees or other compensation or use of the software to perform a commercial service for a third party. Contact terms@alleninstitute.org for commercial licensing opportunities.  

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
