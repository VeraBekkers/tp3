FROM  pytorch/pytorch:1.9.1-cuda11.1-cudnn8-devel

# remove repo keys to avoid apt-get from failing
RUN rm /etc/apt/sources.list.d/cuda.list
RUN rm /etc/apt/sources.list.d/nvidia-ml.list

ENV FORCE_CUDA 1
ENV TORCH_CUDA_ARCH_LIST "3.5 5.2 6.0 6.1 7.0+PTX"

# for gdal
RUN apt-get update
RUN apt-get install gdal-bin -y
RUN apt-get install libgdal-dev -y
ENV CPLUS_INCLUDE_PATH=/usr/include/gdal
ENV C_INCLUDE_PATH=/usr/include/gdal
RUN pip install --upgrade setuptools==57.4.0
RUN pip install GDAL==2.2.2

ADD requirements.txt /
RUN --mount=type=cache,target=/root/.cache \
    pip install -r /requirements.txt

RUN pip install pyvista pytorch-lightning
RUN pip install --upgrade jsonschema
RUN --mount=type=cache,target=/root/.cache \
    pip install torch-points3d
RUN apt-get install -qq xvfb libgl1-mesa-glx -y

RUN apt-get install git -y
RUN git clone https://github.com/torch-points3d/torch-points3d.git
WORKDIR torch-points3d

RUN apt-get install libxrender1 -y
