[![License](http://img.shields.io/:license-apache-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)

# DeLFT 

__Work in progress !__ This is an early alpha version and you most likely don't want to try it at this stage ;) 


DeLFT (Deep Learning Framework for Text) is a Keras framework for text processing, covering sequence labelling (e.g. entity tagging) and text classification (e.g. commenty classification). This library re-implements standard and state-of-the-art Deep Learning architectures which can all be used within the same environment. 

The medium term goal is then to provide good performance (accuracy and runtime) models to a production stack such as Java/Scala and C++. 

DeLFT has been tested with python 3.5, Keras 2.1 and Tensorflow 1.7 as backend. As always, GPU(s) are required for decent training runtime. 

## Sequence Labelling

### Available models

- BidLSTM-CRF with words and characters input following: 

Guillaume Lample, Miguel Ballesteros, Sandeep Subramanian, Kazuya Kawakami, Chris Dyer. "Neural Architectures for Named Entity Recognition". Proceedings of NAACL 2016. https://arxiv.org/abs/1603.01360

<!--
- BidLSTM-CNN with words, characters and custum features input following: 

Jason P. C. Chiu, Eric Nichols. "Named Entity Recognition with Bidirectional LSTM-CNNs". 2016. https://arxiv.org/abs/1511.08308
-->

### Usage

TBD

### Examples

#### NER

Assuming that the usual CoNLL-2003 NER dataset (`eng.train`, `eng.testa`, `eng.testb`) is present under `data/sequenceLabelling/CoNLL-2003/`, for training and evaluating use:

> python3 nerTagger.py train

By default, the BidLSTM-CRF model is used. 

For tagging some text, use the command:

> python3 nerTagger.py tag

#### GROBID models

DeLFT supports GROBID training data (originally for CRF) and GROBID feature matrix to be labelled. 


#### Insult recognition

A small experimental model for recognizing insults in texts, based on the Wikipedia comment from the Kaggle _Wikipedia Toxic Comments_ dataset, English only. This uses a small dataset labelled manually. 

For training:

> python3 insultTagger.py train

By default training uses the whole train set, for n-folds training, which provides better and more stable accuracy, uses: 

> python3 insultTagger.py tag --fold-count 10

#### Creating your own model

As long your task is a sequence labelling of text, adding a new corpus and create an additional model should be straightfoward. If you want to build a model named `toto` based on labelled data in one of the supported format (CoNLL, TEI or GROBID CRF), create the subdirectory `data/sequenceLabelling/toto` and copy your training data under it.  


## Text classification

### Available models



### Usage

TBD

### Examples

#### Toxic comment classification

The dataset of the [Kaggle Toxic Comment Classification challenge](https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge) can be found here: https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/data

This is a multi-label classification problem, where a Wikipedia comment (or any similar short texts) should be associated to 6 possible types of toxicity (`toxic`, `severe_toxic`, `obscene`, `threat`, `insult`, `identity_hate`).

To launch the training: 

> python3 toxicCommentClassifier.py train

For training with n-folds, use the parameter `--fold-count`:

> python3 toxicCommentClassifier.py train --fold-count 10

After training (1 or n-folds), to process the Kaggle test set, use:

> python3 toxicCommentClassifier.py test

To classify a set of comments: 

> python3 toxicCommentClassifier.py classify


#### Twitter 

TBD

#### Citation classification

We use the dataset developed and presented by A. Athar in the following article:

Awais Athar. "Sentiment Analysis of Citations using Sentence Structure-Based Features". Proceedings of the ACL 2011 Student Session, 81-87, 2011. http://www.aclweb.org/anthology/P11-3015

For a given scientific article, the task is to estimate if the occurrence of a bibliographical citation is positive, neutral or negative given its citation context. 


## TODO


__Embeddings__: 

* use a data generator for feeding the models with embeddings, so that embeddings are removed from the models (models are really big because they contain each embeddings matrix for the training vocabulary, it does not make sense to have a set of big and redundant models like that in production), see `model.fit_generator()`

* to free a lot of memory, use serialized embeddings with LMDB, similarly as in https://github.com/kermitt2/nerd/tree/0.0.3 (via the Python package called lmdb,  optionally see also Caffe for storing and using HDF5)

* use OOV (FastText) mechanisms

__Models__:

* Test Theano as alternative backend (waiting for Apache MXNet...)

* augment word vectors with features, in particular layout features generated by GROBID

__NER__:

* benchmark with OntoNores 5 and French NER

__Production stack__:

* see how efficiently feed and execute those Keras models with DL4J

__Build more models and examples__...

## License and contact

Distributed under [Apache 2.0 license](http://www.apache.org/licenses/LICENSE-2.0). 

Contact: Patrice Lopez (<patrice.lopez@science-miner.com>)

