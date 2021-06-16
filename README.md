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

<br>

## Designed Architecture
I built fully connected networks consisting of up to two hidden layers and different neurons in the hidden layers.

In general, relatively few **neurons in the hidden layers** will result in underfitting, so the neural network inadequately detects the signal in the given dataset. On the other hand, relatively many neurons in the hidden layers will result in overfitting, thus the neural network has more information than the training set has, making it impossible to train all neurons in the hidden layer sufficiently. Moreover, **the number of hidden layers** in network architecture is related to model capacity, and the higher the model capacity, the more complex the functions that can be learned by the network. Thus, unless it goes beyond a certain level of complexity, the ability to learn more complex functions means potentially better performance. Lastly, **the learning rate** is a hyper-parameter that determines how fast or slow we will reach the optimal weight. Since it controls how much change the model in response to the estimated error each time the model weight is updated, the model may skip the optimal solution if the learning rate is too large, whereas it takes too long to converge to the best values if it is too small. 
  
<br>

## Training

Now, let's interpret the model performances as follows:

  <br>
  
  - Train on **right-order dataset**

    - first model : `1.0903` validation loss and `70.3833` validation accuracy
    - second model : `0.7205` validation loss and `82.7500` validation accuracy
    - third model : `1.0577` validation loss and `66.1667` validation accuracy

![train_right](https://user-images.githubusercontent.com/37695060/122202404-50758b00-ce9d-11eb-916f-e09ac47dd5b8.png)

  The best model is the second model which reaches `82.75%` validation accuracy and `0.7205` validation loss. The results showed that the best number of layers was 2 layers in the hidden layer, the number of hidden neurons was 1024 and 512 respectively and the learning rate was 0.05. Compared to the first model (1 hidden layer, 1024 hidden neurons and 0.05 learning rate), our best model has approximately `12.37%` higher validation accuracy and `0.37` lower validation loss. Therefore, it means that the best model with 2 hidden layers had a higher model capacity, thus showed better performance. Also, compared to the third model (2 hidden layers, 512/256 hidden neurons respectively and 0.01 learning rate), our best model has approximately `16.59%` higher validation accuracy and `0.34` lower validation loss. So, it concludes that the third model with relatively few neurons in the hidden layers was under fitted. Also, it seems like that the third model took a long process to find optimal parameters since it has a relatively small learning rate.


<br>

  - Train on **concatenated dataset**

    - first model with concatenated training dataset : `0.8247` validation loss and `78.3167` validation accuracy
    - second model with concatenated training dataset : `0.4104` validation loss and `90.35` validation accuracy
    - third model with concatenated training dataset : `0.5904` validation loss and `82.15` validation accuracy

![concat_right](https://user-images.githubusercontent.com/37695060/122202685-916d9f80-ce9d-11eb-8cc3-bd5429ac8ebc.png)

  The best model is again the second model which reaches `90.35%` validation accuracy and `0.4104` validation loss. The results showed that the best number of layers was 2 layers in the hidden layer, the number of hidden neurons was 1024 and 512 respectively and the learning rate was 0.05. Compared to the first model (1 hidden layer, 1024 hidden neurons and 0.05 learning rate), our best model has approximately `12.04%` higher validation accuracy and `0.41` lower validation loss. Therefore, it means that the best model with 2 hidden layers had a higher model capacity, thus showed better performance. Also, compared to the third model (2 hidden layers, 512/256 hidden neurons respectively and 0.01 learning rate), our best model has approximately `8.2%` higher validation accuracy and `0.18` lower validation loss. So, it concludes that the third model with relatively few neurons in the hidden layers was under fitted. Also, it seems like that the third model took a long process to find optimal parameters since it has a relatively small learning rate.

  <br>


## Evaluation

  - Train on **right-order dataset**
    - first model : `70.3833` validation accuracy
    - second model : `82.7500` validation accuracy
    - third model : `66.1667` validation accuracy

 <br>

  - Train on **concatenated dataset**
    - first model with concatenated training dataset : `78.3167` validation accuracy
    - second model with concatenated training dataset : `90.35` validation accuracy
    - third model with concatenated training dataset : `82.15` validation accuracy

 <br>

The best model is the second model with the concatenated training set. The difference between the quality of the models trained on the different training sets is simply because more data gives better results. However, it is not always true that more data gives better results, but we can conclude that the concatenated training set demonstrates better performance in our case.

## Conclusion


For the selected model is the model2 with the concatenated dataset. As we can see the accuracy values below, those are similar to each other, and thus this model is reasonably well-fitted.

|  |accuracy|
|:--|:------|
|Validation| 90.35%|
|Testing|90.98%|

<br>

The reason why is the model better/worse on some digits is because the frequency of each label in the test set is not equally distributed. 

![test](https://user-images.githubusercontent.com/37695060/122203927-d514d900-ce9e-11eb-90f9-66ded26bdb6b.png)



