# VGGSound

Code and results for ICASSP2020 "VGGSound: A Large-scale Audio-Visual Dataset".

The repo contains the dataset file and our best audio classification model. 

## Dataset

To download VGGSound, we provide a [csv file](./VGGSound/vggsound.csv). For each YouTube video, we provide YouTube URLs, time stamps, audio labels and train/test split. Each line in the csv file has columns defined by here.

```
# YouTube ID, start seconds, label,train/test split. 
```

A helpful link for [data download](https://github.com/marl/audiosetdl)!

## Audio classification 

We detail the audio classfication results here. Note, "Pretrain" refers whether the model was pretrained on [YouTube-8M dataset](https://github.com/tensorflow/models/tree/master/research/audioset/vggish). "Dataset (common)" means it is a subset of the dataset. This subset only contains data of common classes ([listed here](./VGGSound/Common.txt)) between AudioSet and VGGSound. "[ASTest](./VGGSound/AStest.csv)" is the intersection of AudioSet and VGGSound testsets.

| 	  | Model    | Aggregation   | Pretrain           | Finetune/Train  | Test          | mAP   | AUC   | d-prime |
|:---:|:--------:|:-------------:| :-------------:    |:--------------: |:-------------:|:-----:|:-----:|:-------:| 
| A   | VGGish   | \             | :heavy_check_mark: |AudioSet (common)| ASTest        | 0.286 | 0.899 | 1.803   |
| B   | VGGish   | \             | :heavy_check_mark: |VGGSound (common)| ASTest        | 0.326 | 0.916 | 1.950   | 
| C   | VGGish   | \             | :x:                |VGGSound (common)| ASTest        | 0.301 | 0.910 | 1.900   |
| D   | ResNet18 | AveragePool   | :x:                |VGGSound (common)| ASTest        | 0.328 | 0.923 | 2.024   |
| E   | ResNet18 | NetVLAD       | :x:                |VGGSound (common)| ASTest        | 0.369 | 0.927 | 2.058   |
| F   | ResNet18 | AveragePool   | :x:                |VGGSound         | ASTest        | 0.379 | 0.934 | 2.134   |
| G   | ResNet18 | NetVLAD       | :x:                |VGGSound         | ASTest        | 0.424 | 0.942 | 2.221   |
| H   | ResNet18 | AveragePool   | :x:                |VGGSound         | VGGSound      | 0.489 | 0.963 | 2.523   |
| I   | ResNet18 | NetVLAD       | :x:                |VGGSound         | VGGSound      | 0.496 | 0.963 | 2.534   |



## Environment

* Python 3.6.8
* Pytorch 1.3.0



## Pretrained model and evaluation 

We provide the pretrained model **H** and **I** here.

To evaluate the model performance,

```
python eval.py --data "./test.csv" --prediction "./resnet18_vlad/"
```



## Citation
```
@InProceedings{Chen20,
  author       = "Honglie Chen and Weidi Xie and Andrea Vedaldi and Andrew Zisserman",
  title        = "VGGSound: A Large-scale Audio-Visual Dataset",
  booktitle    = "International Conference on Acoustics, Speech, and Signal Processing ",
  year         = "2020",
}
```

## License
The VGG-Sound dataset is available to download for commercial/research purposes under a Creative Commons Attribution 4.0 International License. The copyright remains with the original owners of the video. A complete version of the license can be found [here](./LICENCE.txt).
