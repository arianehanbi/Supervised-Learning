# Supervised-Learning for MNIST

I was asked to predict the mod 10 of a sum of two digits on the MNIST dataset. First, I constructed the dataset of pairs of digits from the MNIST dataset. Moreover, I created two datasets in the right order and left order for both training and testing splits of MNIST (see dataset.py)

![ground truth label](https://user-images.githubusercontent.com/37695060/122198010-0a1e2d00-ce99-11eb-89d9-a3e8691eeccb.png)

Given these two digit images, my network should predict the following operation: (6 + 8) % 10 = 4


<br>
<br>

## Dataset

  For both training and testing, I will use MNIST-train and MNIST-test datasets including images and their corresponding labels. Specifically, set aside 90% of training data for training for both right and left order, and the remaining 10% for validation, and then concatenate the validation sets and test sets for both right and left order into one set using PyTorch Library; ConcatDataset.
  
  ![dataset_right](https://user-images.githubusercontent.com/37695060/122200946-cda00080-ce9b-11eb-877b-6de7d5f46be6.png)
  
  ![data distribution](https://user-images.githubusercontent.com/37695060/122200812-ae08d800-ce9b-11eb-934a-ce5b1a85fbfb.png)

  ![dataset_valid](https://user-images.githubusercontent.com/37695060/122200968-d395e180-ce9b-11eb-8289-35893eb935e5.png)

  ![dataset_test](https://user-images.githubusercontent.com/37695060/122200999-dd1f4980-ce9b-11eb-971e-d9ad73595558.png)

  
## Designed Architecture


  
  In general, relatively few **neurons in the hidden layers** will result in underfitting, so the neural network inadequately detects the signal in the given dataset. On the other hand, relatively many neurons in the hidden layers will result in overfitting, thus the neural network has more information than the training set has, making it impossible to train all neurons in the hidden layer sufficiently. Moreover, **the number of hidden layers** in network architecture is related to model capacity, and the higher the model capacity, the more complex the functions that can be learned by the network. Thus, unless it goes beyond a certain level of complexity, the ability to learn more complex functions means potentially better performance. Lastly, **the learning rate** is a hyper-parameter that determines how fast or slow we will reach the optimal weight. Since it controls how much change the model in response to the estimated error each time the model weight is updated, the model may skip the optimal solution if the learning rate is too large, whereas it takes too long to converge to the best values if it is too small. Now, let's interpret the model performances as follows:

  <br>

  - first model : `1.0903` validation loss and `70.3833` validation accuracy
  - second model : `0.7205` validation loss and `82.7500` validation accuracy
  - third model : `1.0577` validation loss and `66.1667` validation accuracy

  <br>

  The best model is the second model which reaches `82.75%` validation accuracy and `0.7205` validation loss. The results showed that the best number of layers was 2 layers in the hidden layer, the number of hidden neurons was 1024 and 512 respectively and the learning rate was 0.05. Compared to the first model (1 hidden layer, 1024 hidden neurons and 0.05 learning rate), our best model has approximately `12.37%` higher validation accuracy and `0.37` lower validation loss. Therefore, it means that the best model with 2 hidden layers had a higher model capacity, thus showed better performance. Also, compared to the third model (2 hidden layers, 512/256 hidden neurons respectively and 0.01 learning rate), our best model has approximately `16.59%` higher validation accuracy and `0.34` lower validation loss. So, it concludes that the third model with relatively few neurons in the hidden layers was under fitted. Also, it seems like that the third model took a long process to find optimal parameters since it has a relatively small learning rate.
