[![codecov](https://codecov.io/gh/scaramallion/pylibjpeg-libjpeg/branch/master/graph/badge.svg)](https://codecov.io/gh/pydicom/pylibjpeg)
[![Build Status](https://travis-ci.org/scaramallion/pylibjpeg-libjpeg.svg?branch=master)](https://travis-ci.org/scaramallion/pylibjpeg-libjpeg)

## pylibjpeg-libjpeg

A Python 3.6+ wrapper for Thomas Richter's
[libjpeg](https://github.com/thorfdbg/libjpeg), with a focus on use as a
plugin for [pylibjpeg](http://github.com/pydicom/pylibjpeg).

Linux, OSX and Windows are all supported.

### Installation
#### Installing the development version

Make sure [Python](https://www.python.org/) and [Git](https://git-scm.com/) are installed. For Windows, you also need to install
[Microsoft's C++ Build Tools](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16).
```bash
git clone --recurse-submodules https://github.com/pydicom/pylibjpeg-libjpeg
python -m pip install pylibjpeg-libjpeg
```

### Supported JPEG Formats

| ISO/IEC Standard | ITU Equivalent | JPEG Format |
| --- | --- | --- |
| [10918](https://www.iso.org/standard/18902.html) | [T.81](https://www.itu.int/rec/T-REC-T.81/en) | [JPEG](https://jpeg.org/jpeg/index.html)    |
| [14495](https://www.iso.org/standard/22397.html)   | [T.87](https://www.itu.int/rec/T-REC-T.87/en) | [JPEG-LS](https://jpeg.org/jpegls/index.html) |
| [18477](https://www.iso.org/standard/62552.html)   | | [JPEG XT](https://jpeg.org/jpegxt/) |

### Supported Transfer Syntaxes

| UID | Description |
| --- | --- |
| 1.2.840.10008.1.2.4.50 | JPEG Baseline (Process 1) |
| 1.2.840.10008.1.2.4.51 | JPEG Extended (Process 2 and 4) |
| 1.2.840.10008.1.2.4.57 | JPEG Lossless, Non-Hierarchical (Process 14) |
| 1.2.840.10008.1.2.4.70 | JPEG Lossless, Non-Hierarchical, First-Order Prediction (Process 14 [Selection Value 1]) |
| 1.2.840.10008.1.2.4.80 | JPEG-LS Lossless |
| 1.2.840.10008.1.2.4.81 | JPEG-LS Lossy (Near-Lossless) Image Compression |

### Usage
#### With pylibjpeg and pydicom
Assuming you already have *pylibjpeg* and *pydicom* installed:

```python
from pydicom import dcmread
from pydicom.data import get_testdata_file

ds = dcmread(get_testdata_file('JPEG-LL.dcm'))
arr = ds.pixel_array
```

#### Standalone

```python
from libjpeg import decode

with open('filename.jpg', 'rb') as f:
    # Returns a numpy array
    arr = decode(f.read())
```