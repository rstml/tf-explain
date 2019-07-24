# tf-explain

[![Build Status](https://api.travis-ci.org/sicara/tf-explain.svg?branch=master)](https://travis-ci.org/sicara/tf-explain)
[![Documentation Status](https://readthedocs.org/projects/tf-explain/badge/?version=latest)](https://tf-explain.readthedocs.io/en/latest/?badge=latest)
![Python Versions](https://img.shields.io/badge/python-3.6%20|%203.7-%23EBBD68.svg)
![Tensorflow Versions](https://img.shields.io/badge/tensorflow-2.0.0--beta1-blue.svg)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/python/black)

__tf-explain__ implements interpretability methods as Tensorflow 2.0 callbacks to __ease neural network's understanding__.

## Installation

__tf-explain__ is not available yet on Pypi. To install it, clone it locally:

```bash
virtualenv venv -p python3.6
git clone https://www.github.com/sicara/tf-explain
pip install -e .
```

## Available Methods

1. [Activations Visualization](#activations-visualization)
2. [Occlusion Sensitivity](#occlusion-sensitivity)
3. [Grad CAM (Class Activation Maps)](#grad-cam)

### Activations Visualization

> Visualize how a given input comes out of a specific activation layer

```python
from tf_explain.callbacks.activations_visualization import ActivationsVisualizationCallback

model = [...]

callbacks = [
    ActivationsVisualizationCallback(
        validation_data=(x_val, y_val),
        layers_name=["activation_1"],
        output_dir=output_dir,
    ),
]

model.fit(x_train, y_train, batch_size=2, epochs=2, callbacks=callbacks)
```

<p align="center">
    <img src="./docs/assets/activations_visualisation.png" width="400" />
</p>


### Occlusion Sensitivity

> Visualize how parts of the image affects neural network's confidence by occluding parts iteratively

```python
from tf_explain.callbacks.occlusion_sensitivity import OcclusionSensitivityCallback

model = [...]

callbacks = [
    OcclusionSensitivityCallback(
        validation_data=(x_val, y_val),
        patch_size=4,
        class_index=0,
        output_dir=output_dir,
    ),
]

model.fit(x_train, y_train, batch_size=2, epochs=2, callbacks=callbacks)
```

<div align="center">
    <img src="./docs/assets/occlusion_sensitivity.png" width="200" />
    <p style="color: grey; font-size:small; width:350px;">Occlusion Sensitivity for Tabby class (stripes differentiate tabby cat from other ImageNet cat classes)</p>
</div>

### Grad CAM

> Visualize how parts of the image affects neural network's output by looking into the activation maps

From [Grad-CAM: Visual Explanations from Deep Networks
via Gradient-based Localization](https://arxiv.org/abs/1610.02391)

```python
from tf_explain.callbacks.grad_cam import GradCAMCallback

model = [...]

callbacks = [
    GradCAMCallback(
        validation_data=(x_val, y_val),
        layer_name="activation_1",
        class_index=0,
        output_dir=output_dir,
    )
]

model.fit(x_train, y_train, batch_size=2, epochs=2, callbacks=callbacks)
```


<p align="center">
    <img src="./docs/assets/grad_cam.png" width="200" />
</p>


## Roadmap

Next features are listed as issues with the `roadmap` label.
