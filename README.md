# deepmux-python

**deepmux** is a PaaS solution to effortlessly deploy trained machine learning models on the cloud and generate predictions without setting up any hardware.

At the moment only **pytorch** models are supported.

## Installation

```
pip install deepmux==0.2.1
```

## Quickstart

### Creating model
Initialize a model and upload it to deepmux servers

```python
from deepmux import create_model

model = create_model(<YOUR PYTORCH MODEL>, <MODEL_NAME>, <SHAPE OF INPUT DATA>, <SHAPE OF OUTPUT DATA>, <TOKEN>)
```

### Getting model by name
On your production server you can simply get model by it's name.
```python
from deepmux import get_model

model = get_model(<MODEL NAME>, <TOKEN>)
```

### Executing model on your import

After initializing your model with `create_model` or `get_model` you can run the model. All computations will be performed on **deepmux** infrastucture.

```python
output = model.run(<YOUR INPUT>)
```

### Complete example on a model from PyTorch Hub

```python
import numpy as np
import torch

from deepmux import create_model

token = "<YOUR_TOKEN>"

pytorch_model = torch.hub.load('pytorch/vision:v0.5.0', 'fcn_resnet101', pretrained=True)

deepmux_model = create_model(
    pytorch_model,
    model_name='my_model',
    input_shape=[1, 3, 600, 800],
    output_shape=[1, 21, 600, 800],
    token=token)

dummy_input = np.zeros([1, 3, 600, 800], dtype=np.float32)

output = deepmux_model.run(dummy_input)
```

## Getting token

Currently, **deepmux** is in closed testing. You can get your own token by contacting [tna0y](https://t.me/tna0y) or 
[alexsaplin](https://t.me/alexsaplin).
