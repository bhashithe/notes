---
title: Python Notes
---
# Python modules

## General python

- Instead of `zip` use `izip` which does not create the extra object
- Instead of items() on a dictionary user iteritems()
- Creating a dictionary with keys and values in lists, `d = dict(izip(keys, values))`
- ChainMaps __look this up__

## OS module

``` python
os.chdir() #change directory
os.listdir() #returns a list of directories
os.getcwd() #returns the current working dir
```

A small snippet with image loading from directories

``` python
def load_data(inpath):
        """
        @inpath: string path for the image files to be loaded
                 this path should have images in directories with their label names
        returns => the loaded pickle file
        """
        data = {}
        working_dir = os.getcwd()
        os.chdir(inpath)
        for label in os.listdir():
                data[label] = []
                os.chdir(label)
                images = os.listdir()
                for image in images:
                        data[label].append(cv2.imread(image))
                os.chdir('../')
        os.chdir(working_dir)

        return data

```

## random module

``` python
random.sample([],k) #random sample of k size of the list
```

## importlib module

It is possible to dynamically load modules with this,

``` python
importlib.import_module(module_name)
```

## pytorch module

> If sizes of matrices are different from calculations, you can print the shape of the output in the forward class and then use that size instead

###  GPU

creating variables at GPU is not an inplace method.

``` python
images = images.to(device)
```

### Dataset class

#### Creating Datsets

``` python
__len__() # implement to return the length of the whole dataset
__getitem__() # to get the ith item from the dataset, can return a dictionary also applied transformations
```

#### Loading Aranged data

If data is arranged in the following order, it can be loaded via the `torchvision.datasets.ImageFolder` class

```
./faces/xxx.jpg
yyy.jpg
zzz.jpg
./vehicles/abc.jpg
def.jpg
```

Best to create dataset dictionary and a dataloader dictionary. [Explained here](https://pytorch.org/tutorials/beginner/transfer_learning_tutorial.html#load-data)

### Schedulers

To adjust learning rate using lr_schedulers [documentation] (https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate)

Documentation over [here](https://pytorch.org/docs/stable/torchvision/datasets.html#imagefolder)

### Conv2d

If the padding parameter is not used, applying convolution will change the dimensions of the image used

### DataLoaders

If the batch_size was not specified in the `__init__` it will default to 1

##  argparse module

Using this it is quite easy to handle commandline arguments. Gets the help text and formatting exact. [Example lies here](https://github.com/bhashithe/facebook_friends)
