---
layout: default
img: ios_keyboard.png
caption: Movie quotes according to autocomplete
img_link: https://www.explainxkcd.com/wiki/index.php/1427:_iOS_Keyboard
title: Homework 5 - Character-based Language Models
active_tab: homework
release_date: 2018-02-07
due_date: 2018-02-14T11:00:00EST
attribution: This assignment is based on [The Unreasonable Effectiveness of Character-level Language Models](http://nbviewer.jupyter.org/gist/yoavg/d76121dfde2618422139) by Yoav Goldberg. Daphne Ippolito, John Hewitt, and Chris Callison-Burch adapted their work into a homework assignment for UPenn's CIS 530 class in Spring 2018.  
readings:
-
   title: Language Modeling with N-grams
   authors: Dan Jurafsky and James H. Martin
   venue: Speech and Language Processing (3rd edition draft)
   type: textbook
   url: https://web.stanford.edu/~jurafsky/slp3/4.pdf
-
   title: The Unreasonable Effectiveness of Character-level Language Models
   authors: Yoav Goldberg
   venue: Response to Andrej Karpathy's blog post.
   type: blog
   year: 2015	
   url: http://nbviewer.jupyter.org/gist/yoavg/d76121dfde2618422139
-
   title: Language Independent Authorship Attribution using Character Level Language Models
   authors: Fuchun Pen, Dale Schuurmans, Vlado Keselj, Shaojun Wan
   type: conference
   year: 2003
   venue: EACL
   url: http://www.aclweb.org/anthology/E/E03/E03-1053.pdf
---

<!-- Check whether the assignment is up to date -->
{% capture this_year %}{{'now' | date: '%Y'}}{% endcapture %}
{% capture due_year %}{{page.due_date | date: '%Y'}}{% endcapture %}
{% if this_year != due_year %} 
<div class="alert alert-danger">
Warning: this assignment is out of date.  It may still need to be updated for this year's class.  Check with your instructor before you start working on this assignment.
</div>
{% endif %}
<!-- End of check whether the assignment is up to date -->

<div class="alert alert-info">
This assignment is due before {{ page.due_date | date: "%I:%M%p" }} on {{ page.due_date | date: "%A, %B %-d, %Y" }}.
</div>


Character-based Language Models <span class="text-muted">: Assignment 5</span>
=============================================================

In the textbook, language modeling was defined as the task of predicting the next word in a sequence given the previous words. In this assignment, we will focus on the related problem of predicting the next *character* in a sequence given the previous characters. 

The learning goals of this assignment are to: 
* Understand how to compute language model probabilities using maximum likelihood estimation
* Implement basic smoothing, back-off and interpolation.
* Have fun using a language model to probabilistically generate texts.
* Use a set of language models to perform text classification. 


<div class="alert alert-info" markdown="1">
Here are the materials that you should download for this assignment:
* [Skeleton python code](downloads/hw5/language_model.py).
* [training data for text classification task](downloads/hw5/cities_train.zip).
* [dev data for text classification task](downloads/hw5/cities_val.zip).
* [test file for leaderboard](downloads/hw5/cities_test.txt)
</div>


## Part 1: Unsmoothed Maximum Likelihood Character-Level Language Models 

We're going to be starting with some [nice, compact code for character-level language models](http://nbviewer.jupyter.org/gist/yoavg/d76121dfde2618422139). that was written by [Yoav Goldberg](http://u.cs.biu.ac.il/~yogo/).  Below is Yoav's code for training a language model.

<div class="alert alert-warning" markdown="1">
Note: all of this code is included in the provided code stub called `language_model.py`. No need to copy and paste.
</div>


### Train a language model

Note: we provide you this code in the Python [stub file](downloads/hw5/language_model.py).

{% highlight python %}
def train_char_lm(fname, order=4, add_k=1):
  ''' Trains a language model.
  This code was borrowed from 
  http://nbviewer.jupyter.org/gist/yoavg/d76121dfde2618422139
  Inputs:
    fname: Path to a text corpus.
    order: The length of the n-grams.
    add_k: k value for add-k smoothing. NOT YET IMPLMENTED
  Returns:
    A dictionary mapping from n-grams of length n to a list of tuples.
    Each tuple consists of a possible net character and its probability.
  '''

  # TODO: Add your implementation of add-k smoothing.

  data = open(fname).read()
  lm = defaultdict(Counter)
  pad = "~" * order
  data = pad + data
  for i in range(len(data)-order):
    history, char = data[i:i+order], data[i+order]
    lm[history][char]+=1
  def normalize(counter):
    s = float(sum(counter.values()))
    return [(c,cnt/s) for c,cnt in counter.items()]
  outlm = {hist:normalize(chars) for hist, chars in lm.items()}
  return outlm
{% endhighlight %}

`fname` is a file to read the characters from. `order` is the history size to consult. Note that we pad the data with leading `~` so that we also learn how to start.


Now you can train a language model.  First grab some text like this corpus of Shakespeare:

``` bash
$ wget http://cs.stanford.edu/people/karpathy/char-rnn/shakespeare_input.txt`
```

Now train the model:
{% highlight python %}
lm = train_char_lm("shakespeare_input.txt", order=4)
{% endhighlight %}

### P(hello world) 

Ok. Now we can look-up the probability of the next letter given some history.  Here are some example queries:

{% highlight python %}
>>> lm['hell']
[('!', 0.06912442396313365), (' ', 0.22119815668202766), ("'", 0.018433179723502304), ('i', 0.03225806451612903), ('\n', 0.018433179723502304), ('-', 0.059907834101382486), (',', 0.20276497695852536), ('o', 0.15668202764976957), ('.', 0.1336405529953917), ('s', 0.009216589861751152), (';', 0.027649769585253458), (':', 0.018433179723502304), ('?', 0.03225806451612903)]
{% endhighlight %}

Actually, let's pretty print the output, and sort the letters based on their probabilities.

{% highlight python %}
import pprint
import operator

def print_probs(lm, history):
    probs = sorted(lm[history],key=lambda x:(-x[1],x[0]))
    pp = pprint.PrettyPrinter()
    pp.pprint(probs)
{% endhighlight %}

OK, print again:

{% highlight python %}
>>> print_probs(lm, "hell")
[(' ', 0.22119815668202766),
 (',', 0.20276497695852536),
 ('o', 0.15668202764976957),
 ('.', 0.1336405529953917),
 ('!', 0.06912442396313365),
 ('-', 0.059907834101382486),
 ('?', 0.03225806451612903),
 ('i', 0.03225806451612903),
 (';', 0.027649769585253458),
 ('\n', 0.018433179723502304),
 ("'", 0.018433179723502304),
 (':', 0.018433179723502304),
 ('s', 0.009216589861751152)]
{% endhighlight %}

This means that `hell` can be followed by any of these dozen characters: 

` ,o.!-?i;\n':s` 

and that the probability of `o` given `hell` is 15.7%, $$p(o \mid hell)=0.157$$.  The most probable character to see after `hell` is a space, $$p(o \mid hell)=0.221$$.

The distribution of letters that occur after `worl` is different than the distribution of letters that occur after `hell`.  Here is that distribution: 

{% highlight python %}
>>> print_probs(lm, "worl")
[('d', 1.0)]
{% endhighlight %}

What does that mean?  It means that in our corpus, the only possible continuation that we observed for `worl` was the letter `d`, and we assign 100% of probability mass to it, $$p(d \mid worl)=1.0$$.

### Let's write some Shakespeare!

Generating text with the model is simple. To generate a letter, we will look up the last `n` characters, and then sample a random letter based on the probability distribution for those letters.   Here's Yoav's code for that:

{% highlight python %}
def generate_letter(lm, history, order):
  ''' Randomly chooses the next letter using the language model.
  
  Inputs:
    lm: The output from calling train_char_lm.
    history: A sequence of text at least 'order' long.
    order: The length of the n-grams in the language model.
    
  Returns: 
    A letter
  '''
  
  history = history[-order:]
  dist = lm[history]
  x = random()
  for c,v in dist:
    x = x - v
    if x <= 0: return c
{% endhighlight %}

To generate a passage of text, we just seed it with the initial history and run letter generation in a loop, updating the history at each turn.  We'll stop generating after a specified number of letters.

{% highlight python %}
def generate_text(lm, order, nletters=500):
  '''Generates a bunch of random text based on the language model.
  
  Inputs:
  lm: The output from calling train_char_lm.
  order: The length of the n-grams in the language model.
  nletters: the number of characters worth of text to generate
  
  Returns: 
    A letter  
  '''
  history = "~" * order
  out = []
  for i in range(nletters):
    c = generate_letter(lm, history, order)
    history = history[-order:] + c
    out.append(c)
  return "".join(out)
{% endhighlight %}

Now, try generating some Shakespeare with different order n-gram models.  You should try running the following commands.  

{% highlight python %}
>>> lm = train_char_lm("shakespeare_input.txt", order=2)
>>> print(generate_text(lm, 2))


>>> lm = train_char_lm("shakespeare_input.txt", order=3)
>>> print(generate_text(lm, 3))


>>> lm = train_char_lm("shakespeare_input.txt", order=4)
>>> print(generate_text(lm, 4))


>>> lm = train_char_lm("shakespeare_input.txt", order=7)
>>> print(generate_text(lm, 7))
{% endhighlight %}

What do you think?  Is it as good as [1000 monkeys working at 1000 typewriters](https://www.youtube.com/watch?v=no_elVGGgW8)?

### What the F?

Try generating a bunch of short passages:


{% highlight python %}
>>> print(generate_text(lm, 5, 40))
First, and quence
Shall we gave it. Now
>>> print(generate_text(lm, 5, 40))
First die.

KING OF FRANCE:
I prithee, 
>>> print(generate_text(lm, 5, 40))
First marriage,
And scarce it: wretches 
>>> print(generate_text(lm, 5, 40))
First, the midsummer;
We make us allia s
>>> print(generate_text(lm, 5, 40))
First choose
Which now,
Where like thee.

>>> lm = train_char_lm("shakespeare_input.txt", order=4)
>>> print(generate_text(lm, 4, 40))
First blood
assurance
To grace and leade
>>> print(generate_text(lm, 4, 40))
First, are almightly,
Am I to bedew the 
>>> print(generate_text(lm, 4, 40))
First Senato, come unexamination hast br

>>> lm = train_char_lm("shakespeare_input.txt", order=2)
>>> print(generate_text(lm, 2, 40))
Firm
Histed mor ituffe bonguis hon tract
>>> print(generate_text(lm, 2, 40))
Fir my fat,
Forromfor intre You to lor c

{% endhighlight %}

Do you notice anything?  *They all start with F!*  In fact, after we hit a certain order, the first word is always *First*?  Why is that?  Is the model trying to be clever?  First, generate the word *First*. Explain what is going on in your writeup.


## Part 2: Perplexity, smoothing, back-off and interpolation  

In this part of the assignment, you'll adapt Yoav's code in order to implement several of the  techniques described in [Section 4.2 of the Jurafsky and Martin textbook](https://web.stanford.edu/~jurafsky/slp3/4.pdf).  

### Perplexity 

How do we know whether a LM is good? There are two basic approaches:
1. Task-based evaluation (also known as extrinsic evaluation), where we use the LM as part of some other task, like automatic speech recognition, or spelling correcktion, or an OCR system that tries to covert a professor's messy handwriting into text. 
2. Intrinsic evaluation.  Intrinsic evaluation tries to directly evalute the goodness of the language model by seeing how well the probability distributions that it estimates are able to explain some previously unseen test set. 

Here's what the textbook says:

> For an intrinsic evaluation of a language model we need a test set. As with many of the statistical models in our field, the probabilities of an N-gram model come from the corpus it is trained on, the training set or training corpus. We can then measure the quality of an N-gram model by its performance on some unseen data called the test set or test corpus. We will also sometimes call test sets and other datasets that are not in our training sets held out corpora because we hold them out from the training data.

> So if we are given a corpus of text and want to compare two different N-gram models, we divide the data into training and test sets, train the parameters of both models on the training set, and then compare how well the two trained models fit the test set.

> But what does it mean to "fit the test set"? The answer is simple: whichever model assigns a higher probability to the test set is a better model.

We'll implement the most common method for intrinsic metric of language models: *perplexity*.  The perplexity of a language model on a test set is the inverse probability of the test set, normalized by the number of words. For a test set $$W = w_1 w_2 ... w_N$$:


$$Perplexity(W) = P(w_1 w_2 ... w_N)^{-\frac{1}{N}}$$


$$ = \sqrt[N]{\frac{1}{P(w_1 w_2 ... w_N)}}$$


$$ = \sqrt[N]{\prod_{i=1}^{N}{\frac{1}{P(w_i \mid w_1 ... w_{i-1})}}}$$


OK - let's implement it. Here's a possible function signature for perplexity.  (We might update it during class on Wednesday).  Give it a go. 

{% highlight python %}
def perplexity(test_filename, lm, order=4):
  '''Computes the perplexity of a text file given the language model.
  
  Inputs:
    test_filename: path to text file
    lm: The output from calling train_char_lm.
    order: The length of the n-grams in the language model.
  '''
  test = open(test_filename).read()
  pad = "~" * order
  test = pad + data
  
  # TODO: YOUR CODE HERE
{% endhighlight %}


A couple of things to keep in mind:

1. Remember to pad the front of the file
2. Numeric underflow is going to be a problem, so consider using logs.
3. Perplexity is undefined if LM assigns any zero probabilities to the test set. In that case your code should return positive infinity - `float("inf")`.
4. On your unsmoothed models, you'll definitely get some zero probabilities for the test set.  To test you code, you should try computing perplexity on the trianing set, and you should compute perplexity for your LMs that use smoothing and interpolation.


#### In your report:
Discuss the perplexity for text that is similar and different from Shakespeare's plays. We provide you [two dev text files](downloads/hw5/test_data.zip), a New York Times article and several of Shakespeare's sonnets, but feel free to experiment with your own text.

Note: you may want to create a smoothed language model before calculating perplexity, otherwise you will get a perplexity of 0.

### Laplace Smoothing and Add-k Smoothing 

Laplace Smoothing is described in section 4.4.1.  Laplace smoothing  adds one to each count (hence its alternate name *add-one smoothing*).   Since there are *V* words in the vocabulary and each one was incremented, we also need to adjust the denominator to take into account the extra V observations.

$$P_{Laplace}(w_i) = \frac{count_i + 1}{N+V}$$

A variant of Laplace smoothing is called *Add-k smoothing* or *Add-epsilon smoothing*.  This is described in section Add-k 4.4.2.  Let's change the function definition of `train_char_lm` so that it takes a new argument, `add_k`, which specifies how much to add.  By default, we'll set it to one, so that it acts like Laplace smoothing:

{% highlight python %}
def train_char_lm(fname, order=4, add_k=1):
    # Your code here...
{% endhighlight %}

### Interpolation

Next, let's implement interpolation.  The idea here is to calculate the higher order n-gram probabilities also combining the probabilities for lower-order n-gram models.  Like smoothing, this helps us avoid the problem of zeros if we haven't observed the longer sequence in our training data.  Here's the math:

$$P_{backoff}(w_i|w_{i−2} w_{i−1}) = \lambda_1 P(w_i|w_{i−2} w_{i−1}) + \lambda_2 P(w_i|w_{i−1}) + \lambda_3 P(w_i)$$

where $\lambda_1 + \lambda_2 + \lambda_3 = 1$.


Now, write a back-off function:

{% highlight python %}
def calculate_prob_with_backoff(char, history, lms, lambdas):
  '''Uses interpolation to compute the probability of char given a series of 
     language models trained with different length n-grams.

   Inputs:
     char: Character to compute the probability of.
     history: A sequence of previous text.
     lms: A list of language models, outputted by calling train_char_lm.
     lambdas: A list of weights for each lambda model. These should sum to 1.
    
  Returns:
    Probability of char appearing next in the sequence.
  ''' 
  # TODO: YOUR CODE HERE
  pass
{% endhighlight %}

You should also write a helper function to set the lambdas.  Here's a function definition that gives you access to a development set.  You can also experiment with setting them manually. 

{% highlight python %}
# returns a list of lambda values that weight the contribution of n-gram model
def set_lambdas(lms, dev_filename):
  '''Returns a list of lambda values that weight the contribution of each n-gram model

  This can either be done heuristically or by using a development set.

  Inputs:
    lms: A list of language models, outputted by calling train_char_lm.
    dev_filename: Path to a development text file to optionally use for tuning the lmabdas. 

  Returns:
    Probability of char appearing next in the sequence.
  '''
  # TODO: YOUR CODE HERE
  pass
{% endhighlight %}

#### In your report:
Experiment with a couple different lambdas and values of k, and discuss their effects.

## Part 3: Text Classification using LMs

Language models can be applied to text classification. If we want to classify a text $$D$$ into a category $$c \in C={c_1, ..., c_N}$$. We can pick the category $$c$$ that has the largest posterior probability given the text. That is,

$$ c^* = arg max_{c \in C} P(c|D) $$

Using Bayes rule, this can be rewritten as:

$$ c^* = arg max_{c \in C} P(D|c) P(c)$$

If we assume that all classes are equally likely, then we can just drop the $$P(c)$$ term:

$$ = arg max_{c \in C} P(D|c)$$

Here $$P(D \mid c)$$ is the likelihood of $$D$$ under category $$c$$, which can be computed by training language models for all texts associated with category $$c$$.  This technique of text classification is drawn from [literature on authorship identification](http://www.aclweb.org/anthology/E/E03/E03-1053.pdf), where the approach is to learn a separate language model for each author, by training on a data set from that author. Then, to categorize a new text D, they use each language model to calculate the likelihood of D under that model, and pick the  category that assigns the highest probability to D.

Try it!  We have provided you training and validation datsets consisting of the names of cities. The task is to predict the country a city is in. The following countries are including in the dataset.
```
af	Afghanistan
cn	China
de	Germany
fi	Finland
fr	France
in	India
ir	Iran
pk	Pakistan
za	South Africa
```


**Leaderboard**

We'll set up a leaderboard for the text classification task.  Your job is to configure a set of language models that perform the best on the text classification task. We will use the city names dataset, which you should have already downloaded. The test set has one unlabeled city name per line. Your code should output a file `labels.txt` with one two-letter country code per line.

In next week's assignment, you will use a recurrent neural network on the same dataset in order to compare performance. 

#### In your report:
Describe the parameters of your final leaderboard model and any experimentation you did before settling on it.



## Deliverables
<div class="alert alert-warning" markdown="1">
Here are the deliverables that you will need to submit:
* writeup.pdf
* code (.zip). It should be written in Python 3 and include a README.txt briefly explaining how to run it.
* `labels.txt` predictions for leaderboard.
</div>

## Recommended readings

<table>
   {% for publication in page.readings %}
    <tr>
      <td>
	{% if publication.url %}
		<a href="{{ publication.url }}">{{ publication.title }}.</a>
        {% else %}
		{{ publication.title }}.
	{% endif %}
	{{ publication.authors }}.
	{{ publication.venue }}  {{ publication.year }}.

	{% if publication.abstract %}
	<!-- abstract button -->
	<a data-toggle="modal" href="#{{publication.id}}-abstract" class="label label-success">Abstract</a>
	<!-- /.abstract button -->
	<!-- abstract content -->
	<div id="{{publication.id}}-abstract" class="modal fade" tabindex="-1" role="dialog" aria-labelledby="{{publication.id}}">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
          <h4 class="modal-title" id="{{publication.id}}">{{publication.title}}</h4>
        </div><!-- /.modal-header -->
        <div class="modal-body">
        {{publication.abstract}}
        </div><!-- /.modal-body -->
	</div><!-- /.modal-content -->
	</div><!-- /.modal-dialog -->
	</div><!-- /.abstract-content -->
	{% endif %}
		{% if publication.bibtex %}
	<!-- bibtex button -->
	<a data-toggle="modal" href="#{{publication.id}}-bibtex" class="label label-default">BibTex</a>
	<!-- /.bibtex button -->
	<!-- bibtex content -->
	<div id="{{publication.id}}-bibtex" class="modal fade" tabindex="-1" role="dialog" aria-labelledby="{{publication.id}}">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
          <h4 class="modal-title" id="{{publication.id}}">{{publication.title}}</h4>
        </div><!-- /.modal-header -->
        <div class="modal-body">
 	   <pre>{{publication.bibtex}}
           </pre>
        </div><!-- /.modal-body -->
	</div><!-- /.modal-content -->
	</div><!-- /.modal-dialog -->
	</div><!-- /.bibtex-content -->
	{% endif %}
</td></tr>
  {% endfor %}
</table>
