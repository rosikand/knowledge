---
categories: [advanced, ml]
---

# Config files for machine learning experimentation 

It has become common to use config files to specify experiment hyperparams when training your models. This is to increase reproducability, modularity, and efficiency when experimenting.

Some packages try to support this:
- [YACS](https://github.com/rbgirshick/yacs)
- [ml_collections](https://github.com/google/ml_collections) 


## Examples 

### `ml_collections`: 

check out [this](https://github.com/ikostrikov/walk_in_the_park/blob/main/configs/droq_config.py) codebase. 


```python
import ml_collections

def get_config():
    config = ml_collections.ConfigDict()

    config.lr = 3e-1
    config.critic_lr = 3e-4
    config.temp_lr = 3e-4

    config.hidden_dims = (256, 256)

    return config
```

this package also supports 

- command line flags (see `absc.flags`) 

### YACS 

... 

### Python OOP 

My currently preferred method is to just use standard python classes. That way, you don't have to deal with the whole `getattr` business with traditional YAML files (programmatic configs!).  

1. Define a `configs.py` file in your working directory. 
2. In `configs.py`, define the `BaseConfig` class which creates all the valid fields as class attributes and provides default values for them. 
3. Create child classes of `BaseConfig` for each new experiment where you only change the hyperparameter you are optimizing. 

Example: 

 
```python
"""
File: configs.py
------------------
Holds the configs classes/objects.
"""


import modules
import optax
import rsbox
from rsbox import ml
import experiments
import cloudpickle as cp


class BaseConfig:
    model = modules.CNN()  # unlike raw yaml, you can specify modules programatically 
    trainloader, testloader = modules.get_dataloaders()
    epochs = 10
    lr = 0.001
    momentum = 0.9
    optimizer = optax.sgd(lr, momentum)
    criterion = modules.softmax_ce
    metrics = {
        'loss': ml.MeanMetric(),
        'accuracy': modules.AccuracyMetric()
    }
    experiment = experiments.SampleExperiment
    
    

class TestNewLR(BaseConfig):
    """Testing larger learning rate"""
    lr = 0.1
    


config = TestNewLR()
```

It may also then be helpful to define `modules.py` to specify things like the loss, metric functions, and models, etc. 

then in `main` in `runner.py`: 

 
```python
import configs
import experiments
import argparse
import warnings

def main(args):
    if args.config is None:
        config_class = 'BaseConfig'
    else:
        config_class = args.config
    cfg = getattr(configs, config_class)
    exp = cfg.experiment(cfg)
    exp.debug()




if __name__ == '__main__':

    # configure args 
    parser = argparse.ArgumentParser(description="specify cli arguments.", allow_abbrev=True)
    parser.add_argument("-config", type=str, help='specify config.py class to use.') 
    args = parser.parse_args()
    main(args)
```

then, run using `python3 runner.py -c TestNewLR`. 


### `types.SimpleNamespace`

You might be wondering, "wouldn't c++-like structs be of good use here?". Well, Python has this not-as-well-known feature called `SimpleNamespace`. 

> "Python's SimpleNamespace class provides an easy way for a programmer to create an object to store values as attributes without creating their own (almost empty) class." - ([link](https://lwn.net/Articles/818777/)) 

This [notebook](https://github.com/soumik12345/functorch-examples/blob/main/01_classfier_training.ipynb) provides an example. 

```python
default_config = SimpleNamespace(
            batch_size = 64,
            num_workers = 4,
            learning_rate = 1e-2,
            epochs = 10,
            artifact_address = 'geekyrakshit/functorch-examples/cifar-10:v0',
            device = "cuda:0" if torch.cuda.is_available() else "cpu",
            classes = (
                'plane', 'car', 'bird', 'cat', 'deer',
                'dog', 'frog', 'horse', 'ship', 'truck')
)
```

Problem I see: can't use inheritance so you have to re-define all non-changed hyperparams for each new config. 






