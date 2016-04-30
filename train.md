## Training models flow

### Prepare data

- Checkout branch feature/train in orec-deepcore repository

- Compile caffe

```
cd caffe-fast-rcnn
mkdir build
cd build
cmake ..
make -j8 && make pycaffe
```

- Edit .bashrc

```
export PY_FASTER_RCNN_PATH=path_to_orec_deepcore
```

- Compile faster-rcnn lib

```
cd orec-deepcore/lib
make
```

- Data directory: 

```
/data/rcnn_train
```

- Structure of training data

```
├── bottle_can_glass
│   ├── annotations
│   └── images
├── sample71
│   ├── annotations
│   └── images
├── sample72
│   ├── annotations
│   └── images
└── sample82
    ├── annotations
    └── images
```


- annotations: xml files create by LabelMeAnnotation tool
- Negative data with empty annotations directory

- Create datasets

```
python tools/create_dataset_mit_csail.py
```

- Training data

```
./scripts/train_faster_rcnn.sh
```

- Ouput models:

```
/home/ubuntu/orec-deepcore/output/faster_rcnn_end2end/MIT-CSAIL
```

### Config caffe neural network architecture

- Change ***settings/class_map.yml*** to map class name with class number

```
names: ["__background__", "can", "glass", "bottle", "fake_bg"]
thresholds: [-.Inf, 0.1, 0.1, 0.1, .inf]
map:
  can: 1
  glass: 2
  beermug: 2
  wineglass: 2
  bottle: 3
  winebottle: 3
```

- Edit caffe architecture (Example: models/VGG16/4class_with_fake_bg)

- Find some line in ***test.prototxt*** and ***train.prototxt*** contain ```# MODIFIED``` and change it to number of classes.

- You can edit ```scripts/train_faster_rcnn.sh``` to fit your system


- When you get model files, change demo.py to this model

```
runner = OrecDetector("models/pascal_voc/VGG16/faster_rcnn_alt_opt/faster_rcnn_test.pt","data/faster_rcnn_models/VGG16_faster_rcnn_final.caffemodel", 0, True)
```

and tools/detect.py to you class names

```
CLASSES = ('__background__',
           'aeroplane', 'bicycle', 'bird', 'boat',
           'bottle', 'bus', 'car', 'cat', 'chair',
           'cow', 'diningtable', 'dog', 'horse',
           'motorbike', 'person', 'pottedplant',
           'sheep', 'sofa', 'train', 'tvmonitor')
```


