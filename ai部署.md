.ONNX、YOLOv5	原始模型

RKNN	用于在芯片NPU上运行AI模型的一套工具和模型格式

RKNN-Toolkit2	转模型的工具

RKNN Runtime(librknnrt.so)	位于开发板上，程序通过它加载模型、调用NPU推理、获取结果

训练是让模型从数据中学到规律；推理是拿训练号=好的模型识别新输入。

```c
电脑上的 ONNX 模型
       ↓ Toolkit2 转换，指定 rk3568
     RKNN 模型
       ↓ 复制到开发板
Python Lite2 或 C++ Runtime
       ↓ 调用内核 RKNPU 驱动
     RK3568 NPU 运算
       ↓
类别、分数、目标框
```

```
解压sdk并锁定依赖
-rknn-toolkit2
-rknpu
rknn_yolov5_demo.zip
```

安装Anaconda和Python3.8

```
~/anaconda3/bin/conda create -y -n py3.8 python=3.8 --override-channels -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main > ~/tools/conda-py38.log 2>&1 //创建py3.8
conda activate py3.8
```

更新npu连板推理运行库

```
rknpu2-master
adb push librknn_api
adb push rknn_server
```

安装rknn-toolkit2

```
rknn-toolkits2
根据requirements_cp38-1.5.0.tex安装依赖库
pip install rknn_toolkit2-1 .5.0+1fa95b5c-cp38-cp38-linux_x86_64.whl
```

安装RKNN -Toolkit Lite2

```
adb push rknn_toolkit_lite2-1.5.0-cp38-cp38-linux_aarch64.whl
pip install rknn_toolkit_lite2-1 .5.0-cp38-cp38-linux_aarch64 .whl
```

