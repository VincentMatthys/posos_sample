# posos_sample

## Introduction

This repo builds on some concepts commonly used in the growing field of data science. These concepts walk you through a part of any data driven machine learning project, which include training, serving and exposing a model.

## Table of contents

* [Objectives](#objectives)
* [General instructions](#general-instructions)
  * [Rules](#rules)
  * [Dependencies](#dependencies)
  * [Data](#data)
* [Technical part](#technical-part)
  * [Building a model](#building-a-model)
  * [Serving a model as a microservice](#serving-a-model-as-a-microservice)
* [Key concepts](#key-concepts)
  * [Makefile](#makefile)
  * [Docker](#docker)
* [Bonus part](#bonus-part)
* [How to get help](#how-to-get-help)
* [Contributing](#contributing)

- - -

## Objectives

Data science is much more than developping a model prototype. For industries, it is about implementing machine learning in products and services. For research, it is about bringing machine learning algorithms to solve scientific challenges, and sharing an environment to reproduce the results. In both cases, you have to share your work with people, inside or outside your team. This can become very time consuming for you and very tedious for the others.

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
- you must not push online:
    - your possible credentials
    - the unencrypted dataset

### Dependencies

The only required dependencies you should've installed on your system in order to complete the general instructions :
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

The built model should be built with:
  - an encoder part, which produces a vector representation of the input text. To build this encoder part, you can start with a TF IDF encoder, or use a neural encoder;
  - a decoder part, which consists here of a classifier. You may want to start with SVM and then use a neural decoder.

The `train` rule have to build the training image defined in `train.Dockerfile` and run a container in which those steps are executed.

### Serving a model as a microservice

To integrate the model into a larger applicaiton in some way, 

- serve the model using a CPU only machine;
- build a web application - endpoint - using route `/intent` on port `4002` - to use the served model as a microservice;
- the endpoint should return a json response whos format is specified at the end of the section;

A functional approach is to build a model server. This is an application to manage and serve models, which allow to serve multiple versions of a same model and get distinct inferences for each version. You can find more details of the way that tensorflow works to put model into production [here](https://www.tensorflow.org/tfx/serving/serving_basic), using a model server available as a [docker image](https://hub.docker.com/r/tensorflow/serving).

The `api` rule have to take the exported model from the `train` rule and start a microservice as a container defined in an `api.Dockerfile` image.

Once the microservice has been started, you should be abble to request it using the following command:
```bash
curl -G "http://localhost:4002/intent" --data-urlencode "query=risques poisson cru pendant la grossesse ?" | jq
```
And get the following response format:
```json
{
    "intent": 26,
    "probability": "0.73356545"
}
```

### Testing the project

A working project should be abble to serve a model through a local API using the following commands:
```bash
make train; make api
```
And get response from:
```
curl -G "http://localhost:4002/intent" --data-urlencode "query=risques poisson cru pendant la grossesse ?" | jq
```

- - -

## Key concepts

### Makefile

Makefile based on [GNU Make](https://www.gnu.org/software/make/) provides command to automate common tasks. 

The documentation can be found [online](https://www.gnu.org/software/make/manual/make.html).

> Make enables the end user to build and install your package without knowing the details of how that is done -- because these details are recorded in the makefile that you supply.

> Make is not limited to any particular language. For each non-source file in the program, the makefile specifies the shell commands to compute it. These shell commands can run a compiler to produce an object file, the linker to produce an executable, ar to update a library, or TeX or Makeinfo to format documentation

Examples of Makefiles can be found in [examples directory](/examples/makefile)

### Docker

Docker introduces two concepts:
- an image
- a container

The documentation can be found [online](https://docs.docker.com/get-started/).

> A container is launched by running an image. An image is an executable package that includes everything needed to run an application--the code, a runtime, libraries, environment variables, and configuration files.

> A container is a runtime instance of an image--what the image becomes in memory when executed (that is, an image with state, or a user process). You can see a list of your running containers with the command, `docker ps`.

Examples of docker images can be found in [examples directory](/examples/docker).


- - -

## Bonus part

- Implement a `test` in your Makefile to request the api with the provided test set to get predictions in a `(ID,question,intent)` format saved to a `predictions.csv` file in the root of your repository;
- Use of an hyperparameter optimizer on a fixed validation set;
- Quantify the variability of model performance;
- Build a web interface for the API.

- - -

## How to get help

For any help send me an email.

- - -

## Contributing

For any contribution, open an issue so we can talk about it.
