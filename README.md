# vdb2raw

## Overview
A simple tool taking a .vdb in input and write a kind of raw file in output.  
If you don't want to compile the tool by yourself, you can find a precompiled win64 executable in the /release directory.

## Building
You need to install [openvdb](https://www.openvdb.org/download/) first.  
The easiest way is to use [vcpkg](https://github.com/microsoft/vcpkg) via :  
 `vcpkg install openvdb:x64-windows`  
Make sure you have already launched `vcpkg Integrate install` once, to integrate vcpkg with Visual Studio.  

## Usage example
```
vdb2raw smoke.vdb
-> density_191x610x178.raw : 100 %
value min/max : 0 / 0.4854
```

## Importing the result in your application
#### Output file format
The output file contains :  
``
width, height, depth
`` in int  
``
data[]
`` in float

#### Loading example in C++
```
#include <fstream>

std::ifstream file("density_191x610x178.raw", std::ifstream::binary);
int dim[3];
file.read((char*)dim, sizeof(int) * 3);
int nbVoxels = dim[0] * dim[1] * dim[2];
float* data = new float[nbVoxels];
file.read((char*)data, sizeof(float) * nbVoxels);
```