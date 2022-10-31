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

My currently preferred method is to just use standard python classes. That way, you don't have to deal with the whole `getattr` business with traditional YAML files. 

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
    # silence warnings 
    # warnings.filterwarnings("ignore")

    # configure args 
    parser = argparse.ArgumentParser(description="specify cli arguments.", allow_abbrev=True)
    parser.add_argument("-config", type=str, help='specify config.py class to use.') 
    args = parser.parse_args()
    main(args)
```

then, run using `python3 runner.py -c TestNewLR`. 


 




