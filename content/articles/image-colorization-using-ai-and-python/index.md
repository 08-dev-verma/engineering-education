[DeOldify](https://github.com/jantic/DeOldify) is a Deep Learning (DL) based project for colorizing and restoring old images and video. It helps us add color old black and white photos adding life into them. The DL model uses a unique NoGAN architecture to train the model. We will use this model to convert some old black and white photos of a city adding color to them.

### Prerequisite
To follow along, you need to be familiar with:
- Machine Learning algorithms.
- Google Colab.

### Outline
- [The Deoldify model](#the-deoldify-model)
- [Cloning the GitHub Repository for the model](#cloning-the-github-repository-for-the-model)
- [Installing the necessary dependencies](#installing-the-necessary-dependencies)
- [Downloading the model](#downloading-the-model)
- [Performing colorization on old black and white photos](#performing-colorization-on-old-black-and-white-photos)
- [Wrapping up](#wrapping-up)
- [References](#references)

### The Deoldify model 
Deoldify uses a Generative Adversarial Neural Network (GAN). But it uses a special type of GAN called a self-attention GAN. Aside from using self-attention GAN and some special transformations, this model also uses a special technique known as No-GAN. It is a highly efficient way of training GANs.

Most GANs have two parts; a Generator and a Discriminator. The Generator is the part that creates the image. The discriminator tries to pick out real color images from fake recolored images. The No-GAN technique works by training the Generator and the Discriminator models present in GANs in isolation. This is similar to how you would train a normal neural network, but different with GANs are they are usually trained side by side. Then, they are fine-tuned together, typically how you would train a GAN.   

The model works by taking a black and white image, and pass it to the Deoldify model. The model will then output a colored image. The model is trained on a lot of colored images and does a good job in producing colored images.

That's a summary of the Deoldify model in a nutshell. Please visit this GitHub [documentation](https://github.com/jantic/DeOldify) to learn more. 

### Cloning the GitHub Repository for the model
We are going to use the GitHub repository that contains the actual model. Inside our Google Colab, let's type in the following code:

```bash
!git clone https://github.com/jantic/DeOldify.git DeOldify
```

### Installing the necessary dependencies
To use the model, we need to install a couple of dependencies.

```python
!pip install opencv-python==4.4.0.42
!pip install -r requirements.txt
```

The `opencv-python` dependency allows us to work with images in Python. By running the `!pip install -r requirements.txt` command, all the dependencies available in the `requirement.txt` file gets installed. These dependencies include:

- fastai==1.0.51
- wandb
- tensorboardX==1.6
- ffmpeg-python
- youtube-dl>=2019.4.17
- jupyterlab
- pillow>=8.0.0

### Downloading the model
Next, we will need to download the pre-trained model.

### Performing colorization on old black and white photos 
Let's now take black and white images and add some color to them. We will use old images of iconic buildings that still stand to date of the city of Nairobi, Kenya.

Image one:

![KICC](/engineering-education/image-colorization-using-ai-and-python/kicc.jpg)

Image two:

![Nairobi]](/engineering-education/image-colorization-using-ai-and-python/nairobi.jpg)

Image three:

![New stanley hotel](/engineering-education/image-colorization-using-ai-and-python/new-stanley-hotel.jpg)

Image four:

![National archives](/engineering-education/image-colorization-using-ai-and-python/national-archives.jpg)


Please find the complete code for this tutorial [here](https://colab.research.google.com/drive/1bh15liSGDkUMwez4xNH1kG6ETFxQVlZ6?usp=sharing).

### Wrapping up
The Deoldify model let's you recolor old images and videos of family members or even cities. The model is open-source and it's available through [GitHub](https://github.com/jantic/DeOldify).

### References
- [DeOldify: A Deep Learning based project for colorizing and restoring old images](https://github.com/jantic/DeOldify)

---
Peer Review Contributions by: [Wilkister Mumbi](/engineering-education/authors/wilkister-mumbi/)
