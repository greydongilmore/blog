---
title: Make/Cmake
template: overrides/main.html
---

## Install Make

### Linux

Install build essentials and Make first:

```console
sudo apt-get install make
sudo apt-get update && sudo apt-get install build-essential
```

## Install CMake

Download the latest version of CMake from the [Cmake website](https://cmake.org/download/).

### Linux

From the website, download the bash shell script. It's best to keep manually installed packages within the `/opt` directory.

In your linux shell run:

```console
cd /opt
chmod +x /home/[your_username]/Downloads/cmake-*-Linux-x86_64.sh
sudo /home/[your_username]/Downloads/cmake-*-Linux-x86_64.sh
```

Then add the following to your `~/.profile`:

```
export PATH=/opt/cmake-3.13.3-Linux-x86_64/bin:$PATH
```