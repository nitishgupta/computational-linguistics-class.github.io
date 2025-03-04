---
layout: default
img: estimating_time.png
caption: Don't Panic
img_link: https://xkcd.com/1658/   
title: The Term Project
active_tab: homework
release_date: 2018-03-01
due_date: 2018-04-25T12:00:00EST
attribution: This assignment was developed by the CIS 530 course staff.
deliverables:
    -
      description: Milestone 1 - Form a team and submit three project ideas
      due_date: 2018-03-14T11:00:00EST
    -
      description: Milestone 2 - Collect your data, and write an evalation script and a simple baseline
      due_date: 2018-03-28T11:00:00EST
    -
      description: Milestone 3 - Implement a published baseline
      due_date: 2018-04-11T11:00:00EST
    -
      description: Milestone 4 -  Prepare a final project presentation, and create a write-up in the style of a homework assignment.  Finish one of your extensions the public baseline (no late days allowed for this Milestone).
      due_date: 2018-04-18T11:00:00EST
    -
      description: Vote on your favorite projects from the class
      due_date: 2018-04-18T12:00:00EST
    -
      description: Milestone 5 - Finish all your extensions to the public baseline, and submit your final project writeup.
      due_date: 2018-04-25T12:00:00EST
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

Term Project <span class="text-muted">: Overview</span>
============


Your term project is to design a project similar to the homework assigments you have completed
in this class. Your final project will consist of the following components:

1. A description of the problem, in the style and format of the homework assignment descriptions.
1. Training and evaluation data.
1. A commented implementation of the simplest possible solution to the problem.  For instance, this could be a majority class baseline or a random baseline. 
1. A commented implementation of a baseline published in the literature, along with
   skeleton code obtained by removing the parts that students should implement.
1. One extension per team member that attempts to improve on the baseline, along
   with a brief (one- to three-paragraph) accompanying write-up for each extension
   describing the general approach and whether it worked.
1. A evaluation script that can be used to score
   submissions like on the class leaderboard. The output of any model
   implementations should be gradeable with this program.

We'll vote on the best projects, and the best ones will be available for ther students to complete as an optional final homework assignment.

We're going to split up the work on the term project into several deliverables, each with their own due dates.  You don't have to wait to start working on each part of the project.  We encourage you to begin work early, so that you have a polished final product.


## Milestones and Due Dates

<div class="alert alert-info">
Here are the milestones for the term project:
{% if page.deliverables %}
<ul>
{% for deliverable in page.deliverables %}
<li> {{ deliverable.due_date | date: "%b %-d, %Y" }} - {{deliverable.description}}.</li>
{% endfor %}
</ul>
{% endif %}
</div>


# Milestone 1

For Milestone 1, you'll need to form a team and come up with 3 project ideas.  For each idea you should describe:
1. A problem definition (1 to 2 paragraphs, plus an illustrative example)
1. A pointer to two or more more papers or sections textbook that describes the problem
1. What evaluation metrics could use to score system outputs 
1. What type of data you will need to evaluate, and how much data is available 


The term project is a team exercise.  The minimum team size is 4, and the max team size is 6.  If you need help finding a team, you can post on [this Piazza thread](https://piazza.com/class/jbse3zxepja7bz?cid=366).


## Project Ideas

You should identify what topic you would like to work on.  Pretty much any topic in natural language processing is fair game.  The first milestone for the term project is to pick 3 topic ideas that your team might be interested in exploring.  The course staff will help assess the feasibility of your ideas and will make a recommendation of which of your 3 initial ideas is the best fit for the scope of the term project.  


The NLP community has a great tradition of "shared tasks".  Many of these are perfect for a term-project for this class, since they give you a great starting point for a problem definition, training and test data, a standard evaluation metric, and lots of published baselines.  Here are some pointers to shared tasks that were featured at CoNLL, SemEval, WMT, and Kaggle. 

You are welcome to choose a share task topic or to develop your own topic, provided that it is related to NLP.

### CoNLL Shared Tasks

The Conference on Computational Natural Language Learning (CoNLL) hosts a shared task every year.  Here are the past [CoNLL shared tasks](http://www.conll.org/previous-tasks): 


1. Multilingual Parsing from Raw Text to Universal Dependencies
1. Universal Morphological Reinflection
1. Multilingual Shallow Discourse Parsing
1. Shallow Discourse Parsing
1. Grammatical Error Correction	English	Proceedings
1. Modelling Multilingual Unrestricted Coreference in OntoNotes
1. Modelling Unrestricted Coreference in OntoNotes	English
1. Hedge Detection	English	Proceedings
1. Syntactic and Semantic Dependencies in Multiple Languages
1. Joint Parsing of Syntactic and Semantic Dependencies
1. Dependency Parsing: Multilingual & Domain Adaptation
1. Multi-Lingual Dependency Parsing
1. Semantic Role Labeling	English	 
1. Language-Independent Named Entity Recognition
1. Clause Identification
1. Chunking
1. NP Bracketing


### SemEval

The International Workshop on Semantic Evaluation (SemEval) hosts a range of shared tasks every year.  Here are links to the SemEval tasks:

[SemEval-2017](http://alt.qcri.org/semeval2017/index.php?id=tasks)


1. Semantic Textual Similarity
2. Multi­lingual and Cross­-lingual Semantic Word Similarity
3. Community Question Answering
4. Sentiment Analysis in Twitter
5. Fine-Grained Sentiment Analysis on Financial Microblogs and News
6. #HashtagWars. Learning a Sense of Humor
7. Detection and Interpretation of English Puns
8. RumourEval. Determining rumour veracity and support for rumours
9. Abstract Meaning Representation Parsing and Generation
10. Extracting Keyphrases and Relations from Scientific Publications
11. End-User Development using Natural Language
12. Clinical TempEval


[SemEval-2016](http://alt.qcri.org/semeval2016/index.php?id=tasks)


1. Semantic Textual Similarity. A Unified Framework for Semantic Processing and Evaluation
2. Interpretable Semantic Textual Similarity
3. Community Question Answering
4. Sentiment Analysis in Twitter
5. Aspect-Based Sentiment Analysis
6. Detecting Stance in Tweets
7. Determining Sentiment Intensity of English and Arabic Phrases
8. Meaning Representation Parsing
9. Chinese Semantic Dependency Parsing
10. Detecting Minimal Semantic Units and their Meanings
11. Complex Word Identification
12. Clinical TempEval
13. TExEval-2 -- Taxonomy Extraction
14. Semantic Taxonomy Enrichment


[SemEval-2015](http://alt.qcri.org/semeval2015/index.php?id=tasks)

1. Paraphrase and Semantic Similarity in Twitter
2. Semantic Textual Similarity
3. Answer Selection in Community Question Answering
4. TimeLine. Cross-Document Event Ordering
5. QA TempEval
6. Clinical TempEval
7. Diachronic Text Evaluation
8. SpaceEval
9. CLIPEval Implicit Polarity of Events
10. Sentiment Analysis in Twitter
11. Sentiment Analysis of Figurative Language in Twitter
12. Aspect Based Sentiment Analysis
13. Multilingual All-Words Sense Disambiguation and Entity Linking
14. Analysis of Clinical Text
15. A CPA dictionary-entry-building task
17. Taxonomy Extraction Evaluation
18. Semantic Dependency Parsing


[SemEval-2014](http://alt.qcri.org/semeval2014/index.php?id=tasks)

1. Evaluation of Compositional Distributional Semantic Models on Full Sentences through  Semantic Relatedness and Entailment
1. Grammar Induction for Spoken Dialogue Systems
1. Cross-Level Semantic Similarity
1. Aspect Based Sentiment Analysis
1. L2 Writing Assistant
1. Supervised Semantic Parsing of Spatial Robot Commands
1. Analysis of Clinical Text
1. Broad-Coverage Semantic Dependency Parsing
1. Sentiment Analysis in Twitter
1. Multilingual Semantic Textual Similarity


[SemEval-2013](https://www.cs.york.ac.uk/semeval-2013/index.php%3Fid=tasks.html)

1. TempEval-3 Temporal Annotation
1. Sentiment Analysis in Twitter
1. Spatial Role Labeling
1. Free Paraphrases of Noun Compounds
1. Evaluating Phrasal Semantics
1. Semantic Textual Similarity (becomes *Sem Shared Task)
1. The Joint Student Response Analysis and 8th Recognizing Textual Entailment Challenge
1. Cross-lingual Textual Entailment for Content Synchronization
1. Extraction of Drug-Drug Interactions from BioMedical Texts
1. Cross-lingual Word Sense Disambiguation
1. Evaluating Word Sense Induction & Disambiguation within An End-User Application
1. Multilingual Word Sense Disambiguation
1. Word Sense Induction for Graded and Non-Graded Senses
1. The Coarse-Grained and Fine-Grained Chinese Lexical Sample and All-Words Task

[SemEval-2012](https://www.cs.york.ac.uk/semeval-2013/index.php%3Fid=tasks.html)

1. English Lexical Simplification
1. Measuring Degrees of Relational Similarity
1. Spatial Role Labeling
1. Evaluating Chinese Word Similarity
1. Chinese Semantic Dependency Parsing
1. Semantic Textual Similarity
1. COPA. Choice Of Plausible Alternatives An evaluation of commonsense causal reasoning
1. Cross-lingual Textual Entailment for Content Synchronization

[Previous years](https://en.wikipedia.org/wiki/SemEval#External_links)


## Kaggle 

Kaggle is a platform for machine learning competitions where people compete to produce the best models for a huge range of different datasets. Companies often offer a reward for their competitions.  There's tons of cool data and competitions that you can base your final project on.  

Here are a few relevant competitions:
* [Sentiment Analysis on Movie Reviews](https://www.kaggle.com/c/sentiment-analysis-on-movie-reviews)
* [Toxic Comment Classification Challenge](https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge)
* [Convert English text from written expressions into spoken forms](https://www.kaggle.com/c/text-normalization-challenge-english-language)
* [Quora Question Pairs - Can you identify question pairs that have the same intent?](https://www.kaggle.com/c/quora-question-pairs)
* [The Allen AI Science Challenge - Is your model smarter than an 8th grader?](https://www.kaggle.com/c/the-allen-ai-science-challenge)
* [DonorsChoose.org Application Screening - Predict whether teachers' project proposals are accepted](https://www.kaggle.com/c/donorschoose-application-screening#evaluation)
* [TensorFlow Speech Recognition Challenge - Can you build an algorithm that understands simple speech commands?](https://www.kaggle.com/c/tensorflow-speech-recognition-challenge)
* [Spooky Author Identification - Identify horror authors from their writings](https://www.kaggle.com/c/spooky-author-identification)


You can also check out the [Linguistics tag](https://www.kaggle.com/tags/linguistics) and  the [Langauges tag](https://www.kaggle.com/tags/languages) for lots of other ideas.  Want [130,000 wine reviews](https://www.kaggle.com/zynicide/wine-reviews) with their ratings, or [55,000 song lyrics](https://www.kaggle.com/mousehead/songlyrics)?  Find them on Kaggle. 


## Course staff ideas

Here are a list of potential project ideas that were brainstormed by the course staff:
* __Rank scalar adjectives__. Adjectives like good, tasty, yummy, delicious, scrumptious all describe some property of a noun (how good something tastes), but they vary in intensity.  Can you write an algorithm to put them in the correct order by intensity?  For instance, *good < tasty < yummy < delicious < scrumptious*.  Here are some good papers about the ranking scalar adjectives:
  * [Was it good? it was provocative. learning the meaning of scalar adjectives.](https://aclanthology.info/pdf/P/P10/P10-1018.pdf)
  * [Good, great, excellent: Global inference of semantic intensities.](https://www.cs.unc.edu/~mbansal/papers/tacl_acl13_semanticIntensity.pdf)
  * [Deriving adjectival scales from continuous space word representations](http://aclweb.org/anthology//D/D13/D13-1169.pdf)
  * [Large, huge or gigantic? identifying and encoding intensity relations among adjectives in wordnet.](https://link.springer.com/content/pdf/10.1007%2Fs10579-012-9212-1.pdf)
  * [Adjscales: Differentiating between similar adjectives for language learners.](http://zzz.cl.cs.titech.ac.jp/_media/publication/639.pdf)
  * [Lexicon-Based Methods for Sentiment Analysis](https://www.mitpressjournals.org/doi/abs/10.1162/COLI_a_00049) provides [intensity rankings](https://github.com/sfu-discourse-lab/SO-CAL/blob/master/Resources/dictionaries/English/adj_dictionary1.11.txt) that might be useful as features.  
 
* __Order prenominal modifiers__. In English, prenominal modifiers must come in a certain order.   It sounds fluent to say *the big beautiful white wooden house*, but not *the white wooden beautiful big house*.  Here's a NLP good paper describing a [class-based approach to ordering prenominal modifiers](http://www.aclweb.org/old_anthology/W/W09/W09-0608.pdf).
You could collect all of the pre-nominal modifiers from a large parsed corpus like the [WaCKy corpora](http://wacky.sslmit.unibo.it/doku.php?id=corpora) or the [Annotated Gigaword](https://catalog.ldc.upenn.edu/ldc2012t21), and then train a model to predict their order.   Here's a rule from a grammar book about what order adjectives are supposed to come in.  Is it true?
 <blockquote align="center" class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Things native English speakers know, but don&#39;t know we know: <a href="https://t.co/Ex0Ui9oBSL">pic.twitter.com/Ex0Ui9oBSL</a></p>&mdash; Matthew Anderson (@MattAndersonNYT) <a href="https://twitter.com/MattAndersonNYT/status/772002757222002688?ref_src=twsrc%5Etfw">September 3, 2016</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

 * __Predict the star rating of Amazon reviews__.  Amazon released a collection of  [130 million customer reviews](https://s3.amazonaws.com/amazon-reviews-pds/readme.html) from 1995 until 2015.  How well you predict the star rating based on the text of the reviews? There are tons of papers on NLP and sentiment analysis.  [Chapter 6](https://s3.amazonaws.com/amazon-reviews-pds/readme.html) and [Chapter 18](https://web.stanford.edu/~jurafsky/slp3/18.pdf) of the textbook as a good place to start. 

 * __Help assess depression and risks of self-harm in social media__.  One way that NLP might be used for social good is to try to identify people who are at risk of suicide based on their social media posts. There's a ton of good academic work on this.
   * The annual workshop on [Computational Linguistics and Clinical Psychology](http://clpsych.org) is a good place to start looking.  It has a lot of relevant publications in its past proceedings, and has featured many shared tasks.
   * One of the EMNLP 2017 best paper awards went to [Depression and Self-Harm Risk Assessment in Online Forums](http://aclweb.org/anthology/D17-1322)
   * Vanessa Callison-Burch was involved in [Facebook's suicide prevention efforts](https://www.nytimes.com/2016/06/15/technology/facebook-offers-tools-for-those-who-fear-a-friend-may-be-suicidal.html)

* __Generation text description of images__.  There's been a lot of cool work that combines computer vision and natural language processing.  One thread of that research tries to generate captions for images.  A good overview is provided in these papers:
  * [Framing Image Description as a Ranking Task: Data, Models and Evaluation Metrics](https://www.jair.org/media/3994/live-3994-7274-jair.pdf)
  * [Show and Tell: Lessons learned from the 2015 MSCOCO Image Captioning Challenge](https://arxiv.org/abs/1609.06647)
  * [From Captions to Visual Concepts and Back](http://www.m-mitchell.com/papers/CVPR15_0866.pdf)
  * There are several tutorials on how to get started with caption generation:  [A Gentle Introduction to Deep Learning Caption Generation Models](https://machinelearningmastery.com/deep-learning-caption-generation-models/)
  * [How to Develop a Deep Learning Photo Caption Generator from Scratch](https://machinelearningmastery.com/develop-a-deep-learning-caption-generation-model-in-python/)
  * [Caption this, with TensorFlow. How to build and train an image caption generator using a TensorFlow notebook.](https://www.oreilly.com/learning/caption-this-with-tensorflow)

* __What can we learn about people on social media through self-identification?__ Google BigQuery has a set of [all Reddit comments since 2005](https://bigquery.cloud.google.com/dataset/fh-bigquery:reddit_comments). Past NLP work on mental health examined social media users who self-identified as having clinical depression or PTSD by looking for public comments like "I was diagnosed with depression".  Can we use self-identification to learn the patterns of language use of different demographics?  Here's a search through a subset of the Reddit comments for the phrase "I'm a [blank]":
{% highlight sql %}
  SELECT author, body FROM [fh-bigquery:reddit_comments.2015_05] WHERE LENGTH(body) < 255 AND LENGTH(body) > 30 AND 
  (body LIKE 'i\'m a %'
  or body LIKE 'I\'m a %'
  or body LIKE 'a\'m a %'
  or body LIKE 'i\'m an %'
  or body LIKE 'I\'m an %'
  or body LIKE 'a\'m an %') LIMIT 10000;
{% endhighlight %}
And you get back a set of usernames and how they self identified.  Can you develop self-indentification queries for different demographic info, retrieve all of the comments from those users and then analyze the language differentiates for different groups like [men v. women](http://www.aclweb.org/anthology/P13-1070) or straight people v. gays and lesbians? 

## What do you need to turn in?

For Milestone 1, you'll need to turn in writeups for your 3 project ideas.  

For the whole project, here's a provisional list of the deliverables that you'll need to submit:

1. `report.md`: The final version of your write-up, incorporating any additional changes to your revised draft (if any).
1. `readme.md`: A brief description of your task and the included code.
1. `data-train/`: A directory containing the training data.
1. `data-dev/`: A directory containing the development data for local evaluation.
1. `data-test/`: A directory containing the test data for leaderboard evaluation.
1. `default`: A full implementation of the default system.
1. `baseline`: A skeleton of the baseline system to be provided to students.
1. `baseline-solution`: A full implementation of the baseline system.
1. `extension-1`, `extension-2`, ...: Full implementations of the extensions, one per group member.
1. `extensions.md`: A brief write-up describing your extensions and their performance.
1. `grade-dev`: A grading script for local evaluation. This may be a wrapper around a generic grading script `grade`.
1. `grade-test`: A grading script for leaderboard evaluation. This may be a wrapper around a generic grading script `grade`.



<a name="milestone-2"></a>
# Milestone 2

The course staff will review the 3 ideas that you submitted for Milestone 1, and make a recommendation on which of your ideas you ought to pursue.  For Milestone 2, your job is to get started on that idea with three steps:
1. Collect your data
2. Write an evaluation script
3. Write a simple baseline (for instance, a majority class baseline)

We have also assigned a course staff member to be your mentor.  Feel free to reach out to your mentor with any questions.

## Collect your data

Since most of the projects that we do in this course are data-driven, it's very important to have your data ready to go at the outset of a project.  You should collect all of the data that you'll need for your term project and split the data into three pieces:

* Training data
* Development data
* Test data

The training data will be used to train the model, the dev data can be used to optimize your system parameters and/or to evaluate different approaches to the problem, the test data is a "blind" test set that will be used in the final evaluation.

If you are basing your term project on a shared task, then usually the data will be collected already, and usually it will be divided into a standard training/dev/test split.  If it's already assembled and split - great!  You're ahead of the game.  If you're not doing a shared task, then you may need to assemble your own data.  A good way of creating your own training/dev/test split is to divide the data into chunks that are sized around 80%/10%/10%, where you want to use most of the data for training.  It's important to ensure that the same items don't appear in more than one of the splits.

For your M2 deliverables, we'll ask you to submit your data, plus a markdown file named data.md that describes the format of the data.  If your data is very large, then you can submit a sample of the data and give a link to a Google Drive that contains the full data set.   You data.md should describe the number of items in each of your training/dev/test splits.

## Write an evaluation script

For the next part of M2, you'll need to determine a suitable evaluation metric for your task, and implement it.  If you're basing your term project on a shared task, then there is likely an established evaluation metric for the task.  You should re-use it. If you're doing a new task, then you may have to do a literature review in order to determine what metrics are best suited for your task.

You should write an evaluation script that takes two things as input: a system's output and a corresponding set of gold standard answers.  Your script should output a number that quantifies how good the system's answers are.    

For your deliverables, you should include your script, plus an example of how to run it from the command line.  You should give a formal definition of the evaluation metric that explains how it is calculated in a markdown file called scoring.md - this file should  cite any relevant papers that introduce the metric.    You can also cite Wikipedia articles that describe your evaluation metric, and/or link to an overview paper describing the shared task that you're basing your project on if it defines the metric.

## Write a simple baseline

As the final part of M2, you should write a simple baseline.  This should be the simplest way of producing output for your task.  For example, it could be a majority class baseline (like the one that we used in HW1) that determines the majority class from the training data and guesses that class for each item in the test set.

You should write a python program that will generate the output for the baseline, and you should submit that as simple-baseline.py.  You should also include a markdown file named simple-baseline.md that describes your simple baseline, gives sample output, and reports the score of the baseline when you run it on the test set, and evaluate it with your scoring script. 


## What do you need to turn in?

* You should create a directory containing your training/dev/test data (please create a gzipped tar archive of the data).  If your data is too large to upload to gradescope, the you can submit a sample of the training data, plus your compute dev and test sets.
* Please upload a markdown file that describes your data (name it data.md).  It should give an example of the data, describe the file format of the data, give a link to the full data set (if you're uploading a sample), and give a description of where you collected the data from.
* You should describe your evaluation metric in a markdown file called scoring.md.  This should give a formal definition of your metric, and relevant citations to where it was introduced.  Your scoring.md file should also show how to run your evaluation script on the command line (with example arguments, and example output).  The scoring.md file should say whether higher scores are better, or lower scores are better.
* You should include your evaluation script (you can call then score.py if you're writing it in python).
* You should upload simple-baseline.py and describe it in simple-baseline.md.  Your simple-baseline.md should say what score your evaluation metric gives to the simple baseline for your test set.



<a name="milestone-3"></a>
# Milestone 3

The goals of Milestone 3 are to do a literature review to determine the approaches that other researchers took to solve your problem, and to implement a published system to establish as a strong baseline for your project.

For your literature review, you should read 3-5 research papers that address the problem that you are working on.  You should write a 1-2 paragraph summary of each paper, desribing the approaches that they proposed and what results they got.  You should also include an addition 1-2 paragraphs saying which of the approaches that you selected as the published baseline that you are re-implementing.  You should submit your literature review in a markdown formatted file called lit-review.md.

You should re-implement the published baseline that you selected.  It's fine to use machine learning packages like sklearn, or NLP software like Spacy or NLTK, but you should implement the main algorithms yourself.  You should not turn in existing code that implements the baseline.

You should include a baseline.md markdown file that includes step-by-step instructions on how to run your baseline code.   Your baseline.md should also report the score for your system for your test and development data, and compare that to your random baseline.

For Milestone 5, you'll need to implement several extensions beyond this published baseline.  These should be different experiments that you run to try to improve its performance.  The number of extension that you'll implement depends on number of members of your group.  If you have 4 team members, you should implement 2 extensions.  If you have 5, then 3 extensions.  If you have 6, then 4 extensions. 



## What do you need to turn in?

* You should submit a literature review in a markdown file called lit-review.md.  This will include the citation information for each paper  (authors, title of paper, publication venue, year of publication, number of pages) in a Works Citated section. You should have a 1-2 paragraph description of each paper, plus a 1-2 paragraph explanation of which one you chose to implement as your baseline and why.
* You should submit your code for the baseline system.  This should be in a python file called a baseline.py.  You should also submit a baseline.md file explaining how to run it, and reporting its performance on your dev and test set, according to your evaluation metric. 




<a name="milestone-4"></a>
# Milestone 4

For Milestone 4, you will do an in-class presentation for your project, write-up your project as if it were a homework assignment, and turn in a draft of your final report with one of your extensions completed. 

Your in-class presentation should be 12 minutes long.  You should create a slidedeck with [Google Slides](https://www.google.com/slides/about/).  Your presentation should convey  these main ideas:
* What is the topic of your term project?  You should clearly explain to your classmates the problem that you selected to work on.  Give an illustrative example of the problem first, and then give a more formal definition of the problem.
* What is exciting about your term project?  Why did you want to work on this topic?  
* How does the topic relate to the class? What new things did you learn? 

You may also want to cover topics like this:
* What kind of data is available for this problem?  How do you evaluate whether a solution is good or not?  If the evaluation metric is not already familiar to the class, then walk through an explanation of how it works.
* What is the baseline performance for the simple baseline like a majority class baseline?
* What approaches have people taken in the past?  How successful have they been?
* What did you implement for your published baseline?

In addition to your in-class presentation, you'll need to create a write-up your project as if it were a homework assignment.  Based on the presentations, we'll have a vote to pick a few of your term projects that will be options for what the rest of the students in the class do as their final HW assignment.

Finally, by the Milestone 4 deadline, you need to have completed one of the extensions to your published baseline.

## What do you need to turn in?


* The slides for your presentation.
* A markdown file called homework.md that contains the write-up your project as if it were a homework assignment. 
* A markdown file called extensions.md that desribes the extension(s) to the published baseline that you implemented for Milestone 4.  It should explain what you tried, and whether it improved performance over the baseline (it's OK if it didn't).  You should include tables of results using your scoring function and test data.



<a name="milestone-5"></a>
# Milestone 5

For your final milestone, you'll complete your extensions to the baseline, and you'll produce a final writeup for your term project.  As a reminder, the number of extensions that you must submit depends on your group size.  If you have 4 team members, you should implement 2 extensions.  If you have 5, then 3 extensions.  If you have 6, then 4 extensions. You already produced one of those extensions for Milestone 4.

Your final report should be written in the style of a scientific paper.  It should contain the following sections:

* Title.  A descrpitive title for your term project
* Authors.  A list of team members
* Abstract.  Your abstract should give an overview of your project and your results (~100 words).
* Introduction.  Your introduction should contain the following information. (~300-500 words, plus one illustrative example).
   * An informal description of the task, and how it relates to NLP/Computational Linguistics (1-2  paragraphs)
   * A figure that illustrates the task, or an illustrative example of the type of problem you're trying to solve.  This can be a picture, or an example of an input and output.  You should include a caption or a short paragraph that describes what's happening in your illustration.
   * A formal definition of the problem.
   * A paragraph describing why you picked this task for your term project. 
* Literature Review. You can adapt your literature review from Milestone 3 for this part of your writeup.  (~300-500 words, with 3 or more ciations).
   * If you adapted a shared task for your term project, then you should describe the share task in your literature review, and cite the overview paper and give a URL to shared task homepage (if applicable).
   * For your literature review, you should also cute and summarize 3-5 research papers that address the problem that you are working on.  You should write a 1-2 paragraph summary of each paper, desribing the approaches that they proposed and what results they got.  Be sure to include a full citation of these papers in your Bibliography. 
* Experimental Design.  Your Experimental Design section should include a description of your training data, your evaluation metric, and your simple baseline model along with its performance on the test set.  You can adapt your Milestone 2 submission for this part. (~300-500 words, plus 2 figures/tables, plus 1 or more equations).
   * Data.  This subsection should describe your training/development/test data.  You should give an figure or table with examples from your data (including inputs and output labels).  You should include a table that describes the size of your data sets.  For example, it should give number of sentences or words, etc for each of the splits.  You should also characterize the data.  For instance, if there's a skewed distribtuion over the labels, you should reoprt it here.  If your training data comes from a published paper, then cite that paper and explain how they collected the data.  If you constructed your data set, then explain in detail how you collected it, and include example code in an appendix.
   * Evaluation Metric.  This subsection should describe your evaluation metric.  You should include an English description of the metric, an equation for how your metric is computed, and a citation for this metric, and some citation(s) that shows what past publication(s) used this metric for the task that you're working on. For your equation, you can use [MathJax](https://www.mathjax.org) markup.
   * Simple baseline.  You should compute the majority class baseline (or other simple baseline) for your data, and report it in this section.  This is a way of characterizing the data and showing the diffiulty of the task.  
* Experimental Results.  In this section, you should describe your implementation of a published baseline, and all of the extensions that you experimented with for your term project, and an error analysis of your system's output. (~300-500 words).
   * Published baseline.  In this subsection you should write a detailed description of the published baseline that you implemented and cite the paper that it was published in. (You can update your Milestone 4 submission for this).  You should report how well the model performs on your test set using the evaluation metric that you defined in your experimental design section.  Does your implementation of the published baseline reach the same level of accuracy as the original paper?  If not, why not?  Are your results directly comparable -- are they on the same test set?  If not, why not?
   * Extensions.  In this subsection, you should describe each of the extensions that you tried.  You should include a ~1-2 paragraph of each extension that explains what you tried, why you tried it, and how it performed compared to your baseline.  You should include a table of results, where the rows are the performance of the baseline or one of your extensions, and the columns are  the performance on the test set (and on the dev set if you measured it).  If you did any experiments where you searched over a set of different parameters, then you should include a result on how varying the parameter changed the performance on the dev or test set.  Your tables and figures should include a detailed caption that explain how to read them.
   * Error analysis.  In this subsection, you should perform an error anlaysis for your best performing system.  Show examples of the errors that it makes.  Can you cateorize the types of errors that it makes, and give an esimate of how prevelant each error type is?  If you extensions performed better than the published baseline, then show examples of the errors that the published baseline makes that your extensions get correct (and vice versa if your extension introduces some new errors).  
* Conclusions. You should write a brief summary of what you accomplished in your term project.  Did any of your implementations reach state-of-the-art performance on the task?  If not, how close did you come?  If not very close, then why not?  (~100-300 words). 
* Acknowledgements.  If you used someone else's code or you benefited from discussions with one of the TAs, then you should thank them here.  Give credit generously!   (Optional)
* Appendicies. This can include short snippets of code that were relevant to your project, along with a description of what it's doing.  It could also include more examples of your training data or your system's output. (Optional)

I really like examples and good illustrations.  If you created some nice visuals for your final presentation slides, then I encourage you to include them in your writeup too.  You can submit your images in a images/ subfolder.


## What do you need to turn in?

You should turn  the following items:
* final-report.md - a markdown formatted file
* images/ - a subdirectory containing any image files that you use in the figures for your report
* data/ - a subdirectory containing the training/dev/test splits that you use.  If your data is too large to submit, then you can include a file named download.md that explains how to download your data.
* code/ - a subdirectory containing all code that you developed for your project, including the baseline and extensions, and your evaluation scripts.  This should include a README.md that gives a step by step walk thorugh of how to run your code, including an example of the command lines to run to reproduce the results that you report. 
* output/ - a subdirectory containing your model's predictions on the test set, along with the gold labels.  This should also include a README.md that shows the command line on how to run your evaluation script on the output, and example of what scores the script returns.


You've reached the end.  Great job!