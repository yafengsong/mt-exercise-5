# MT Exercise 5: Byte Pair Encoding, Beam Search
This repository is a starting point for the 5th and final exercise. As before, fork this repo to your own account and the clone it into your prefered directory.

## Requirements

- This only works on a Unix-like system, with bash available.
- Python 3 must be installed on your system, i.e. the command `python3` must be available
- Make sure virtualenv is installed on your system. To install, e.g.

    `pip install virtualenv`

## Steps

Clone your fork of this repository in the desired place:

    git clone https://github.com/[your-name]/mt-exercise-5

Create a new virtualenv that uses Python 3.10. Please make sure to run this command outside of any virtual Python environment:

    ./scripts/make_virtualenv.sh

**Important**: Then activate the env by executing the `source` command that is output by the shell script above.

Download and install required software as described in the exercise pdf.

Download data:

    ./download_iwslt_2017_data.sh
    
Before executing any further steps, you need to make the modifications described in the exercise pdf.

Train a model:

    ./scripts/train.sh

The training process can be interrupted at any time, and the best checkpoint will always be saved.

Evaluate a trained model with 

    ./scripts/evaluate.sh

## Models
1. word_level_transformer
2. bpe_level_transformer
3. bpe_level_transformer2

## Comments
I choose the translation direction from Italian to English. I build, train, and evaluate the model as following steps:
1.  Sub-sample the training data to 100K sentences
2.  Use JoeyNMT to train the word level model, setting the vocabulary size=2000
3.  Generate BPE vocabulary with the size of 2K and 3K respectively
4.  Use JoeyNMT to train 2 BPE level model respectively
5.  Evaluate the BLEU score of these three models as follows:
 **null** | **use BPE** | **vol size** | **BLEU** 
----------|-------------|--------------|----------
 **(a)**  | no          | 2000         | 7.1      
 **(b)**  | yes         | 2000         | 6.5      
 **(c)**  | yes         | 3000         | 4.9      
