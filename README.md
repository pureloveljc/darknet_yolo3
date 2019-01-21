# darknet_yolo3
第一 coco数据集编译</br>
git clone https://github.com/pdollar/coco.git</br>
cd coco/PythonAPI</br>
vi Makefile </br>
# 将python改为python3</br>
make</br>

第二数据集下载</br>
git clone https://github.com/pjreddie/darknet.git</br>
cd darknet</br>
cp scripts/get_coco_dataset.sh data</br>
cd data</br>
bash get_coco_dataset.sh</br>

Darknet安装配置</br>
git clone https://github.com/pjreddie/darkent.git</br>
配置 yolov3.cfg 并下载yolov3.weights(别人已经熟练好的模型)</br>
