# Bert-ARC-Challenge
The project just tries to get BERT answer a subset of ARC challenge questions. 
See the ipynb file for the project 
[Arc challenge solver](https://nbviewer.jupyter.org/github/tanishkasingh9/Bert-ARC-Challenge/blob/master/All_Arc.ipynb)

**Objective** : Perform semantic parsing on the [ARC dataset](http://data.allenai.org/arc/) and do the question answering task.  We have chosen to focus on a subset of the ARC dataset mainly questions that ask to `find an example of`. For this set of questions we obtained relevant sentences, which were fetched using an IR system. 

## Pre-processing performed on the dataset:
Stemming and Stop-word removal
Steps we performed to create the file.
1. Make the number and  choices consistent. This meant for the few examples which had options as  `(1), (2), (3), (4)` we transformed them to `(A), (B), (C), (D)`. Another thing we found was for a varying option numbers, for example the number of options was 5 instead of 4. These few questions we replaced option `(D)` with option `(E)`.
2. Next we split the question-option to a question and four choices.
3. Finally all easy, challenge, train, dev, and test examples were all  put to one file. 

## Dataset and DataLoaders used:
Datasets and Dataloaders are basically data iterators that pytorch provides us to iterate on the data. Dataloaders provides additional benefits of shuffling, sampling the data, and mostly importantly batching data. So next we created train, dev and test datasets first, and then their respective dataloaders.

 BERT Model, Tokenizer and Vocabulary: [bert-base-uncased](https://s3.amazonaws.com/models.huggingface.co/bert/bert-base-uncased-vocab.txt)
 
 |Experiment details                     | Train Acc | Train loss | Dev Acc | Dev loss | Test Acc | Test loss |Num Epochs | remarks |
|--------------------------------------------|:---------------:|:--------------:|:------------:|:-------------:|:-------------:|:--------------:|:-------------------:|--------------:|
| ARC challenge **without corpus**|  0.259 | 1.386 | 0.262 | 1.386 | 0.254 | 1.386 | 3 | LR : 5e-5|
| ARC challenge **with corpus**| 0.242 | 1.392 | 0.274 | 1.386 | 0.245 | 1.386 | 3 | LR :  5e-5|
| ARC challenge **without corpus**| 0.391 | 1.309 | 0.679 | 1.120 | 0.317 | 1.388 | 3 | LR : 5e-6 | 
| ARC challenge **with corpus**|**0.432** | **1.258** |**0.718** | **0.956** | **0.317** | **1.376** | 3 | **LR : 5e-6**|
| ARC easy **without corpus** | 0.605 | 0.990 | 0.802 | 0.645 | 0.500 | 1.227 | 3 | LR : 5e-6|

* Train set challenge size : 1119
* Dev set challenge size : 299
* Test set challenge size : 1172
* Optimizer : BertAdam (Huggingface)
* Learning Rate : 5e-6 performs better than 5e-5, in which case the model does not learn anything

These accuracy values do not look particularly good. 

