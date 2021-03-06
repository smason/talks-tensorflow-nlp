# Prerequisites

 * a dataset to be analysed!
 * an idea of what you want to get out of the model

# Aims

1. get tensorflow installed
2. get familiar with tensorflow in an example or two
3. process the data, split into training and test sets
4. initial modelling and plotting of results
5. iterative improvements to above
6. profit!

# 1. Installing Dependencies

Tensorflow is Python based, and I've found these following tools
useful when doing data-science things in Python:

 * Virtualenv: allows multiple versions of libraries to be installed
   in parallel, basically alleviating with "dependency hell"

 * The usual "Scientific Python" toolkit: i.e. run this in a fresh
   `virtualenv`:

   ``` shell
   pip install -U numpy scipy pandas matplotlib jupyter
   ```

   A Jupyter notebook "allows you to create and share documents that
   contain live code, equations, visualizations and narrative text".
   Apparently they even have baked in support for Tensorflow these
   days!

 * Git and Github: working with code in a source control system makes
   the world a better place.

# 2. Sample Tensorflow models

Tensorflow provides a example models and these seem like a good place to
start.  See:

> <https://www.tensorflow.org/get_started/premade_estimators/>

Quite a big repository, so I'd suggest a shallow clone (still ~360MB),
and then proceed as suggested above:

``` shell
git clone --depth 10 https://github.com/tensorflow/models.git
cd models/samples/core/get_started/
python premade_estimator.py
```

# 3. My dataset

The problem we want to solve is automatically classifying a telephone
conversation between two NHS health professionals.  Because this is
pretty sensitive I'm going to be working with a similar "open dataset"
in this example.  I found the following subreddit useful for finding
some data to play with:

> <https://www.reddit.com/r/datasets/>

I'm starting with the [Cornell Movie-Dialogs Corpus].  Mostly because
this is conversational data and it includes a set of genres that we
can predict from the conversations.

[Cornell Movie-Dialogs Corpus]: http://www.cs.cornell.edu/~cristian/Cornell_Movie-Dialogs_Corpus.html

As is the case with most data, the people producing it have invented
their own weird, wonderful and idiosyncratic file format.  They use a
delimiter separated file format, like CSV, but use a delimiter of `
+++$+++ ` for some weird reason.  They also include various fields
containing a JSON-like "array of strings"---but of course it's invalid
JSON and this needs to be munged before any standard JSON parser will
touch it.

That said, it's pretty easy to coerce `pandas` into handling these
files and end up with a mostly conventional set of `DataFrame`s.
