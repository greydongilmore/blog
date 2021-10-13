---
title: Image Processing Intro
template: overrides/main.html
---

# Image Processing Intro

Image processing is a large and very general set of tools that are used across a variety of research disciplines to analyze image data. Naturally, image processing algorithms are fundamental to neuroimaging, because a lot (if not all) the data that we analyze in neuroimaging is image data. **Image data** is defined as multi-dimensional homogenous data in which *spatial relationships matter*. That is, neighbouring pixels are treated differently than pixels from disparate parts of the array. Spatial contiguity is meaningful. Usually, image data will have 2 or 3 dimensions, corresponding to the 3 spatial dimensions or 2D projection: either from a specific view-point (think photographs) or through a 3D object (think slice).

### Common image processing operations

There are many different kinds of image processing operations. Here are a few common operations:

- Filtering
  - Detrending
  - Denoising
  - Smoothing
- Segmentation
- Feature detection
- Texture analysis
- Statistical characterization
- Classification
- Registration
- Combination (e.g. 'stitching')

Because of their nature (homogenous/spatial dimensions matter) data lend themselves easily to a representation as arrays. Let's demonstrate this with some human neuroimaging data.

## Nibabel

One of the challenges of data science in neuroimaging (and in other scientific fields) is the range of different file formats that are used to store data. Often these files will be opaque to a naive user, because the data is stored in a binary format, that cannot be read without knowledge of the organization of the data on disks. The [`Nibabel`](https://nipy.org/nibabel/) library alleviates these difficulty through a careful implementation of a wider range of different neuroimaging file-formats. Wherever possible, the library presents a common interface to these different file formats, making it particularly easy to write code that will work on data stored in these different formats.

To install it, you can use the following command-line call:

```console
python -m pip install nibabel
```

## Dipy

[`Dipy`](http://dipy.org) stands for "diffusion MRI in Python", but it is a library devoted to diffusion MRI, as well as other applications in computational neuroimaging.

To install it, you can use the following command-line call:

```console
python -m pip install dipy
```

```python
import dipy.data as dpd
```

```python
remote, local = dpd.fetch_stanford_t1()
```

`remote` is the URL from which the data was read (and a cryptographic hash used to validate the data)

`local` is where the data is stored on your machine

IPython knows how to make sense of that:

```python
!ls $local
```

    HARDI150.bval  HARDI150.bvec  HARDI150.nii.gz  t1.nii.gz


The data is stored in a compressed NIfTI file (`nii.gz` extension). The path to the file we want is:

```python
import os.path as op
t1_file = op.join(local, 't1.nii.gz')
```

The `nibabel` API for reading data from file has two steps:

```python
import nibabel as nib
T1w_img = nib.load(t1_file)
```

Because `nibabel` loads the data "lazily", the data hasn't been read into memory
yet, only some basic metadata stored in the file header. To access the data, we
need to explicitly call the `get_data` method of the image object that we
currently have in memory:


```python
T1w_data = T1w_img.get_data()
```

The data is stored in a `numpy` array. We can verify that by running:


```python
type(T1w_data)
```




    numpy.ndarray



We can check some basic properties of this array by running:


```python
print(T1w_data.shape)
print(T1w_data.dtype)
```

    (81, 106, 76)
    int16


We can also visualize the data that was stored in the file using `Matplotlib`


```python
import matplotlib.pyplot as plt
%matplotlib inline

fig, ax = plt.subplots(1)
ax.matshow(T1w_data[:, :, T1w_data.shape[-1]//2], cmap='bone')
```

    /opt/conda/lib/python3.5/site-packages/matplotlib/font_manager.py:273: UserWarning: Matplotlib is building the font cache using fc-list. This may take a moment.
      warnings.warn('Matplotlib is building the font cache using fc-list. This may take a moment.')
    /opt/conda/lib/python3.5/site-packages/matplotlib/font_manager.py:273: UserWarning: Matplotlib is building the font cache using fc-list. This may take a moment.
      warnings.warn('Matplotlib is building the font cache using fc-list. This may take a moment.')





    <matplotlib.image.AxesImage at 0x7f3420043b00>




    
![png](001-introduction_files/001-introduction_23_2.png)
    


> ## Exercise: The nibabel header
>
> Explore the 'T1w_img' object. How would you extract information about the
> parameters used to collect data? What information is missing?
>


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```

> ## Solution: The nibabel header
>  
> Information about the acquisition can be accessed using the image header:
>
>     hdr = T1w_img.get_header()
>
> For example:
>
>     affine = hdr.get_zooms()
>
> will usually provide the dimensions of the voxel (how do we know the units?)
>
> Some information might be missing from the file header (or not make sense).
> For example, try running:
>
>     hdr.get_n_slices()
>


> ## Affine transforms
>
> The nibabel image header also contains the affine transformation between the
> image and a standard space (usually the scanner iso-center in mm). For more
> information on how and why this information is used, you might want to refer
> to [this excellent tutorial in the nibabel documentation](http://nipy.org/nibabel/coordinate_systems.html).
>
>


```python

```
