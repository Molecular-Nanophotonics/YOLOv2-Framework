# YOLOTrack 1.0

*M. Fränzl*

Molecular Nanophotonics Group, Peter Debye Institute for Soft Matter Physics, Universität Leipzig, Linnestr. 5, 04103 Leipzig, Germany

[[1] M. Fränzl and F. Cichos, Active Particle Feedback Control with a Single‑Shot Detection Convolutional Neural Network, *Sci. Rep.* **10**, 12571 (2020)](http://www.nature.com/articles/s41598-020-69055-2).

## Content

- [Discription](#discription)
- [Repository Contents](#repository-contents)
- [Users Guide](#users-guide)
- [System Requirements](#system-requirements)
- [Setup Instructions](#setup-instructions)
- [License](./LICENSE)

## Discription 

This is a framework for the real-time localization and classification of objects in optical microscopy images using a single-shot covolutional neural network YOLO ("You Only Look Once") . We adapted the TinyYOLOv2 architecture enabling to localize and classify objects at very low signal-to-noise ratios for images as large as 416 x 416 px at frame rates of up to 100 fps. Here, we provide scripts to train the network in Python/Keras using the TensorFlow backend and source codes to run the model inference on a GPU with C++ or LabVIEW.

<p align="center">
  <img src="Resources/YOLOTrack10-Detection-Example.png" width=380> <br>
  <b>Fig. 1</b> YOLOTrack 1.0 detection for a synthetic image of microparticles as observed in a darkfield microscope.
</p>



## Repository Contents

- [YOLOTrack 1.0 Training (Python)](./YOLOTrack%201.0%20Training%20(Python)):  Jupyter notebooks and Python modules for synthetic image generation, training and exporting YOLOTrack 1.0 models with Python/Keras using the TensorFlow backend
- [TF DLL](./TF%20DLL): DLL for running TensorFlow models on GPU (`TF.dll`)
- [YOLOTrack 1.0 DLL](./YOLOTrack%201.0%20DLL): DLL for decoding the YOLOTrack 1.0 output tensor (`YOLOTrack10.dll`)
- [YOLOTrack 1.0 Inference (LabVIEW)](./YOLOTrack%201.0%20Inference%20(LabVIEW)): Example for importing and running a trained YOLOTrack 1.0 model in LabVIEW
- [YOLOTrack 1.0 Inference (C++)](./YOLOTrack%201.0%20Inference%20(C%2B%2B)): Example for importing and running a trained model with Qt/C++

## Users Guide

The network is trained and evaluated in Python/Keras using the TensorFlow backend. For real-time inferencethe model graph is exported as protocol buffer file (`*.pb`) and parameters required to decode the YOLOTrack 1.0 output are exported to an INI file (`*.ini`). These files are imported by the C based dynamic link libraries `TF.dll`, `YOLOTrack10.dll` that are easily integrable in other programming languages such as LabVIEW and C++. Fig. 1 shows the structure of the framework.

<p align="center">
  <img src="Resources/YOLOTrack10-Framework-Design.png" width=550> <br><br>
  <b>Fig. 2</b> Design of the framework used for training and real-time inference.
</p>

The `TF.dll` is a generic library for the inference of TensorFlow models build on top of the GPU supported [TensorFlow C API](https://www.tensorflow.org/install/lang_c) (`tensorflow.dll`). It can be used with any TensorFlow model and is not specific to YOLOTrack. It is a copy of [TF-Framework/TF DLL](https://github.com/Molecular-Nanophotonics/TF-Framework/tree/master/TF%20DLL). The `YOLOTrack10.dll` adds specific functions required to decode the YOLOTrack 1.0 output and does not depend on the [TensorFlow C API](https://www.tensorflow.org/install/lang_c).

## System Requirements

 The framework requires Windows 7, 10 (64-Bit) and a GPU that supports CUDA Toolkit 10.0. It has been tested on the following system:
 - Windows 7, 64-Bit
 - Intel Core i7-2600 4 × 3.40 GHz CPU
 - GeForce GTX 1660 Ti GPU
 - CUDA Toolkit 10.0 + cuDNN 7.4.2
 - TensorFlow 1.14.0 GPU

## Setup Instructions

For setup instructions refer to the `README.md` in each directory. 
