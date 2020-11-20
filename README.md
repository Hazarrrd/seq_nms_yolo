# Seq_nms_YOLO

#### Membres: Yunyun SUN, Yutong YAN, Sixiang XU, Heng ZHANG

---

## Introduction

![](img/index.jpg) 

This project combines **YOLOv2**([reference](https://arxiv.org/abs/1506.02640)) and **seq-nms**([reference](https://arxiv.org/abs/1602.08465)) to realise **real time video detection**.

## Steps

In order to perform real time video detection, perform folowing steps using terminal [Prepered for Ubuntu, python 3.7]:

## Create the environment

Create virtual envirement, where code will be executed/
1. Create envirement with command > conda create -y --prefix ENVNAME python=3.7
2. For activate envirement type > source activate ENVNAME

## Install important librarys 

3. conda install -y -c conda-forge opencv

4. conda install -y -c anaconda cudatoolkit==10.1.168

5. conda install -y cudnn==7.6.4

6. conda install -y numpy

7. conda install -y -c menpo imageio 

8. conda install -y matplotlib

9. conda install -y -c anaconda scipy

10. conda install -y -c conda-forge tensorflow

11. pip install tensorflow-object-detection-api

## Configurate variables and prepere makefile

First set variable PKG_CONFIG_PATH with commands:

12. PKG_CONFIG_PATH=$PKG_CONFIG_PATH:./env/lib/pkgconfig

13. export PKG_CONFIG_PATH

And afterwards do two changes in makefile:

14. at the beggining of the file, in ARCH = ... add at the end addtional line: gencode arch=compute_75,code=[sm_75,compute_75]

15. change from cuda-8.0 to cuda-10.1 in two lines below:

> COMMON+= -DGPU -I/usr/local/cuda-8.0/include/

> LDFLAGS+= -L/usr/local/cuda-8.0/lib64 -lcuda -lcudart -lcublas -lcurand

16. 'make' the project

## Prepere code and data to usage

17. Download `yolo.weights` and `tiny-yolo.weights` by running `wget https://pjreddie.com/media/files/yolo.weights` and `wget https://pjreddie.com/media/files/tiny-yolo-voc.weights`
18. Rename tiny-yolo-voc.weights to tini-yolo.weights
19. Upload the video.mp4, on which you want use detection algorithm, to folder video
20. In files img2video.py, video2img.py, yolo_segnms.py, yolo_detection.py make all print functions to use parenthesis - print ('xx') instead print 'xx'
21. Change files:
### in yolo_seqnms.py change:
* add to imports import imageio
* replace import cpickle as pickle with import pickle
* in line 288 replace scipy.misc.imsave with imageio.imwrite
* in line 39 replace the if condition box[0]==cls with str(box[0],'utf-8')== cls

## Run the commands

22. In the video folder, run `python video2img.py -i input.mp4` to generate frames and then `python get_pkllist.py`;

23. Move file pkllist.txt to folder video

24. Return to root floder and run `python yolo_seqnms.py` to generate output images in `video/output`

25. If you want to reconstruct a video from these output images, you can go to the video folder and run `python img2video.py -i output`

And you will see detection results in `video/output`

## Reference

This project copies lots of code from [darknet](https://github.com/pjreddie/darknet) , [Seq-NMS](https://github.com/lrghust/Seq-NMS) and  [models](https://github.com/tensorflow/models).
