Welcome to the first module of our course, 

which covers preliminary ideas and fundamentals. 

In this short video, 

I'll go over what we can expect 

as we navigate through this module. 

Let's go ahead and get started. 

As with most modules, 

we're going to have a couple of 

many lectures on different core topics. 

In this case, fundamental techniques 

for the design and analysis of algorithms. 

We'll include a fun optional enrichment lecture. 

I'll say a bit more about that in a second.

Play video starting at ::34 and follow transcript0:34

We'll have some practice exercises 

so that you can make sure that you 

are able to apply the material that we're talking about. 

And then we'll launch our first assignment. 

More on that in just a second as well. 

That will be due in another week or two, 

giving you plenty of time to think about it. 

If you are taking this course for credit, 

this would be a good time to make sure 

you review the syllabus to make sure that 

you're familiar with all of 

the important details like course grading policies, 

academic integrity policies, things like that. 

Do, of course, reach out to 

the course staff if you have any questions at all. 

In general, make sure that you do 

stay engaged with the course staff.

Play video starting at :1:14 and follow transcript1:14

We are here to help you whenever 

you get stuck on anything. 

This is an online course. 

It's especially important that 

both sides make an effort to stay 

engaged so that we can help you as much 

as possible in navigating the course material. 

Let me say a little bit about some of these items. 

I'll say something about the lecture content in a second. 

The optional enrichment lecture is on a topic, 

which is quite interesting. 

It's how you account 

for real-world memory management and caching.

Play video starting at :1:47 and follow transcript1:47

A lot of algorithms perform 

very differently on a real system than you 

might expect because of the fact that real systems 

involve memory hierarchies with 

different levels of caching and whatnot, 

and an algorithm that, say, scans 

sequentially through memory is likely to run 

much faster than one that jumps around 

haphazardly through memory and has a lot of cache misses. 

We're going to talk about elegant ideas for 

algorithm design and analysis 

that take this into account, 

in particular something that I'm a big fan 

of called the Cache-Oblivious model. 

Also want to say a word or 

two about the first assignment. 

I'm particularly proud of this assignment. 

I think it illustrates a lot of really nice concepts. 

It's quite approachable. 

It's based on nothing more 

than a slight generalization of binary search, 

but it does highlight a very 

real-world application of how to find 

the right settings of a parameter 

to plug into a complicated model, 

and it highlights all of 

the wonderful messy open-endedness 

that you see in real-world problems.

Play video starting at :2:54 and follow transcript2:54

There's a lot of depth to the assignment. 

You can take it as far as you want it to go. 

There's a lot of interesting ideas that 

can be brought to bear on just this one assignment. 

I think it should be fun. 

Hopefully everyone enjoys working on that. 

In terms of core topics, 

we'll spend most of our time this week on 

the topic of how to analyze algorithm performance, 

what terminology and tools do we have 

for describing the running time 

of an algorithm in particular. 

We'll see lots of examples.

Play video starting at :3:25 and follow transcript3:25

We'll work through many, many 

different algorithms and talk 

about how we can analyze 

their performance using different approaches. 

We will also talk about algorithm design in general, 

so what are some high-level algorithm 

design paradigms, so to speak, 

that are very prevalent in 

terms of how we build algorithms, 

general design techniques, 

things like iterative refinement, 

incremental construction, those types of ideas. 

We'll also talk about models of computation. 

We want to make sure that our algorithms are generic and 

portable and not really tied 

to any particular hardware environment. 

We define what's called a model of computation, 

which is an abstract computing environment 

on which our algorithms are executing, 

and it's intended to serve as 

an approximation for a modern digital computer. 

That gives us a way of describing 

algorithms in a way that doesn't 

necessarily tie us to a particular hardware environment. 

We'll cover basic data structures, 

arrays, link lists, stacks, queues, 

things you're likely to encounter 

throughout the course and that you've maybe 

seen quite a bit already if 

you're a software engineer, for example.

Play video starting at :4:37 and follow transcript4:37

Then finally, I'm going to sneak in discussion 

of several prominent sorting algorithms, 

mostly as examples of how to compute running times. 

We'll see things like insertion sort, 

bubble sort, merge sort. 

That way, everyone can become 

familiar and make sure that you have 

refreshed your memory on 

some of the basic sorting algorithms. 

Finally, since week 1 is covering the fundamentals, 

it's inevitable that we have to cover the basics. 

I don't want the basics to get too boring, 

and so we're going to lead up to at the end of 

the module a discussion of a cool, 

interesting problem that has maybe a non-obvious, 

yet elegant solution with maybe a 

non-obvious, yet elegant analysis. 

The backstory behind this problem 

was I was talking to my father-in-law one day. 

He's an avid photographer, 

and he had some very large digital photographs 

that were rectangular images.

Play video starting at :5:35 and follow transcript5:35

The problem he was interested in was: 

Can I rotate one of those images by 90-degrees? 

But I don't want to use too much extra memory 

in doing that. 

That actually brings up 

a very interesting and relevant problem, 

which is essentially transposing a matrix. 

If you want to take a matrix of 

a two-dimensional array and rotate it 90-degrees, 

that means instead of listing it out row by row, 

you're listing it out column by column. 

In memory, there are several ways 

you can represent a matrix. 

Two of the most common are row order, 

where you list out the contents of row 1, 

the contents of row 2, the contents of row 3. 

You serialize the matrix that way.

Play video starting at :6:16 and follow transcript6:16

You can also list out the matrix in column major order, 

so listing out the columns 

one by one in memory one after the other. 

If you transpose the matrix, 

if you essentially rotate it 90-degrees, 

then you're just moving the elements of the matrix around 

in memory so that instead of 

the matrix being represented row by row, 

it's now represented column by column. 

This is extremely easy to do 

if you have a lot of memory because you can 

just allocate a new memory buffer and copy 

the elements into the new memory buffer 

in column major order. 

It's a lot more interesting 

if you don't have much extra memory, 

so if you have to rearrange 

the contents of your matrix in place 

so that you don't use more than 

say a constant amount of extra memory. 

We'll see what order 1 means, 

but basically that means 

just a constant amount of 

fixed amount of additional memory. 

That's the problem that we're going to look at. 

That is actually a very relevant problem nowadays, 

especially in the world of data 

analytics because a lot of times we 

use a matrix to encode a set of data.

Play video starting at :7:21 and follow transcript7:21

For example, you might encode 

n elements of data in the rows of the matrix and 

the columns of the matrix represent each 

of the features involved in describing our data elements. 

Abstractly, this is n points in 

an m dimensional feature space encoded in a matrix. 

If you wanted to do analysis on this dataset, 

maybe you'd want to do something 

like cluster the data elements, 

cluster the rows of the matrix. 

Oftentimes, instead of analyzing the data elements, 

you want to look at 

the dual problem of analyzing the features. 

Maybe I want to cluster the features 

instead of the data elements. 

Of course, you can do that 

by just transposing the matrix and 

applying whatever algorithm you are 

going to apply to the rows. 

There are actually some very practical applications for 

even the techniques we're going to talk about 

this first week in Module 1.

Play video starting at :8:15 and follow transcript8:15

Hopefully, it'll be a lot of fun. 

I'm looking forward to our ongoing discussion.