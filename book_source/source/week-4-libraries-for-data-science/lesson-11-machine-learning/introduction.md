# Introduction

<div style="position: relative; padding-bottom: 62.5%; height: 0;">
    <iframe src="https://www.loom.com/share/cbaacf9d52ae4a8a85ee99da5e2fa0b4?sharedAppSource=personal_library" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
</div>

```{warning}

**Word of Warning**

<Element 'break' at 0x7fcd26039180>

<Element 'break' at 0x7fcd26039720>
Learning machine learning can be kind of challenging at first! There are whole courses dedicated to this topic! Our goal in CSE 163 is to provide you with some framework to think about machine learning so that you can be "conversational" in ML. You are not expected to be an expert in this topic after this reading!
<Element 'break' at 0x7fcd26039950>

<Element 'break' at 0x7fcd26039b80>
This lesson will be a bit different than the rest because it will contain lots of new vocabulary. We usually recommend that you are taking notes on these lessons (so you can synthesize your knowledge), but this one will be very important to take notes on the terms defined in
**bold**
. Annoyingly, we aren't able to present mathematically precise definitions for these terms because that requires some mathematical formalism that requires taking one of those courses on ML to understand. However, you can still get an intuition for what the term means from the way we present it!
<Element 'break' at 0x7fcd26039b30>

<Element 'break' at 0x7fcd260391d0>
One thing that is particularly difficult is that there are a lot of concepts/terms that interrelate. It's hard to tell a "linear" story that goes from point A to point B without hitting something we haven't heard before. We want to recognize that the structure of this lesson might be a bit confusing and it's totally expected that you go back to re-read stuff after reading on!

```

## Twitter: Text Data

Congrats! You have been hired as a data scientist at Twitter! Your boss comes up to you and tells you that your first task is to answer the age-old question: Which is more popular on the internet, cats or dogs?

As a Twitter employee, you learned how to access all the tweets on the website in Python. Using your CSE 163 knowledge so far, you come up with a good first attempt at trying to answer this question. Your idea is to just scan through all the tweets (a list of strings) and just count the number of tweets contain the string
`'dog'`
or
`'cat'`
. You go ahead and write something like the following code.

```py
cats = []
dogs = []
for tweet in tweets:
    if tweet.find('dog') >= 0:
        dogs.append(tweet)
    elif tweet.find('cat') >= 0:
        cats.append(tweet)
        
# Normally people would write
#   if 'dog' in tweet:
# But we want to be clear for example how this works for strings
```

This doesn't capture all the complexity of the problem, but it seems like a good first try and your boss seems happy enough!

A big part fo the reason we are able to solve this problem, is because it's "easy" to tell if the string
`'dog'`
is inside a tweet.

## Instagram: Image Data

The job market is good for data scientists so you decide to switch jobs and work at Instagram instead. Your reputation as an expert in the field of cat-vs-dog precedes you. Your new boss asks you to solve the same problem but using Instagram's dataset of images instead. You decide to start with what you know and try something similar to what you did at Twitter by writing the following code.

```py
cats = []
dogs = []
for pic in pictures:
    if 'somehow tell there is a dog in this pic':
        dogs.append(pic)
    elif 'somehow tell there is a cat in this pic':
        cats.append(pic)
```

Unfortunately, there doesn't seem to be a straight-forward way of describing that a picture contains a dog or a cat. How could you write an if-statement indicating there is a dog there?

Think about that task for a second. Imagine your friend has never seen a cat or a dog before. Come up with an English description that lets your friend determine, for a given photo, whether there is a cat or a dog there. Even if you were able to come up with some rule that your friend could follow, I imagine it would be a nightmare to try to write a program to detect if that rule is met!

We have set up why this is hard to do ourselves, so now we can explain why this thing called
**machine learning**
can help us solve this problem.

## Machine Learning


**Machine learning**
is a set of techniques and algorithms that allows the computer to learn by example to solve some task. There is an annoyingly abstract definition of machine learning shown below, but what it's really saying is "uses experience (data) to improve itself".

<Element 'blockquote' at 0x7fcd2603c4a0>
In our example of classifying cats vs dogs in images, this would mean a fundamental change to the approach. Instead of writing the rules ourselves, machine learning lets us give the computer a ton of examples of cat images and a ton of examples of dog images, and letting it learn the rules itself from those examples. This is still pretty abstract, and we will see a concrete example of how to learn rules from data in a bit, but before that, we need a little bit more terminology for setup.

You might have noticed from the last paragraph, that we said you need to give it examples of cat images and dog images, implying that you need to have a dataset of examples that you already know the answer to! We call this dataset of known examples a
**training set.**
In our context, each
**example**
is a single image and a label indicating whether the image contains a dog or a cat. The training set is a dataset that you will use to "train" the model so that it can learn the rules of differentiating between cats and dogs.

A
**machine learning algorithm**
(commonly, just called a "learning algorithm") takes this training set and outputs a
**model**
that it thinks will do the best at the task. A
**model**
is the "rules" to predict the value for any given example.

For most setups in machine learning, this training set needs to have
**features**
and
**labels**
. The
**labels**
are the correct values for an example in the training set and the
**features**
are the description of the example itself. Notice this definition of features is awfully vague! It turns out one of the hardest parts of machine learning is coming up with a good set of features to describe your data that is useful for the learning algorithm to learn from!

## Features Matter

In the image below, we show an example of what a model to classify cats and dogs is trying to do. The features describing each image put the examples in a "feature space", and the learning algorithm chooses a model that acts as a separator between dog images and cat images in this space. In the picture below, the green plane is the learned model. You, as the expert on the task you are trying to get the machine to learn, come up with a set of features to describe each example.

So in classifying dog and cat images, maybe you determine that you will use the following features:

<Element 'list' at 0x7fcd2377e450>
In practice, you might want to use more than 3 features and these 3 features might not actually be good ones for solving this problem in real life. We will pretend these features describe the data well for this example though. Below, we show a picture of what these cats and dogs would look like in this feature space and a model that was learned to separate dogs from cats.

<Element 'figure' at 0x7fcd236cfea0>
There are tons of different types of learning algorithms and different types of models to consider for solving a task (you'd learn many of these in a machine learning class). By far, the most important thing to have is good features describing your data. There is a saying for machine learning practitioners that goes "Garbage in, garbage out". If you don't come up with a good set of features describing the problem, your model won't do well no matter how cool or great that model is.

Consider the picture below showing examples of cats and dogs drawn in a feature space that just uses a single feature (e.g., how many red pixels are in the image). You can probably tell if we use this as the only feature, it will be quite difficult for the model to tell them apart. There isn't a good separation between the dogs and cats in this feature space, so the learning algorithm will probably struggle to learn a model that separates them well.

<Element 'figure' at 0x7fcd236cf9f0>
Frustratingly, there is no right answer on what feature(s) to use or how they are computed. There is usually a balance between having too few and having too many, but the quality of the features at describing the data is usually the most important. You have to use domain expertise to come up with the right choices and, usually, do a lot of trial and error! We will see in our examples today, it's usually more clear what the features should be (e.g., the columns of the CSV we are working with).

## A Little More Terminology

We have been focusing a lot on this example of cats vs dogs, but machine learning can solve many types of tasks! Machine learning tasks generally fall into the following categories depending on what type of value you are trying to predict.

<Element 'list' at 0x7fcd2375b680>
A lot of the time, people rush to apply ML to a task without sitting down and defining what they are trying to solve and how. Before you begin any ML task, ask yourself:

<Element 'list' at 0x7fcd2375bd10>
```{warning}
Notice: We have yet to bring up the question of "Is this a problem that you can solve in an ethical way using ML?" We haven't brought up this question yet, not because it's not important, but because we need some technical and conceptual practice understanding how ML models learn before we can better explore when and why we might not want to use it. We will talk more about this a little bit in Lesson 12, and in much more detail in our Ethics module later this quarter.

```

## Recap Questions

Use these questions to help you test your understanding. These might be good things to talk about with your group in class!

<Element 'list' at 0x7fcd2375bb30>