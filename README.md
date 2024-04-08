# SEP-775-Natural-Language-Processing
Final Project 

The project is divided into two parts. We are initially using a sequence-to-sequence model with self-attention using GRU to test a supervised learning approach. Whereas in the second part, we are using an unsupervised learning approach using a transformer-based model. Hence, you will be able to see two different folders with Jupyter notebooks and datasets associated with each approach.


# 1. Supervised Approach: Sequence-to-Sequence Model with Bahdanau Attention

This project implements a sequence-to-sequence model with a Bahdanau attention mechanism for translation tasks. 

## Introduction

Sequence-to-sequence models are a type of neural network architecture that can be used for tasks like machine translation, text summarization, and more. Bahdanau attention is an attention mechanism that allows the model to focus on different parts of the input sequence when generating each part of the output sequence.

This project implements a sequence-to-sequence model with Bahdanau attention using TensorFlow. The model is trained on a dataset of English and Shakespearean sentences to translate Shakespearean sentences to English.

In the code, the encoder is implemented using a recurrent neural network (RNN) with a Gated Recurrent Unit (GRU) cell. The GRU cell processes the input sequence token by token and updates its internal state at each step.Bahdanau attention allows the decoder to focus on different parts of the input sequence dynamically at each time step. It calculates attention weights based on the current decoder state and the encoder outputs. We also experimented with dot product attention but Bahdanau attention mechanism performed well. The decoder takes the context vector produced by the encoder and generates the output sequence token by token. At each time step, the decoder attends to different parts of the input sequence (or context) using an attention mechanism. The training loss decreases steadily over the epochs, indicating effective learning initially. However, towards the end of training, the validation loss begins to increase, suggesting potential overfitting.


## Dependencies

To run this project, you need the following dependencies:

Python 3.x
TensorFlow 2.x
- NumPy
- pandas

To use this project, follow these steps:
(Dataset available in the same folder)
1. Clone the repository:

```bash
git clone https://github.com/yourusername/sequence-to-sequence.git
cd Supervised Learning
```
# 2. Unsupervised Approach: Text Attribute Transfer via Iterative Matching and Translation 

## Introduction

This approach is inspired by the paper IMaT: Unsupervised Text Attribute Transfer via Iterative Matching and Translation, authored by Zhijing Jin, Di Jin, Jonas Mueller, Nicholas Matthews, and Enrico Santus. https://arxiv.org/abs/1901.11333 .
While the paper suggests an approach using a sequence-to-sequence LSTM, we decided to use a transformer-based architecture to train our model. Since then, we have become highly familiar with the advantages of using a transformer over an LSTM-based model. For better results and limited resources, we are using a pre-trained T5-small model so that the model is already trained on an English language corpus and can comprehend the sentence better.

## Explaniation

We decided to go ahead with this unsupervised approach because there is a high scarcity of parallel corpus when it comes to text-style transfer, and that is highly evident from all the research papers that are published in this domain. We are using a Yelp Reviews dataset, which has both positive and negative reviews. 

To summarize the approach, we are initially creating a pseudo-parallel dataset from a non-parallel dataset. This is done by caculating the cosine similarity between the vector embeddings of the positive and negative reviews. The idea will help get review pairs that are talking about the same context. For example, reviews regarding sushi will pair up, but a review about sushi will not pair with a review about pizza.

Once we have created this dataset, after the first iteration, we train our model. Once we get a well-trained model, we pass the dataset through the model to get negative output reviews. If the new review generated by the model has a better Word Movers Distance value as compared to the previous existing pair, we update the dataset and call this step iteration 2. We continue this processing until we get a good parallel dataset and an industry-standard BLEU score.

![image](https://github.com/nidhivanjare/SEP-775-Natural-Language-Processing/assets/55614604/594d3921-eead-4e18-b740-b59d4a8ef7d0)

## Steps to execute

The unsupervised learning folder has three Jupyter notebooks.

1. The data preparation creation script notebook is used to create our first Pusedo parallel dataset. You can directly use the data.xlsx file, as it is the output from our first iteration and contains 843 review pairs.

To access the origin dataset you can use this link: https://drive.google.com/file/d/1sZOKXfgtEidZui5OFSOJcMue0_Np9Y3d/view?usp=sharing

3. The next notebook is positive_negative, which is used to preprocess and clean the initial data input, train the t5-small model with our dataset, save the model, and test the model.

To directly access the trained model after the first iteration, you can access this link: https://drive.google.com/drive/folders/1zXKjhGM86_iigeazRfFoomoPSqVCpclm?usp=share_link

3. Lastly, you can use the positive-negative-iteration2 notebook for iteration 2 of training the model. In this file, we are updating the dataset based on the MDV value from our first model and origin data. We are also cleaning and preprocessing the new data and training a new model on the updated dataset.

You can access the trained model after the second iteration using this link: https://drive.google.com/drive/folders/1SGMqM7VTHvvV5l7DVbc_qqmVlZWCOUQn?usp=share_link

## Results

We can see significant growth as soon as after the first iteration. If we train the model for more iterations, we will be able to generate even better results. We were also able to update 154 rows from the origin dataset after training the first model. This shows that the dataset is also getting updated, and we are getting better positive-negative pairs. 

![image](https://github.com/nidhivanjare/SEP-775-Natural-Language-Processing/assets/55614604/e1352010-7ba2-47d7-8e15-20b360a0955f)

![image](https://github.com/nidhivanjare/SEP-775-Natural-Language-Processing/assets/55614604/3f48118f-cddd-47df-89e4-f95d0eeacc62)











