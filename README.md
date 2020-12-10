## Super-Resolution Label-free Vibrational Imaging of Cells and Tissues

### Calculation of Pearson's correlation correlation
The Pearson correlation coefficient is calculated as:

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


