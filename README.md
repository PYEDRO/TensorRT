# TensorRT
## Tutorial of installing TensorRT

### Dependecies
For instal is necessary CUDA  11.0, 11.2, 11.3, 11.4, 11.5, 11.6, 11.7. 
you can check by running
```
nvcc --version
```
If not installed click : https://developer.nvidia.com/cuda-10.0-download-archive

Is necessary also verify if you has
OpenCV, for that execute:

```
dpkg -l | grep opencv
```
If not installed, execute : 
```
sudo add-apt-repository ppa:timsc/opencv-3.3
sudo apt-get update
sudo apt install libopencv-dev
```
### Installing TensorRT

Go to nvidia-https://developer.nvidia.com/nvidia-tensorrt-8x-download. You might need login.

Choose TensorRT 8.6 GA for Ubuntu 22.04 and CUDA 11.0, 11.1, 11.2, 11.3, 11.4, 11.5, 11.6, 11.7 and 11.8 DEB local repo Package

Install with following commands, after apt install tensorrt, it will automatically install cudnn, nvinfer, nvinfer-plugin, etc.

sudo dpkg -i nv-tensorrt-repo-ubuntu1604-cuda10.0-trt7.0.0.11-ga-20191216_1-1_amd64.deb
sudo apt update
sudo apt install tensorrt

For check by if was installed, execute :
```
dpkg-query -W tensorrt
```

## Executing "Hello Wold" of the TensorRT

First execute this code :

```
git clone https://github.com/wang-xinyu/pytorchx
cd pytorchx/lenet
```
Execute : 
```
python lenet5.py
```
For generate arquive with weights of the TensorRT, execute :

```
python inference.py
```
The exit it will be : 

```
lenet out: tensor([[0.0950, 0.0998, 0.1101, 0.0975, 0.0966, 0.1097, 0.0948, 0.1056, 0.0992,
         0.0917]], device='cuda:0', grad_fn=<SoftmaxBackward>) 
```
### Compare using TensorRT

Copy  the arquive lenet5.wts, generete previously.

 After execute :
```
git clone https://github.com/wang-xinyu/tensorrtx
cd tensorrtx/lenet
cp [PATH-OF-pytorchx]/pytorchx/lenet/lenet5.wts .
mkdir build
cd build
cmake ..
make
```

After 
```
./lenet -s
```

Finaly

```
./lenet -d
```
The exit it will be : 

```
lenet out: tensor([[0.0949623, 0.0998472, 0.110072, 0.0975036, 0.0965564, 0.109736, 0.0947979, 0.105618, 0.099228, 0.0916792,]], device='cuda:0', grad_fn=<SoftmaxBackward>) 
```