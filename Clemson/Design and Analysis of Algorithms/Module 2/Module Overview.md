Welcome to Module 2 on the core subject 

of randomization and randomized algorithms. 

There's a lot of cool stuff we're going to be 

covering in this rather extensive module. 

Our main goal is to build out our toolbox—so to speak— 

of techniques for designing 

and analyzing randomized algorithms, 

and also—I guess— for performing 

average case analysis of non-random algorithms. 

In doing this, we will showcase 

a wide range of prominent randomized algorithms. 

Many of them are very elegant and quite 

useful for addressing a wide range of applications. 

Let's maybe briefly introduce 

the two main types of 

randomized algorithms that we tend to study. 

They have cute names drawn from 

the world of gambling, I guess.

Play video starting at ::54 and follow transcript0:54

A Monte Carlo randomized algorithm 

is a randomized algorithm where 

the running time is deterministic, 

but the algorithm could potentially make 

a mistake and output the wrong answer if you're unlucky. 

So, the goal here is typically to design the algorithm in 

a way that minimizes 

the probability of outputting the wrong thing. 

You want the output to be correct with high probability. 

We'll actually define what we mean by 

with high probability later in the module. 

The other main type of 

randomized algorithm that we're going to talk 

about is the so called Las Vegas randomized algorithm. 

Here, the randomization shows up in the running time. 

The running time is actually 

given by a probability distribution.

Play video starting at :1:34 and follow transcript1:34

If you're unlucky, the algorithm runs slowly. 

If you're lucky, the algorithm runs much faster. 

Here we typically analyze 

either the expected running time 

—what you expect on average the running time to be— 

or you'll like to have a bound on 

running time that holds with high probability— 

so, maybe you run an order N squared 

with high probability if there is 

a very minuscule probability that you 

don't run in order N squared time. 

There's a very tiny amount of 

mass in the tail of this distribution. 

A lot of the same techniques that we're 

going to study can also be used to 

analyze the average case performance of 

non-random algorithms, of course, as well. 

That goes hand in hand with our study of 

Las Vegas randomized algorithms. 

If we look at the structure of 

this module and what it's going to contain— 

Just like with Module 1, 

we'll have some simple practice exercises so that 

you can make sure you're understanding 

the core concepts in the module.

Play video starting at :2:34 and follow transcript2:34

We're also going to include 

a coding lecture where we talk about 

a class of data structures called 

priority queues that are very 

prominent and very fundamental. 

We'll see a very elegant example 

of a randomized priority queue 

called a randomly mergeable binary heap, 

which should be a lot of fun. 

Then for our enrichment lecture (optional, of course) 

we'll talk about some interesting connections 

with information theory. 

There are lots of ideas in that space. 

This is relevant because it goes 

hand in hand with probability theory and randomization. 

—Lots of interesting ideas here, involving 

variants of entropy, data compression, 

things like mutual information; 

lots and lots of interesting applications 

to problems in areas like data analytics. 

That should be a fun discussion that we can have. 

This particular topic, randomized algorithms, 

we're introducing this module 

very early in the curriculum.

Play video starting at :3:27 and follow transcript3:27

There's a good reason for that. 

Because a lot of the techniques that we're going to 

introduce and a lot of the ideas in 

randomized algorithm analysis are just so fundamental 

(We're going to be seeing them throughout the entire course), 

that it makes sense to introduce 

them as early as possible. 

So, that's why this is module number 2. 

Maybe a few other quick notes. 

This is probably going to be a little bit more on 

the analytical side when it comes to different modules, 

so we're going to see a little bit more mathematical content 

in this module. 

Please don't let that scare you or intimidate you. 

One of the goals of the module is to show that 

randomized algorithm analysis can be 

quite approachable if you use the right tools.

Play video starting at :4:7 and follow transcript4:07

Hopefully, we will see that 

these algorithms are not intimidating, 

but, in fact, their analysis can be 

actually quite simple and quite elegant. 

Looking forward to a lot of cool ideas and 

cool discussion in this module. Let's get started.
![[../Module 1/VFJZKGlES8qs89FYQDCaUw_ffcdfe9aba2042b3920e3b0c9390c7f1_Module-2-Overview.pdf]]