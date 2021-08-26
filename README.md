# PokemonSpriteCNN
![CharizardDon3](https://user-images.githubusercontent.com/17886837/131034019-22477bf3-1513-44c1-af13-b888fbb134c9.PNG)

# Introduction
If you're anything like me and grew up in the early 2000s, you probably also have the same fascination I do with Pokemon. I used to "borrow" my brother's Gameboy to play Pokemon Crystal so much that my parents had to end up getting me my own. My intention for this project was to combine my nostalgic appreciation for Pokemon and cement some python and machine learning concepts I've been watching on Coursera. The goal was to create some model that takes in an image of a Pokemon and predicts its type (fire, water, grass, etc.) and stats.


# WebScraping and Data Agumentation
The first step of this project was to compile all the images to train the model. I started by webscrapping all of the images from the most recent generation, which resulted in ~800 training examples for 20 different classes. The thinking was that higher resolution training examples would provide better training data; however, that decision proved poor. It was challenging to train the model with that few training examples, so I went back and downloaded more from older generations to have closer to 6k training examples.  To further augment the data, the convolutional model included a random horizontal flip and a random rotation. Images of the current training dataset can be seen below

![Training Example](https://user-images.githubusercontent.com/17886837/131034676-3ee61758-48de-47db-805c-fe99041cec2d.PNG)

# Convolutional Model Development
The training data looks sufficient at this point. Now, we can look at developing the convolutional model. Given the size of the dataset and that Pokémon type recognition seemed akin to classifying animals at a zoo, transfer learned from readily available pre-trained networks seemed like an auspicious path.

To speed up the model selection profess, I opted to reduce the image size down to 75x75 to weed our poorly performing models in favor of moe auspicious architectures. Then, once I was happy with the model, I updated image size to 128x128. Althought it drastically increased the training time, the accuracy increased by around 20% with the increased resolution. Since all of teh preliminary development was done on smaller files, I was able to consider more options quicker. Ultimately, I arrived at a validation set accuracy of ~76%.

![Model Diagram](https://user-images.githubusercontent.com/17886837/126919949-b3263b0c-d084-4b9a-a0ec-60efa14ada21.PNG)


Only 3 classes comprised 70% of the training data, which was one of the major issues. Another issue was the inconsistency in the training data. Not all images were of similar quality or same size. With more time, I would make a confusion matrix to better understand the error and work on image handling to improve the train and test dataset. Developing a framework to understand the error was challenging, because in theory, the Bayes Error is 0%. There are people who know the typing of every Pokémon, but that's because there are a finite number of Pokémon and that can easily be memorized. On the other hand, the model is tasked with the task of classifying Pokémon it hasn't seen before, which explains the some of the avoidable bias. Although impossible to quantify, the error for experts completing the same task as the model would likely be greater than 0%. For such an arbitrary and meaningless task, it is challenging to put numbers to the type of error present in the model.


# Regression Model Development
The next step is to develop a model that translates images into numerical values, representing the stats of a Pokémon. Starting from scratch by making another convolutional model would require more time doing model development. Instead, the classification model can be turned into an image encoder by removing the SoftMax layer. Then, the processed image encodings would be used to tune a simple sequential model.  The intuition is that layers early in a convolutional network pickup small and individual edges, and as the information propagates, the network develops these into larger scale or more meaningful pieces of information. So, the last dense layer in the classification model has taken the (128, 128, 3) image and distilled it into 512 factors that suffice to describe the original image.


# Output
Putting this all together,  we have a model that takes an image of a Pokémon and predicts its typing and stats. One model handles the image encoding and classification, and the second model leverages the image encoding of the first model to predict its stats.

This project was a good opportunity to get some TensorFlow development under my belt, learn how to webscrape, and do some machine learning model development.
![modleout](https://user-images.githubusercontent.com/17886837/126919976-8c40c498-cd0c-4513-befc-0ef93206179a.PNG)
![ditto](https://user-images.githubusercontent.com/17886837/126919988-ffdfbd56-de3f-4030-a33b-42154c35ead6.PNG)

If you're still here, I'll let you in on a little secret. The project was a just a facade so that I could do this last part.
![Patrick](https://user-images.githubusercontent.com/17886837/131034202-bc436e3e-f01b-482c-bf7c-5b0354de146a.JPEG)
![Capture](https://user-images.githubusercontent.com/17886837/131034526-0b32e685-def3-4e91-a9b1-6089c8a44394.PNG)
