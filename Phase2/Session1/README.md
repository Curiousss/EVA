
# Implementation of Embedding Layer with fully connected layers:
- Code extracted from http://faculty.neu.edu.cn/yury/AAI/Textbook/Deep%20Learning%20with%20Python.pdf
- Raw IMDB Dataset downloaded from  http://mng.bz/0tIo 
- Precomputed embeddings downloaded from https://nlp.stanford.edu/projects/glove, 2014 English Wikipedia. It’s an 822 MB zip file called glove.6B.zip, containing 100-dimensional embedding vectors for 400,000 words (or nonword tokens)

(Used 2 different notebooks for same with different training sample values. It could have been coded in the 1 notebook using functions.)

The tokenizer found 88582 unique tokens from the IMDB dataset out of 25000 reviews. 

### Results:

1. 200 training samples:

The notebook [Glove_Nlp200.ipynb](Glove_Nlp200.ipynb) trains the model with 200 samples 

![200 samples](nlp200acc.png)
![200 samples](nlp200loss.png)

2. 8000 training samples

The notebook [Glove_Nlp8000.ipynb](Glove_Nlp8000.ipynb) trains the model with 8000 samples 

![8000 samples](nlp8000acc.png)
![8000 samples](nlp8000loss.png)

Notes:
- The model with 200 samples is overfitting with training accuracy reaching 100% and validation accuracy staying at 57.45%.
- The model with 8000 is better but still overfitting with training accuracy reaching 92.21% and validation accuracy reaching 69.67%. The reason is that there is more training data in this case than just 200 samples in the first case.
- The validation loss is oscillating throughout the training in both the cases.

Upload the *.tsv files here http://projector.tensorflow.org/ for embedding projections.
