---
title: FMRIB Software Library (FSL)
template: overrides/main.html
---

# Installing FSL

The easiest method is to download this [python script](https://fsl.fmrib.ox.ac.uk/fsldownloads_registration/). You will need to register. On the subsequent page you will download the `fslinstaller.py` file.

## Installing on Pop_OS!

You will first need to run the following steps prior to installing FSL.

!!! note
    The following steps were originally written here <a href='https://forums.linuxmint.com/viewtopic.php?p=1531616&sid=eca87543f47ece83994a3e3b656447c3#p1531616' target="_blank"> __here__ </a>.

!!! warning
    make sure you run a backup prior to performing this hack… just in case.

1. move your current OS information files into a temporary location:

    ```console
    sudo mv /etc/os-release /etc/os-release.pop && sudo mv /etc/lsb-release /etc/lsb-release.pop
    ```

2. write a new `os-release` file:

    ```console
    sudo gedit /etc/os-release
    ```

    copy the following into this file:

    ```
    NAME="Ubuntu"
    VERSION="20.04 LTS (Focal Fossa)"
    ID=ubuntu
    ID_LIKE=debian
    PRETTY_NAME="Ubuntu 20.04 LTS"
    VERSION_ID="20.04"
    HOME_URL="https://www.ubuntu.com/"
    SUPPORT_URL="https://help.ubuntu.com/"
    BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
    PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
    VERSION_CODENAME=focal
    UBUNTU_CODENAME=focal
    ```

3. write a new lsb-release file:

    ```console
    sudo gedit /etc/lsb-release
    ```

    copy the following into this file:

    ```
    DISTRIB_ID=Ubuntu
    DISTRIB_RELEASE=20.04
    DISTRIB_CODENAME=focal
    DISTRIB_DESCRIPTION="Ubuntu 20.04 LTS"
    ```

4. now run the fslinstaller.py script in the below section and return here to Step 5 to return your OS information.

5. after running the FSL install steps, remove the files you wrote:

    ```console
    sudo rm /etc/os-release && sudo rm /etc/lsb-release
    ```

6. move the original files back:

    ```console
    sudo mv /etc/os-release.pop /etc/os-release && sudo mv /etc/lsb-release.pop /etc/lsb-release
    ```

## Linux

Run the following in a linux terminal (the install will take awhile):

```console
python /home/*[your_username]*/Downloads/fslinstaller.py
```

You will also need to install the package `wxpython`:

```console
pip install wxpython
```

If that does not work then run:

```console
pip install -U -f https://extras.wxpython.org/wxPython4/extras/linux/gtk3/ubuntu-16.04 wxPython
```

### Potential libraries you may need

You may need to install some of the following libraries.

**Multiple-image Network Graphics library (libmng)**

```console
sudo apt-get install libmng2
sudo apt-get install libmng-dev
```

**PNG library - development (libpng-dev)**

```console
sudo apt-get install libpng-dev
```

**Optimized BLAS (linear algebra) library (libopenblas-base)**

```console
sudo apt-get install libopenblas-base
export LD_LIBRARY_PATH=/usr/lib/openblas-base/
```

**libmng.so.1 Error**

You will need to create a symbolic link for the library dll ```libmng.so.1```:

```console
sudo ln -s /usr/lib/x86_64-linux-gnu/libmng.so.2 /usr/lib/x86_64-linux-gnu/libmng.so.1
```

**Independent JPEG Group's JPEG runtime library (libjpeg62)**

```console
sudo apt-get install libjpeg62
```

**PNG library - runtime (libpng12.deb)**

```console
wget -q -O /tmp/libpng12.deb http://mirrors.kernel.org/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1_amd64.deb \
  && sudo dpkg -i /tmp/libpng12.deb \
  && rm /tmp/libpng12.deb
```

**GTK+ graphical user interface library (gtk2.0)**

```console
sudo apt-get install gtk2.0
```

**Pulseaudio for other random libraries**

```console
sudo apt-get install pulseaudio
```

**You may also receive an error `No D-BUS daemon running`**

run the following:

```console
sudo chown -R *[your username]*:admin ~/.dbus
```
