<strong>UPDATE (10/22/18)</strong>: Very excited that this notebook won a Google Kaggle Kernels award! [Check it out](https://www.kaggle.com/general/37924#391409).<br>

<img src='https://spacy.io/pipeline-7a14d4edd18f3edfee8f34393bff2992.svg'><center><span style="font-size:10px;">Source: <a href="https://spacy.io/usage/processing-pipelines">spaCy Language Processing Pipelines</a></span></center>

# Quick and Dirty - Entity Extraction

<span style="color:gray;font-size:20px;">From idea to prototype in AI.</span>

<em>If you've ever been around a startup or in the tech world for any significant amount of time, you've <strong>definitely</strong> encountered some, if not all of the following phrases: "agile software development", "prototyping", "feedback loop", "rapid iteration", etc.</em>

<em>This Silicon Valley techno-babble can be distilled down to one simple concept, which just so happens to be the mantra of many a successful entrepreneur: test out your idea as quickly as possible, and then make it better over time. Stated more verbosely, before you invest mind and money into creating a cutting-edge solution to a problem, it might benefit you to get a baseline performance for your task using off-the-shelf techniques. Once you establish the efficacy of a low-cost, easy approach, you can then put on your Elon Musk hat and drive towards #innovation and #disruption.</em> 

<em>A concrete example might help illustrate this point:</em>

## Introduction

### Entity Extraction

Let's say our goal was to create a natural language system that effectively allowed someone to converse with an academic paper. This task could be step one of many towards the development of an automated scientific discovery tool. Society can thank us later. 

But where do we begin? Well, a part of the solution has to deal with [knowledge extraction](https://en.wikipedia.org/wiki/Knowledge_extraction). In order to create a conversational engine that understands scientific papers, we'll first need to develop an entity recognition module, and this, lucky for us, is the topic of our notebook! 

"What's an entity?" you ask? Excellent question. Take a look at the following sentence:

> Dr. Abraham is the primary author of this paper, and a physician in the specialty of internal medicine.

Now, it should be relatively straighforward for an English-speaking human to pick out the important concepts in this sentence:

> **[Dr. Abraham]** is the **[primary author]** of this **[paper]**, and a **[physician]** in the **[specialty]** of **[internal medicine]**.

These words and/or phrases are categorized as "entities" because they represent salient ideas, nouns, and noun phrases in the real world. A subset of entities can be "named", in that they correspond to <strong><em>specific</em></strong> places, people, organizations, and so on. A [named entity](https://en.wikipedia.org/wiki/Named_entity) is to a regular entity, what "Dr. Abraham" is to a "physician". The good doctor is a real person and an instance of the "physician" class, and is therefore considered "named". Examples of named entities include "Google", "Neil DeGrasse Tyson", and "Tokyo", while regular, garden-variety entities can include the list just mentioned, as well as things like "dog", "newspaper", "task", etc.

Let's see if we can get a computer to run this kind of analysis to pull important concepts from sentences. 

### The Task

For our conversational academic paper program, we won't be satisfied with simply capturing named entities, because we need to understand the relationships between general concepts as well as actual things, places, etc. Unfortunately, while most out-of-the-box text processing libraries have a moderately useful <strong>named entity recognizer</strong>, they have little to no support for a generalized <strong>entity recognizer</strong>. 

This is because of a subtle, yet important constraint. 

Entities, as we've discussed, correspond to a superset of named entities, which <strong><em>should</em></strong> make them easier to extract. Indeed, blindly pulling all entities from a text source is in fact simple, but it's sadly not all that useful. In order to justify this exercise, we'd need to develop an entity extraction approach that is restricted to, or is cognizant of, some particular domain, for example, neuroscience, psychology, computer science, economics, etc. This paradoxical complexity makes it nontrivial to create a generic, but useful, entity recognizer. Hence the lack of support in most open-source libraries that deal with natural language processing. 

To largely simplify our task then, we must generate a set of entities from a scientific paper, that is <strong><em>larger</em></strong> than a simple list of named entities, but <strong><em>smaller</em></strong> than the giant list of all entities, restricted to the domain of a particular paper in question. 

Yikes. Are you sweating a little? Because I am. Instead of reaching for some Ibuprofen and deep learning pills, let's make a prototype using a little ingenuity, simple open-source code, and a lot of heuristics. Hopefully, through this process, we'll also learn a bit about the text processing pipeline that brings understanding natural language into the realm of the possible. 

Enought chit-chat. Let's get to it! Check out the full [Jupyter Notebook](https://nbviewer.jupyter.org/github/SudoSharma/entity_extraction/blob/master/entity_extraction.ipynb) online at this nbviewer link for better rendering of all graphics.
