# ultralytics-YOLO-DeepSort/ByteTrack-PyQt-GUI
a GUI application, which uses ultralytics YOLO for  Object Detection/Tracking, Human Pose Estimation/Tracking from images, videos or camera. 

All python scripts performing detection, pose and segmentation using the YOLO model in ONNX.

![GUI](./data/ui.png)

Supported AI tasks:
- [x] Detection
- [x] Pose Estimation
- [x] Segmentation
- [ ] OBB

Supported Models:
- [x] YOLOv13
   - [x] YOLOv13-n
   - [x] YOLOv13-s
   - [x] YOLOv13-l
   - [x] YOLOv13-x
- [x] YOLO11
   - [x] YOLO11-n
   - [x] YOLO11-s
   - [x] YOLO11-m
   - [x] YOLO11-l
   - [x] YOLO11-x
- [x] YOLOv8
   - [x] YOLOv8-n
   - [x] YOLOv8-s
   - [x] YOLOv8-m
   - [x] YOLOv8-l
   - [x] YOLOv8-x

Supported Trackers:
- [x] DeepSort
- [x] ByteTrack

Supported Input Sources:
- [x] local files: images or videos
- [x] Camera
- [x] RTSP-Stream

## Install

Install required packages with pip:

```shell
pip install -r requirements.txt
```

or with conda:

```shell
conda env create -f environment.yml

# activate the conda environment
conda activate yolo_gui
```

## Download weights

Download the model weights：

``````shell
python download_weights.py
``````

The model files are saved in the **weights/** folder.

## Run

```shell
python main.py
```

## Troubleshooting

### WSL 环境下的 Qt 平台插件错误

如果在 WSL 中运行时遇到 `Could not load the Qt platform plugin "xcb"` 错误，请按以下步骤解决：

#### 方法 1：安装系统依赖（推荐）

```bash
sudo apt-get update
sudo apt-get install -y libxcb-xinerama0 libxcb-cursor0 libxcb-xfixes0 libxcb-xkb1 libxkbcommon-x11-0 libxkbcommon0 libxcb-render-util0 libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-randr0 libxcb-render0 libxcb-shape0 libxcb-sync1 libxcb1
```

或者安装完整的 Qt5 依赖：

```bash
sudo apt-get install -y qt5-default libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev-tools
```

#### 方法 2：配置 X11 转发（如果需要在 Windows 上显示 GUI）

1. 在 Windows 上安装 X 服务器（推荐使用 [VcXsrv](https://sourceforge.net/projects/vcxsrv/) 或 [X410](https://www.microsoft.com/store/productId/9NLP712ZMN9Q)）
2. 启动 X 服务器
3. 在 WSL 中设置 DISPLAY 环境变量：

```bash
export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):0.0
```

或者添加到 `~/.bashrc` 使其永久生效：

```bash
echo "export DISPLAY=\$(cat /etc/resolv.conf | grep nameserver | awk '{print \$2}'):0.0" >> ~/.bashrc
source ~/.bashrc
```

