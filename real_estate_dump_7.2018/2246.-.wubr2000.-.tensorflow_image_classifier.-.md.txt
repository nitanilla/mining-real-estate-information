Real Estate Image Classifer using Tensorflow
===========================

## Introduction

I followed [this O'Reilly tutorial](https://www.oreilly.com/learning/tensorflow-for-poets) to train an image classifier for real estate photos using Tensorflow.

The first version of the model is based on Inception trained with ImageNet photos. I've retrained the final layer with a set of real estate images that have nine different labels (bathroom, bedroom, closet, dining room, etc). The overal accuracy of the first version is 84.6%.

## Steps for Retraining Inception for Real Estate Images

Follow instructions in [this tutorial](https://www.oreilly.com/learning/tensorflow-for-poets) and set up real estate photos in `tf_files` directory (with categories already labeled) as instructed.

Load `Docker Quickstart Terminal` app and use iTerm as terminal.

```
$ docker run -it -v $HOME/tf_files:/tf_files b.gcr.io/tensorflow/tensorflow:latest-devel
```

Updating the code…(this is apain - have to do it every time). Pulling the code requires a default email address, which you can set to anything, since we’re not planning on pushing any changes back.

```
$ git config --global user.email "you@example.com"
$ git config --global user.name "Your Name"
```

Now you should be able to pull the latest source code.

```
$ cd /tensorflow/
$ git pull origin master
```

error...

```
$ git commit -a
$ git pull origin master
```

**THIS IS VERY IMPORTANT:** You should now have fully up-to-date code. We want to sync it to a version we know works, though, so we’ll run this command:

```
$ git checkout 6d46c0b370836698a3195a6d73398f15fa44bcb2
```

Now build the code:

```
$ cd /tensorflow/
$ bazel build -c opt --copt=-mavx tensorflow/examples/image_retraining:retrain
```

Running the code (or some version of below with different parameters):

```
$ bazel-bin/tensorflow/examples/image_retraining/retrain \
--bottleneck_dir=/tf_files/home_bottlenecks \
--model_dir=/tf_files/inception \
--output_graph=/tf_files/home_graph.pb \
--output_labels=/tf_files/home_labels.txt \
--image_dir /tf_files/home_photos
```

The model is saved as a protobuf file (in this case `home_graph.pb`) and training label names are saved as a text file (`home_labels.txt`). Here is a version of the training model with different learning rate and batch size:

```
$ bazel-bin/tensorflow/examples/image_retraining/retrain \
--bottleneck_dir=/tf_files/home_bottlenecks_3 \
--model_dir=/tf_files/inception \
--output_graph=/tf_files/home_graph_4.pb \
--output_labels=/tf_files/home_labels_4.txt \
--image_dir /tf_files/home_photos \
--learning_rate 0.001 \
--training_batch_size 200
```

## Future Improvements
1. Using other topologies: e.g. VGGNet, MXNet (which are better for localized images)
2. Using other base training datasets: e.g. MIT Places dataset (better for location, architecture, room images)
3. Tweaking model hyperparameters (e.g. learning rate, training batch size), input distortions (to make training more robust), size of training/test set (control for overfitting).
