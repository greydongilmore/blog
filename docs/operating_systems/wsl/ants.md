---
title: Advanced Normalization Tools (ANTs)
template: overrides/main.html
---

## Get the latest ANTs code

Download the latest code into an arbitrary directory, I use `~/code`:

```console
cd ~/code
mkdir ants_{build,install,source}
git clone https://github.com/ANTsX/ANTs.git ./ants_source
```

You will also need to install the ZLIB libraries:

```console
sudo apt-get install zlib1g-dev
```

## Run CMake/Make

I install custom software in `/opt`, which is the default location with ANTs `/opt/ANTs`. You can chnage the path within ccmake.

```console
cd ~/code/ants_build
ccmake ~/code/ants_source
```

Hit __'c'__ to do an initial configuration. CMake will do some checking and then present options for review. Hit __'c'__ again to do another round of configuration. If there are no errors, you're ready to generate the make files by pressing __'g'__.

Now you are back at the command line, it's time to compile. To save time, you can use multiple threads by using `-j`, for example:

```console
sudo make -j2
```

The build and install will happen together so you will not need to run `make install`.

## Post-install Configuration

If you want to use ANTs scripts, copy them from the source directory `/ants_source/Scripts/` to the `/opt/ANTs/bin` directory where `antsRegistration` etc are located:

```console
cp -r ~/code/ants_source/Scripts/* /opt/ANTs/bin/
```

After the build, there will be a binary directory `/opt/ANTs/bin` that contains the programs (and scripts if you've included them). The scripts additionally require ANTSPATH to point to the bin directory including a trailing slash.

You will need to edit your ```.profile``` file by adding the following lines:

```console
export ANTSPATH=${HOME}/opt/ANTs/bin
export PATH=${ANTSPATH}:$PATH
```

Close your WSL and reopen. Now check the install by running:

```console
which antsRegistration
```
