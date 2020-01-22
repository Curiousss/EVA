
### Implementation of Embedding Layer with fully connected layers:
- Code extracted from http://faculty.neu.edu.cn/yury/AAI/Textbook/Deep%20Learning%20with%20Python.pdf
- Raw IMDB Dataset downloaded from  http://mng.bz/0tIo 
- Precomputed embeddings downloaded from https://nlp.stanford.edu/projects/glove, 2014 English Wikipedia. It’s an 822 MB zip file called glove.6B.zip, containing 100-dimensional embedding vectors for 400,000 words (or nonword tokens)


1. 200 training samples:

The notebook [Glove_Nlp200.ipynb](Glove_Nlp200.ipynb) trains the model with 200 samples 

![200 samples](nlp200acc.png)
![200 samples](nlp200loss.png)

2. 8000 training samples

The notebook [Glove_Nlp8000.ipynb](Glove_Nlp8000.ipynb) trains the model with 8000 samples 

![8000 samples](nlp8000acc.png)
![8000 samples](nlp8000loss.png)

Upload the *.tsv files here http://projector.tensorflow.org/ for embedding projections.
