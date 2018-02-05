# Conditional Wasserstein GANs

This is an implementation of <a href="https://arxiv.org/pdf/1411.1784.pdf" target="_blank">conditional</a>
<a href="https://arxiv.org/pdf/1406.2661.pdf" target="_blank">GANs</a> using the
<a href="https://arxiv.org/pdf/1704.00028.pdf" target="_blank">Improved Wasserstein (WGAN-GP)</a> method.
Currently I'm trying it out on multiple datasets, though Celeba has been the main target.

## Results
Results can be seen on MNIST, CelebA, and the EFIGI Galaxy dataset.


### MNIST

Below show two examples of the ability to capture style on the MNIST dataset. Each row uses the same z vector, and each column
contains a different y vector representing the label. These can be reproduced via `generate_mnist.py`.

![m1](https://i.imgur.com/4etNYpZ.png) ![m2](https://i.imgur.com/sXic4ao.png)

For these two images, I generated the four corners of each grid, and interpolated between both z and y. Although the model was not
trained on continuous attributes (binary only), it still is able to accurately capture the latent space when given them.
These can be reproduced via `grid.py`.

![m3](https://i.imgur.com/pK14IhX.png) ![m4](https://i.imgur.com/qAiUIOE.png)

### CelebA

These are some results generated by taking random attribute values from the Celeba test set.

| Image         | Attributes    |
|:-------------:|:-------------:|
| ![g1](https://i.imgur.com/lGnnXzq.png) | Male, Smiling  |
| ![g2](https://i.imgur.com/zfAfNI8.png) | Female, Blonde |
| ![g3](https://i.imgur.com/51rzV8s.png) | Female, Heavy Makeup |
| ![g4](https://i.imgur.com/rCYeDw2.png) | Female, Heavy Makeup, Smiling |

Attributes in consideration: bald, bangs, black hair, blond hair, eyeglasses, heavy makeup, male, pale skin, smiling

Male attribute while alternating the others
![m1](https://i.imgur.com/cB0Qqee.png)

![m2](https://i.imgur.com/Cr2uq05.png)

Female attribute while alternating the others
![f1](https://i.imgur.com/2QQgRmV.png)

![f2](https://i.imgur.com/lCiujc3.png)


### Interpolation results

#### On just y
Same z vector being used, but interpolating along the attribute.

##### Bald &rarr; not bald

![b1](https://i.imgur.com/ra1nHXd.png)

##### Female &rarr; male

![b2](https://i.imgur.com/BSRKpd8.png)

##### Male, glasses, smiling, &rarr; male, no glasses, not smiling
![b3](https://i.imgur.com/GCHoFOC.png)


#### Male, glasses, smiling, bangs &rarr; no glasses, not smiling, pale skin, no bangs
![b4](https://i.imgur.com/cVlZnE3.png)

#### On just z
These are interpolating between two different z vectors but using the same y (same attributes).
![i1](https://i.imgur.com/Ca6nRZt.png)

![i2](https://i.imgur.com/7sxwx1a.png)

![i3](https://i.imgur.com/PaDw1RV.png)

#### Grid representation

This shows interpolation between four faces (four corners) using random attributes for each face,
and interpolating between the attributes as well.

![i4](https://i.imgur.com/q13bJL3.png)

### EFIGI Galaxy Dataset


[//]: # I also ran this on the [EFIGI dataset](https://www.astromatic.net/projects/efigi), which is a dataset of images of galaxies
[//]: #with attributes. The attributes I consider in this case are continuous. There are about 40 attributes, but for simplicity I only
[//]: consider four of them. 

[//]: Due to the nature of the data, it is easier to visualize via interpolation along y.

[//]: Arm Strength: More &rarr; Less

[//]: ![ga1](https://i.imgur.com/6CpH7F9.png)


[//]: Arm Curvature: More &rarr; Less

[//]: ![ga2](https://i.imgur.com/oqg1B1z.png)


[//]: Visible Dust: More &rarr; Less

[//]: ![ga3](https://i.imgur.com/6YXpYAT.png)


[//]: Neighboring Galaxy Abundance: More &rarr; Less

[//]: ![ga4](https://i.imgur.com/3XoDuvQ.png)



### How to run
1. Download the cropped and aligned celebA dataset from [here](http://mmlab.ie.cuhk.edu.hk/projects/CelebA.html)
as well as the annotations.

2. Your folder layout must be like so:
```
root_celeba/
   img_align_celeba/
   img_align_celeba_cropped/
   list_attr_celeba.txt
```

3. Run the crop script on the downloaded images. `img_align_celeba_cropped/` is an empty folder made by you.
Then copy the `ops/crop_images.py` file to your `root_celeba/` folder and run

   `python crop_images.py`


## TODO
Everything is in different folders. Ideally, I'd like to have just one.
