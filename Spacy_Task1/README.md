# Task was to prepare a Name Entity recognition model (using spacy, custom dataset) which can detect food names from text.
## Dataset
### Data preparation
* I am using food data from the USDA's [Branded Food's dataset](https://fdc.nal.usda.gov/download-datasets.html).
* First, I checked for special characters and made all names lower case.
* Then I have collected food names from that file. I preprocessed foods for one, two, and three word name and dropped the others, and duplicates.
* Then I figure out that the difference of data. One word food was 1453 but others are 14022 and 26159.
* To hangle this biasness, I took 1000 two and three words of food name.
* Finally my data was prepared for making the NER sapcy dataset.
### NER spacy dataset
* First, I have collected template for food entities to make a complete sentence for each entities.
* Then for every sentence I have measured the index position of food. And store them as a touple of sentence and index position.
* Finally, I have splited data for train and test and saved as a json file.
## Training
1. I have downloaded pre-trained spacy language model name [en_core_web_lg](https://spacy.io/models/en#en_core_web_lg).
2. Then loaded the json file as train data.
3. Lastly I have trained the model using train data with 30 epoch.
## Evaluating
```
word = nlp("I eat Apple, Banana and Brade in every morning")
for ent in word.ents:
        print(ent.text, ent.label_)
```
*Apple FOOD*<br />
*Banana FOOD*<br />
*Brade FOOD*

## NOTE
All data, model, processing and train method are collected from many different sources of online.
