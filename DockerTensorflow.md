#Usage of Tensorflow docker container with GPU support

##Starting point:
* https://www.tensorflow.org/install/docker
* https://hub.docker.com/r/tensorflow/tensorflow/

##Steps

### Step 1: Install NVIDIA driver
The script that I downloaded from [the Nvidia site](https://www.nvidia.com/object/unix.html) did not work.
Therefore I used [an alternative way](http://www.linuxandubuntu.com/home/how-to-install-latest-nvidia-drivers-in-linux).
However I had to make a slight adjustment during installation described on
[askubuntu](https://askubuntu.com/questions/951046/unable-to-install-nvidia-drivers-unable-to-locate-package).

I replaced original command:
```bash
sudo apt install nvidia-<version number>
```
with
```bash
sudo apt install nvidia-driver-<version number>
```

### Step 2: Install NVIDIA Container Runtime 
https://github.com/NVIDIA/nvidia-docker

### Usage examples

Run Jupyter Notebook with tensorflow usage examples
```bash
docker run --runtime=nvidia -it -p 8888:8888 tensorflow/tensorflow:latest-gpu
```

Use the latest TensorFlow GPU image to start a bash shell session in the container:
```bash
docker run --runtime=nvidia -it tensorflow/tensorflow:latest-gpu bash
```
Run python code with tensorflow usage:
```bash
docker run -it --rm tensorflow/tensorflow \
   python -c "import tensorflow as tf; tf.enable_eager_execution(); print(tf.reduce_sum(tf.random_normal([1000, 1000])))"
```
To run a TensorFlow program developed on the host machine within a container, mount the host directory and change the container's working directory (-v hostDir:containerDir -w workDir):
```bash
docker run -it --rm -v $PWD:/tmp -w /tmp tensorflow/tensorflow python ./script.py
```


### See also
* [TensorFlow Dockerfiles on GitHub](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/tools/dockerfiles)
