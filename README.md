# Supervised-Learning for MNIST

I was asked to predict the mod 10 of sum of two digits on MNIST dataset.

I explored techniques to leverage large amounts of unlabelled data to learn image representations. Specifically, I made two types of experiments to learn features in both an unsupervised and a self-supervised manner. In the first trial, I trained a GAN, and then transfer the features of the discriminator (see GAN file). In the second experiment, I trained a self-supervised network that generates free rotating labels by rotating images from the given unlabeled data. I finally chose a rotation prediction method due to the limitation in improving the performance of the GAN model. The detailed implementation I made is as follows: 

<br>

- Dataset/ Dataloader

  - A large unlabelled training set: 72,257 unlabelled images for training
  - A small labelled training set: 500 labelled images for training and 2000 labelled images for validation
            
  
    I extracted a dataset consisting of 0, 90, 180 and 270 degrees rotated images and each label of 0, 1, 2 and 3. 

- Designed Architecture

  I used a convolutional neural network consisting of four convolutional layers and one classification layer (with the number of filter 64). The backbone is designed with convolutional layers consisting of normalization layers and max-pooling layers which is similar to the previous assignment's network, and the head is made up with one convolutional layer.

- Transfer Learning (Down stream task)
  
  After saving the model trained on a large unlabeled dataset in a self-supervised manner (rotation prediction), I transferred its parameters to a small labelled dataset. I only extracted the first 4 layers (the backbone) and froze/unfroze all the weights in those layers. Then, changed the last classification layer (the head) to the custom one which makes a prediction of 10 digits. However, the accuracy was much better if I trained all the layers, finetuned features, than fixed features. 
