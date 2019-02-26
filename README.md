# darknet_yolo3
第一 coco数据集编译</br>
git clone https://github.com/pdollar/coco.git</br>
cd coco/PythonAPI</br>
vi Makefile </br>
将python改为python3</br>
make</br>

第二数据集下载</br>
git clone https://github.com/pjreddie/darknet.git</br>
cd darknet</br>
cp scripts/get_coco_dataset.sh data</br>
cd data</br>
bash get_coco_dataset.sh</br>

Darknet安装配置</br>
git clone https://github.com/pjreddie/darkent.git</br>
配置 yolov3.cfg 并下载yolov3.weights(别人已经训练好的模型)</br>
./darknet imtest data/dog.jpg  # 测试

git clone https://github.com/pjreddie/darknet</br>
cd darknet</br>
vim Makefile：</br>
  ... GPU=1
  ... CUDNN=1
  ... OPENCV=1</br>
make</br>


以上信息表示三个不同尺度(82, 94, 106)上预测到的不同大小的框的参数.</br>

82 卷积层为最大的预测尺度, 使用较大的 mask, 但是可以预测出较小的物体;</br>
94 卷积层为中间的预测尺度, 使用中等的 mask;</br>
106卷积层为最小的预测尺度, 使用较小的 mask, 可以预测出较大的物体.</br>
上述输出信息的各个参数含义是(主要观察某一个尺度上的参数), 下面就 Region 82 分析:</br>

Region Avg IOU: 0.326577： 表示在当前 subdivision 内的图片的平均 IOU, 代表预测的矩形框和真实目标的交集与并集之比, 这里是 75.96%, 这个模型此时已经达到了很高的训练精度;</br>
Class: 0.809470: 标注物体分类的正确率, 期望该值趋近于1;</br>
Obj: 0.732717： 越接近 1 越好;</br>
No Obj: 0.002799： 期望该值越来越小, 但不为零;</br>
.5R: 1.000000： 是在 recall/count 中定义的, 是当前模型在所有 subdivision 图片中检测出的正样本与实际的正样本的比值。在本例中, 全部的正样本被正确的检测到。 </br>
count: 4： 所有当前 subdivision 图片（本例中一共 8 张）中包含正样本的图片的数量。 在输出 log 中的其他行中, 可以看到其他 subdivision 也有的只含有 6 或 1 个正样本, 说明在 subdivision 中含有不包含在检测对象 classes 中的图片。</br>

开始训练</br>

sudo ./darknet detector train cfg/voc.data cfg/yolov3-voc.cfg darknet53.conv.74 -gpus 0,1</br>

开始测试</br>
sudo ./darknet detector test cfg/coco.data cfg/yolov3.cfg backup/yolov3.weights data/test.jpg
sudo ./darknet detector test cfg/coco.data cfg/resnet101.cfg backup/resnet101_900.weights test1.jpg
