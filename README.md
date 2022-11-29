# Bittle_Leg_Angle_with_YOLOv5
Joint angles were identified with YOLOv5

## 实验环境和相关预备
|key|value|
|----------|----------|
|系统环境|VMware Workstation Pro virtual machine Ubuntu 18.04|
|CPU|intel core i7 7700HQ|
|Python版本|python3.7.3(anaconda installed python3.7.3 virtual environment)|
|Yolov5模型版本|YOLO v5s|
|摄像头像元尺寸|未知|
|摄像头传感器尺寸|未知|
|摄像头视角角度|未知|
|摄像头输出分辨率|640*480|
|其他|Bittle，Bittle支架，摄像头支架|

** 注意YOLOv5一直在更新，报错了大概率是版本问题。

YOLOv5环境搭建见[YOLOv5](https://github.com/ultralytics/yolov5)
 ```python
git clone https://github.com/ultralytics/yolov5  # clone
cd yolov5
pip install -r requirements.txt  # install
```

```python
git clone https://github.com/weimaotou/Bittle_Leg_Angle_with_YOLOv5.git
```

把leg_detection.yaml放入YOLOv5的data文件夹中.datasets数据集和detectnode.py放入YOLOv5中，然后进入YOLOv5文件路径。

模型下载：见[YOLOv5](https://github.com/ultralytics/yolov5)

修改的文件：detectnode.py和leg_detection.yaml

## 实验示意图
![实验示意图](./%E7%A4%BA%E6%84%8F%E5%9B%BE.png)

## 第一步 数据集的建立
在不同的环境下拍摄相当数量的图片，然后用[labelImg](https://github.com/heartexlabs/labelImg/tree/b33f965b6d14c14f1e46b247f1bf346e03f2e950)对图像进行标注。
标注好的数据集划分为训练集、测试集和验证集（这里没有用测试集），示例见[datasets](./datasets/)文件夹。

## 第二步 开始训练
修改配置文件，见[leg_detection.yaml](./leg_detection.yaml)
``` python
python train.py --img 640 --batch 1 --epochs 20 --data leg_detection.yaml --weights yolov5s.pt
```
## 第三步 Houghcircles参数选择
见[bimgprocess.ipynb](./bimgprocess.ipynb)

## 第四步 测试效果
``` python
python detectnode.py --weights best.pt --source 1.jpg
```

### 结果如下：

![实验结果图](./%E7%BB%93%E6%9E%9C%E5%9B%BE.jpg)

我遇到的问题：
* 安装torch时，killed. 我的解决：```python pip install torch --no-cache-dir ```
* 建议去官网安装[pytorch](https://pytorch.org/)