# Pix2Pix cGAN for Image-to-Image Translation

This tutorial demonstrates how to build and train a conditional generative adversarial network (cGAN) called pix2pix that learns a mapping from input images to output images. The method is based on the paper [Image-to-image translation with conditional adversarial networks](https://arxiv.org/abs/1611.07004) by Isola et al. (2017).

## Overview

Pix2pix is a versatile model that can be applied to a range of tasks, such as:
- Synthesizing photos from label maps
- Generating colorized photos from black and white images
- Turning Google Maps photos into aerial images
- Transforming sketches into photos

In this example, we will generate images of building facades using the [CMP Facade Database](http://cmp.felk.cvut.cz/~tylecr1/facade/).

## Prerequisites

- Python 3.x
- TensorFlow 2.x
- GPU (optional but recommended for faster training)

## Setup

1. **Clone the repository:**
    ```sh
    https://github.com/moto23/pix2pix-ImageTranslation.git
    cd pix2pix-cgan
    ```

2. **Install dependencies:**
    ```sh
    pip install -r requirements.txt
    ```

3. **Download the dataset:**
    Download the preprocessed CMP Facade dataset from [this link](https://efrosgans.eecs.berkeley.edu/pix2pix/datasets/) and extract it into the `data/` directory.

## Model Architecture

- **Generator:** Uses a U-Net-based architecture.
- **Discriminator:** Uses a convolutional PatchGAN classifier.

## Training

1. **Prepare the dataset:**
    Make sure your dataset is in the `data/facades/` directory and structured as follows:
    ```
    data/
        facades/
            train/
                <input-output image pairs>
            val/
                <input-output image pairs>
            test/
                <input-output image pairs>
    ```

2. **Train the model:**
    ```sh
    python train.py --data_dir data/facades --epochs 200 --batch_size 1
    ```

    Note: Each epoch can take around 15 seconds on a single V100 GPU.

3. **Sample Outputs:**
    After training, you can visualize the generated images by running:
    ```sh
    python generate_samples.py --model_dir checkpoints --output_dir results
    ```

## Results

Below are some examples of the output generated by the pix2pix cGAN after training for 200 epochs on the facades dataset.

![sample output_1](https://www.tensorflow.org/images/gan/pix2pix_1.png)
![sample output_2](https://www.tensorflow.org/images/gan/pix2pix_2.png)

## References

- [Image-to-image translation with conditional adversarial networks](https://arxiv.org/abs/1611.07004) - Isola et al. (2017)
- [Conditional Generative Adversarial Nets](https://arxiv.org/abs/1411.1784) - Mirza and Osindero (2014)
- [U-Net: Convolutional Networks for Biomedical Image Segmentation](https://arxiv.org/abs/1505.04597) - Ronneberger et al. (2015)
