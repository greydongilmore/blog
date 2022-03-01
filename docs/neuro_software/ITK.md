---
title: ITK
template: overrides/main.html
---

# Installing ITK

## Linux

Create a build, install and source directory for ITK:

```console
mkdir ~/Downloads/itk_{build,source}
```

Obtain the newest version of [SimpleITK](https://sourceforge.net/projects/niftyreg/files/latest/download) or by running the following:

```console
cd ~/Downloads/itk_source
git clone --recursive https://github.com/SimpleITK/SimpleITK.git .
```

### Run CMake/Make

!!! Note 
    If you don't have make/cmake, follow the steps in this [guide](../operating_systems/cmake.html).

Make the build and install directories. 

The default install location is `/usr/local`, which falls on your PATH. This is the easiest location to install. If you want to install somewhere else then specify the path in the `CMAKE_INSTALL_PREFIX` variable.

```console
cd ~/Downloads/itk_build
ccmake ~/Downloads/itk_source/SuperBuild
```

Press __'c'__ to configure the ITK project, press __'c'__ again to finalize the configuration. Once the project is correctly configured, press the __'g'__ key to generate the Makefiles. You can then build and install the project:

```console
make -j4
```

If the install prefix directory you chose in ccmake is not on your PATH, you will need to add it to your PATH. In order to use ITK in any terminal, you will need to edit your `.profile` file by adding the following lines:

```
ITKbin=<path_to_your_ITK_install>
export PATH={ITKbin}/ITK-build/bin:${PATH}
export LD_LIBRARY_PATH={ITKbin}/ITK-build/lib :${LD_LIBRARY_PATH}
```

