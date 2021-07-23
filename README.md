# Deepstream example installation guide

## Computer details
- Ubuntu 20.04.2 LTS, 64-bit
- GNOME Version 3.36.8
- Windowing System X11
- NVidia RTX 3090
- Intel® Core™ i9-10900KF CPU @ 3.70GHz × 20
```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 460.32.03    Driver Version: 460.32.03    CUDA Version: 11.2     |
|-------------------------------+----------------------+----------------------+
```

## Set LD_LIBRARY_PATH
Desired
```bash
$ echo $LD_LIBRARY_PATH #/usr/local/lib::/home/samuel/Downloads/TensorRT-7.2.3.4/lib:/usr/local/cuda/lib64
```

```bash
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:~/Downloads/TensorRT-7.2.3.4/lib
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64
```

## Build
```bash
$ cd /opt/nvidia/deepstream/deepstream-5.1/sources/apps/sample_apps/deepstream-test1
$ sudo CUDA_VER=11.2 make
```

## Run
```bash
$ cd /opt/nvidia/deepstream/deepstream-5.1/sources/apps/sample_apps/deepstream-test1
$ deepstream-test1-app /opt/nvidia/deepstream/deepstream/samples/streams/sample_720p.h264
```

## All steps
1. cd ~/Downloads
2. tar xzvf TensorRT-7.2.3.4.Ubuntu-18.04.x86_64-gnu.cuda-11.1.cudnn8.1.tar.gz
3. cd TensorRT
4. export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:~/Downloads/TensorRT-7.2.3.4/lib
5. cd python && sudo pip3 install tensorrt-7.2.3.4-cp38-none-linux_x86_64.whl # follow installation guide for others
6. tar -xzvf cudnn-11.4-linux-x64-v8.2.2.26.tgz
7. sudo cp cuda/include/cudnn*.h /usr/local/cuda/include
8. sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda/lib64
9. sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*
10. nvidia-smi
11. dpkg-deb -x cuda-nvrtc-11-1_11.1.105-1_amd64.deb ./nvrtc
12. cd nvrtc/usr/local/cuda-11.1/lib64
13. sudo mkdir /usr/local/cuda/lib64Backup
14. sudo cp -r /usr/local/cuda/lib64/* /usr/local/cuda/lib64Backup
15. sudo cp ~/Downloads/nvrtc/usr/local/cuda-11.1/lib64/* /usr/local/cuda/lib64/
16. export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64
17. sudo tar -xvf deepstream_sdk_v5.1.0_x86_64.tbz2 -C /
18. cd /opt/nvidia/deepstream/deepstream-5.1/
19. sudo ./install.sh
20. cd /opt/nvidia/deepstream/deepstream-5.1/sources/apps/sample_apps/deepstream-test1
21. sudo apt-get install libgstreamer1.0-dev
22. sudo apt-get install libgstreamer-plugins-base1.0-dev
23. sudo CUDA_VER=11.2 make
24. deepstream-test1-app /opt/nvidia/deepstream/deepstream/samples/streams/sample_720p.h264
25. Wait a bit and then it starts playing the video and classifying the video!


### Probably not needed
1. git clone https://github.com/edenhill/librdkafka.git
2. git reset --hard 7101c2310341ab3f4675fc565f64f0967e135a6a
3. ./configure
4. make
5. sudo mkdir -p /opt/nvidia/deepstream/deepstream-5.1/lib
6. sudo cp /usr/local/lib/librdkafka* /opt/nvidia/deepstream/deepstream-5.1/lib
7. export GST_LIBS="-lgstreamer-1.0 -lgobject-2.0 -lglib-2.0"
8. export GST_CFLAGS="-pthread -I/usr/include/gstreamer-1.0 -I/usr/include/glib-2.0 -I/usr/lib/x86_64-linux-gnu/glib-2.0/include"
9. git clone https://github.com/GStreamer/gst-python.git
10. git checkout 1a8f48a
11. sudo apt install autoconf
12. sudo apt install automake
13. ./autogen.sh PYTHON=python3
14. sudo apt-get install python3-gi


