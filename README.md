
# Accelerated Image Restoration using CUDA

This software application is a performant image restoration filter to leverages parallelization capabilities in C++ and CUDA to do the operation of deblurring images faster than the out-of-the-box OpenCV deblur filter. This is achieved by replacing most of the inbuilt library functions with optimized loop constructs and leveraging enhanced native language capabilities. The performance analysis indicates that the computation time for image restoration is reduced by 62.13% compared to using the OpenCV standard restoration filter. This gain in performance is verified by checking for similarity of correctness in the Peak Signal to Noise Ratio(PSNR) and Mean Squared Error(MSE) computed between the original and restored image for each of the implementations. The complete report with performance analysis and results is showcased [here]().


## Hardware Specification

#### CPU Specification



| CPU | Intel(R) Core(TM) i9-9900K     |
| :-------- | :------- |
| Memory | 128 GB |
|Cores | 8 (16 Threads) |
|Clock Speed | Base = 3.60 GHz, Max = 5.00 GHz|
|Instruction Per Clock Cycle | FP32 = 32, FP64 = 16 |
|Caches | 16 MB Intel® Smart Cache(L1 - 256 KB (code)/256 KB(data), L2 - 2048 KB, L3 - 16384 KB)

#### GPU Specification

|GPU | NVIDIA GeForce RTX 3070|
| :-------- | :------- |
|Architecture and Compute Capability|Ampere, 8.6|
|Cores (GPU) | 5888|
|Clock Speed (GPU) | 1500 MHz|
|Memory (GPU) |8GB |
|Bandwidth | 448.0 GB/s|
|Theoretical Performance(Single Precision) | 20.31 TFLOPS|
| Theoretical Performance(Double Precision) |  317.4 GFLOPS|


## Tools

- Visual Studio Code - Version: 1.69.0 
- CUDA - version: V11.2
- OpenCV 3.2 with CUDA Support
- Nsight Profiler

## Instructions to Compile and Execute

- Add the path of a high-quality input(.png) images to the imread method in each of the .cu and .cpp implementations
- The program findbestparams.cpp helps find the optimal values of R and SNR for the point spread function that is used to enhance the quality of image restoration.

- Use the following command to run findbestparams.cpp

```c++
g++ findbestparams.cpp -o program -I/usr/local/include/opencv4 -lopencv_core -lopencv_highgui -lopencv_imgcodecs -lopencv_imgproc $(pkg-config opencv4 --libs)
```

- Use the following command to run the C++ openCV implementation of the filter

```c++
g++ Opencv_implementation.cpp -o program -I/usr/local/include/opencv4 -lopencv_core -lopencv_highgui -lopencv_imgcodecs -lopencv_imgproc $(pkg-config opencv4 --libs)
```
-----
- Use the following command to run the sequential C++ manual (without openCV built-in function) implementation of the filter

```c++
g++ Sequential_implementation.cpp -o program -I/usr/local/include/opencv4 -lopencv_core -lopencv_highgui -lopencv_imgcodecs -lopencv_imgproc $(pkg-config opencv4 --libs)
```

- Use the following command to run the CUDA-based GPU implementation of the filter

```c++
nvcc -std=c++11 Cuda_implementation -o program -I/usr/local/include/opencv4 -lopencv_core -lopencv_highgui -lopencv_imgcodecs -lopencv_imgproc $(pkg-config opencv4 --libs)
```

- Use the following command to run the execution using a Profiler

```c++
nv-nsight-cu-cli ./program
nsys profile --stats=true --force-overwrite true --show-output true ./program

```



## Authors

- [@kishan92](https://github.com/kishan92)
- [LinkedIn](https://www.linkedin.com/in/kishan-nagendra-profile/)

