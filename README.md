Transliteration related data files and/or models.

Contains:
  * Arabic-English transliteration dataset mined from Wikipedia.
  * Trained transliteration modules for Arabic-English, English-Japanese and English-IPA.
  
## The models

The transliteration models provided are recurrent neural networks trained with a [CTC loss](http://www.cs.toronto.edu/~graves/icml_2006.pdf).
For a detailed description of the models, see the [paper](https://arxiv.org/abs/1610.09565).

## Getting the code for loading and training models

If you want to use some of the models provided in this repository you can use [the clstm library](https://github.com/tmbdev/clstm), as provided in the branch [here](https://github.com/mihaelacr-google/clstm/tree/transliteration).

To clone the repository:

```
git clone git@github.com:mihaelacr-google/clstm.git
```

## How to use the trained models 

The binary `clstmfilter` can be used to use an already existing model to transliterate your data.

To build the binary, use the command below. For more on how to install clstm read [this](https://github.com/mihaelacr-google/clstm/tree/transliteration#clstm). You can read more about scons [here](http://scons.org/).

```
scons -j 4
```

For example, if you have a list of Arabic words which you want to transliterate to English, you can run the following commands in your shell:

```
set -a
load="ar2en.clstm"
./clstmfilter your_data.txt

```

## How to train your own models

If you want to train a new model with your data, you can use the `clstmfiltertrain` binary.

To build the binary, run:

```
scons -j 4
```

To train the model:

```
set -a
lr=0.1
./clstmfiltertrain your_train_data.txt your_eval_data.txt

```

## Reproduce our results

If you want to reproduce the results from our paper, you can run:

```
scons -j 4
set -a 
load=ar2en.clstm
with_gt=1
./clstmfilter ar2en-test.txt
```

This will load the one layer Arabic to English model, and produce the character error rate and the word error rate of the model on the test data. You can similary load the 2 layer model and compute the metrics of that model.

