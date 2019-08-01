# posos-challenge

# Table of contents

* [Data](#data)
* [Goals](#goals)
  * [Building a model](#building-a-model)
  * [Serving a model](#serving-a-model)
  * [Building a microservice](#building-a-microservice)
* [Support](#support)
* [Contributing](#contribution)

- - -

## Introduction

The posos challenge builds on some concepts commonly used in the growing field of data science. These concepts walk you through a part of any data driven machine learning project, which include training, serving and exposing a model.

- - -

## Objectives

Data science is much more than developping a model prototype. For industries, it is about implementing machine learning in products and services. For reasearch, it is about bringing machine learning algorithms to solve scientific challenges, and sharing an environment to reproduce the results. In both cases, you have to share your work with people, inside or outside your team. This can become very time consuming for you and very tedious for the others.

We do not expect you to produce a functional project, but to get familiar with the concepts you are not yet used to. Learning efficiently is crucially needed to gain the autonomy required to drive a machine learning project from the collection of data, collected accordingly to scientifics methods, to the production of an evolving interface which can easily be reused and improved.

Whatever the outcome of our meetings, we hope this project will help you for all your future machine learning projects.

- - -

## General instructions

### Rules

- you have to provide an online git repository;
- you must provide two Dockerfiles in the root of the repository:
    - `trainer.Dockerfile`: specify the image to train the model;
    - `api.Dockerfile`: specify the image to expose the model trained by `trainer.Dockerfile`
- you must provide a Makefile in the root of the repository with the following rules:
    - `train`: build the model who will be served
    - `api`: serve the trained model through an api
    - `test`: request the api with test set to get predictions
- you must not push online:
    - your possible credentials
    - the unencrypted dataset

### Dependencies

The following are the only required dependencies you should've installed on your system in order to complete the general instructions :
- [`Git`](https://git-scm.com)
- [`GnuPG`](https://gnupg.org)
- [`Docker`](https://docs.docker.com/) - you should use the [Docker Engine - Community](https://docs.docker.com/install/)


### Data

Data are symetricly encrypted with GPG using a passphrase. To decrypt the file use the following command:
```bash
gpg -d data.tgz.gpg  | tar -xz
```
To get the passphrase, send me an email.

- - -

## Technical part

### Building a model

Building a machine learning model consist, non extensively, into the following parts:
  - split the training data into a train and a validation set;
  - build and train a model on the train set;
  - obtain micro and macro precision, recall and F1 score over the validation set;
  - get a confusion matrix over the valiadtion set
  - export the model in a suitable format to be served

The `train` rule have to build the training image defined in `train.Dockerfile` and run a container in which those steps can be executed.

### Serving a model

- serve the model using a CPU only machine
- 

### Building a microservice

- build a web application - API endpoint `/intent` on port `4002`.

### Test results

- request the api with test set to get predictions
- 

To obtain test results, open an issue with a link to a public repository containing a Docker image.

- - -

## Bonus part

- Use of an hyperparameter optimizer on a fixed validation set;
- Quantify the variability of model performance;
- Web interface to access model inference method.

- - -

## Support

For any help send me an email.

- - -

## Contributing

For any contribution, open an issue so we can talk about it