---
title: Notes for future reference
author: Bhashithe Abeysinghe
---

# Python modules

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
