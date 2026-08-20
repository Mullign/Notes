[MUSIC] ![[37achWS6QKeVZjlCpUwVRA_93c04e55f22f4ce98db44384a962a9f1_Geometric-Random-Variables.pdf]]

Any of our analyses so 

far have involved decompositions into indicator random variables. 

And beyond indicator random variables, 

there is actually one other primitive type of random variable that we see very often 

in the analysis of randomized algorithms, that's the geometric random variable. 

So in this video, we're going to spend a few minutes talking about geometric random 

variables and related ideas. 

So these types of random variables, 

they arise from a very straightforward type of algorithmic process. 

Imagine you have an algorithm that performs repeated independent trials, and 

each trial succeeds in some way with probability p. 

So a geometric random variable is one that describes the number of trials 

you perform up to and including the first successful trial. 

We'll show in just a second that the expected value of such a variable is kind 

of what you would naturally expect it to be.

Play video starting at ::59 and follow transcript0:59

It's 1 over the success probability. 

So if you keep rolling a dice until you see the number 3, 

the probability of success is one-sixth, and you expect six trials. 

So it's a fairly intuitive and natural concept. 

We can also put inequalities on things. 

So if every trial succeeds with probability, at least p, then the expected 

number of trials up to and including success is going to be at most 1 over p. 

And the prototypical example here of this phenomenon in action is, 

if you take a Monte-Carlo randomized algorithm. 

Remember Monte Carlo randomized algorithms, they can make mistakes, 

they can fail to output the right answer.

Play video starting at :1:41 and follow transcript1:41

But suppose you have such an algorithm that succeeds with probability, 

at least say one-fifth. 

And suppose further that you can actually tell if the algorithm has failed or 

succeeded. 

In this situation, 

what you commonly do is just keep rerunning the algorithm until it succeeds. 

And since the probability of success on each trial is at least a fifth, 

you expect to only have to run the algorithm at most five times. 

So a very standard sort of situation where geometric random variables come 

up expected trials until success. 

It's relatively straightforward to prove the upper bound of 1 over p on 

expected value. 

One way we could do that is we could take our geometric random variable and 

decompose it into a sum of indicator random variables, 

actually an infinite sum, in this case.

Play video starting at :2:23 and follow transcript2:23

Each of those indicator random variables is just going to 

tell me if the algorithm is still running by a particular iteration. 

So xj is set to one if the algorithm is still running by the jth iteration. 

If you want a picture, maybe down below, it would appear that this would correspond 

to an algorithm that finally succeeded by the fifth iteration. 

The first four were failures. 

So in this case, x1 through x5 would be set to 1, and 

x6 onward would be set to 0. 

So if I want to use linearity of expectation to calculate the expected 

value of x, all I need to do is calculate the expected values of 

these indicator random variables. 

That's relatively straightforward.

Play video starting at :3:3 and follow transcript3:03

Remember, the expected value of an indicator random variable is nothing 

more than the probability of the event for which it serves as an indicator. 

So the probability that we're still running by the jth iteration, 

and if we're still running by the jth iteration, 

that means the first j minus one iterations had to all have failed. 

And so what I'm really looking at here is the probability that I 

had failures on the first j minus one iterations. 

This I can conveniently decompose because I'm running independent iterations. 

So the probability that you fail on the first j minus one iterations, 

that breaks down into a product of the probability that you fail on the first 

iteration times the probability that you fail on the second iteration, dot, dot, dot, 

up until you fail on the j minus first iteration. 

Each of those individual probabilities is at most one minus p. 

So I get 1-p to the j-1.

Play video starting at :3:56 and follow transcript3:56

And then if I add those all up to find the expected value of x, 

I end up with a geometric series. 

Maybe not surprising, 

because this is a geometric random variable that I'm analyzing. 

So I just have to add up a geometric series. 

Many of you may know just a formula for doing that. 

I'm not really big on formulas. 

And so let me show you a trick that I often use for 

adding up any series that has kind of a geometric character to it. 

So if I recall the series that I'm adding up, let's call S, 

that was (1-p) to the 0 + (1-p) to the 1 + (1- p)^2 and so on.

Play video starting at :4:34 and follow transcript4:34

What I'm going to do here is sometimes called shifting as a technique. 

I'm going to take the series and 

I'm going to multiply it by the common ratio of the series. 

And so 1-p times the series is effectively going to take each term and 

kind of shift it over by 1. 

So (1-p)^0 is going to turn into a (1-p)^1, 

and the (1-p)^1 term is going to turn into (1-p)^2. 

And so on. 

And conveniently, now I can subtract one of these from the other and 

I get a lot of cancellation. 

So on the left hand side, I just get p times s.

Play video starting at :5:9 and follow transcript5:09

On the right hand side, everything cancels except the (1-p)^0, 

which is otherwise known as 1. 

And so, clearly, the sum of this series is just 1 / p. 

So relatively straightforward to add up any geometric series or 

even some slightly more interesting series, 

as long as they have kind of a geometric character to them. 

You can often successfully apply this technique of shifting. 

Okay, let's maybe talk about some applications of geometric random 

variables. 

Here's an easy one to start with. 

Suppose I would like to sample a point uniformly and 

at random from this yellow circle.

Play video starting at :5:45 and follow transcript5:45

It may seem hard to sample from a circle, so instead, 

why don't we draw a sample from the enclosing blue square? 

That's much easier, because I can just take a uniformly distributed x coordinate 

and a uniformly distributed y coordinate to get a sample from the square. 

So imagine now I'm just throwing darts at that blue square, and 

I succeed if one of those darts lands also in the circle, 

because it gives me a uniform sample over the circle. 

So how many darts do I have to throw? 

Well, the probability of success here is PI over four, 

the ratio of the area of the circle to the area of the square. 

So the expected number of trials involved here is the reciprocal of that 4 

divided by PI. 

So just a constant number of trials to successfully sample from that circle.

Play video starting at :6:28 and follow transcript6:28

Sampling, in general, is an incredibly important algorithmic topic in areas like 

data analytics and simulation. 

And as a result, we will be talking a lot about sampling throughout this course. 

At this point, since applications like machine learning involve very high 

dimensional data sets, it's probably worth a quick aside to revisit our preceding 

rejection sampling approach and look at what happens as dimensionality increases. 

And unfortunately, the news is not good here. 

If you look at the ratio of the volume of an n dimensional sphere to that 

of its enclosing n dimensional cube, 

that ratio actually tends to zero pretty quickly as dimensionality increases. 

So you can throw all the darts you want at, say, 100 dimensional cube, and 

pretty much none of them will land in the corresponding enclosed 100 dimensional 

sphere, making the preceding approach incredibly inefficient at sampling 

from spheres in the high dimensions. 

So I guess what approaches are effective for 

sampling from high dimensional spheres?

Play video starting at :7:28 and follow transcript7:28

Maybe I'll give you one very simple approach that people do tend to use. 

If you want to sample maybe a random point from the surface of a unit sphere in n 

dimensions, that's kind of equivalent to sampling just a random unit vector in 

n dimensions that just points in some random direction in space, 

then an easy way to do this is you pick each of the n components of your 

vector independently from a gaussian distribution. 

And that makes the entire vector effectively sampled from an N-dimensional 

multivariate Gaussian distribution that's known to be a spherically symmetric distribution. 

So then you just normalize your vector, and you are left with a vector that is 

randomly sampled from the surface of an N-dimensional unit sphere. 

In general, if you're writing algorithms that deal with high dimensional spheres, 

those are somewhat weird objects. 

Your intuition from two and three dimensions doesn't 

always directly apply to what happens in high dimensional settings. 

This is kind of a general principle in high dimensions, 

kind of non intuitive things sometimes happen, and 

we'll be mentioning that throughout the course as well.

Play video starting at :8:31 and follow transcript8:31

But for example, like in the case of a high dimensional sphere, 

almost all of its mass lives in a thin shell near the surface. 

So these are somewhat maybe nonintuitive objects. 

So just exercise proper caution when designing algorithms that involve 

these types of objects. 

Okay, moving along to other simple applications of geometric random 

variables. 

Suppose I have a biased coin. 

Maybe it comes up heads with probability 1/7. 

And I would like to simulate a fair coin using a constant number of expected flips 

of the biased coin.

Play video starting at :9:2 and follow transcript9:02

There are several ways to do that pretty easily. 

So one way is you flip the coin twice, and 

out of the four outcomes that you can have, two of them, heads, tails, and 

tails, heads, have the same probability of occurring. 

And so I can map those two heads and 

tails of the fair coin that I'm trying to simulate. 

If instead I get heads heads or 

tails tails, then I just do a redo, I flip the coins twice again and 

I keep doing that until I get either the outcome head tails or tails heads. 

What about the reverse problem, where I'm given a fair coin, and 

I would like to simulate a biased coin? 

So maybe I would like to simulate a coin that comes up heads with probability 

one 7th. 

So it turns out we can also do this with only a constant number of expected 

coin flips.

Play video starting at :9:45 and follow transcript9:45

In fact, only two coin flips of our fair coin in expectation are needed to do this. 

So, a couple ways to think about this process. 

My favorite way is to take a unit interval between zero and one, and 

to divide that up into two segments, one of them corresponding to heads that has 

length 1/7, and one corresponding tails that has length 6/7. 

So those numbers are the probabilities of the events that we're trying to simulate, 

then I just pick a random real number, x on the unit interval, and whichever 

segment x lands on that corresponds to the outcome of my biased coil. 

So the trouble here is this requires sampling a real number between zero and 

one, and all I have is a fair coin. 

So how do I sample a real number using only a fair coin? 

It turns out what I can do is I can flip the coin to generate 

the successive binary digits that make up x, 

because flipping the coin gives me effectively a zero or a one.

Play video starting at :10:40 and follow transcript10:40

So I'm going to flip the coin to generate the bits in x and 

I'll keep doing that until it becomes kind of unambiguous. 

If x lives in the heads or tails region of the unit interval, maybe a nice 

way to picture this is kind of think of it as walking down a binary tree. 

So every single I start at the root, every single coin flip I make, 

I go either left with heads or right with tails. 

So heads corresponds to a 0, tails corresponds to a 1, and so a series of 

coin flips is going to kind of look like a path down this little binary tree. 

So I start out, I flip the coin once and I see maybe heads. 

So I take the zero path here. 

And so now x starts with a zero after the decimal point.

Play video starting at :11:21 and follow transcript11:21

None of the remaining digits though are specified. 

So all I know is that X lives in the first half of my unit interval. 

And it still isn't clear if my outcome is going to be heads or 

tails because, well, both heads and tails is a possibility. 

So I flip the coin another time, maybe now I flip tails. 

So I add a 1 to my representation of x. 

X is now 0.01 and then some unspecified digits. 

That means that x now lives in the second quarter of the unit interval.

Play video starting at :11:52 and follow transcript11:52

And now conveniently, there's no ambiguity. 

I'm going to output tails. 

I don't need to generate any more digits of x because whatever those digits 

come out as, x is going to live in the segment that corresponds to tails. 

So I can stop at this point. 

So that's my algorithm. 

How many expected coin flips do I use? 

It turns out only two, because if you think about right before any coin flip, 

there's kind of a good and a bad outcome.

Play video starting at :12:18 and follow transcript12:18

So if I'm sitting maybe on this node right here, if I go left, 

that's kind of a bad outcome, because it lands me in a part of the unit interval 

that there's still ambiguity about whether I'm in heads or tails. 

The other direction, though, is unambiguous. 

If I flip tails and I end up in this region, 

I can stop because there's no more ambiguity. 

So at every single coin flip that I make, 

one of the directions will be an ambiguous direction. 

It'll lead to a further ambiguity and I'll need to keep flipping more coins. 

The other direction, though, will lead to no ambiguity. 

I can terminate.

Play video starting at :12:52 and follow transcript12:52

So every step there's a one half chance that I terminate, and so 

I only expect two coin flips overall. 

There's maybe another nice way to think about exactly this same process. 

So imagine that I write out 1/7 in binary. 

I'm really trying to figure out if the value of x that I pick is less than or 

greater than 1/7, because that tells me if I'm in the heads region or 

the tails region. 

And so you can think of this as generating the digits of x and stopping when 

it becomes clear that x is either bigger than or smaller than 1/7. 

So what I'm going to do is just keep generating binary digits of x 

as long as they agree with the binary representation of 1/7. 

But I stop when I finally generate a digit of x that's different from 

the corresponding binary digit in one 1/7th.

Play video starting at :13:40 and follow transcript13:40

And at that point I can resolve whether x is bigger than or smaller than 1/7. 

So in this example here, x generated a digit of one. 

The digit in 1/7 was 0. 

So that means that x is going to be bigger than 1/7. 

It doesn't matter what the rest of the digits are. 

At this point, we know that x is bigger than 1/7 and 

it's going to end up in the tails region. 

So because there's always a one half chance of generating a different digit 

from the corresponding digit of 1/7 and stopping, you expect only two coin flips.

Play video starting at :14:11 and follow transcript14:11

So this is just an alternate way of looking at what is essentially the same 

process. 

There's nothing magical from the previous algorithm that requires us to sample 

between two different possibilities, like heads or tails. 

You could also generalize the same exact approaches to sample from a set of n 

possibilities, each having a corresponding probability. 

So maybe I would like to sample a random vowel with probabilities proportional to 

how often they occur in English language text. 

So e is the most frequently occurring vowel. 

It occurs about one third of the time sometimes. 

This is called roulette wheel selection.

Play video starting at :14:45 and follow transcript14:45

You can imagine this roulette wheel divided up into sectors that correspond 

to the objects you're trying to sample, and the width of 

each sector corresponds to the probability of each object you're trying to sample. 

So spinning the wheel would generate a sample with the appropriate probability 

distribution, so we can really generalize exactly the approaches from the previous 

slide to work here. 

I can pick a random x on the unit interval between zero and one, and 

wherever x lands, whatever segment that lands on, that determines the object 

that I have sampled. So easily in linear time. 

I can generate a sample from among n different objects this way. 

Actually, if I want to do repeated samples, if I know that I'm going to be 

drawing several samples from the same distribution, then now I get some more 

interesting algorithmic questions of how can I set things up? 

Maybe with a little bit of preprocessing so that I can.

Play video starting at :15:37 and follow transcript15:37

I can now do a whole bunch of samples quickly. 

And one easy idea that comes to mind here is that I can basically 

use a binary search to figure out which segment x belongs to. 

That basically boils down to binary searching in the sorted array of 

the dividing points that delineate my different segments. 

If I binary search that array, I'll figure out where x lives, 

what segment it lives on. 

So after setting up that array in just logarithmic time, 

I can generate sample after sample. 

In fact, there's even a way to do this in constant 

time per sample after a linear amount of preprocessing. 

That's a little bit more interesting of a question.

Play video starting at :16:16 and follow transcript16:16

So maybe I'll leave that as an exercise for the reader. 

It's a little bit challenging, but give that some thought. 

It's a fun question. 

If we go back to our vantage point of flipping a coin to generate x, 

that actually leads us to, gosh, I have now recursive asides. 

So this is an aside squared that we're going to revisit in our enrichment lecture 

when we talk about things like entropy and whatnot. 

But this actually is also related to data compression and variable length coding. 

You can imagine, E is very frequent.

Play video starting at :16:49 and follow transcript16:49

So if I wanted to generate a set of codes, 

binary numbers that are of different lengths that represent AEIO and U, 

then I would like a really short code to represent E. 

Because E occurs often. 

I don't want to waste a lot of space representing E. 

I could afford to spend a larger number of bits on a code that represents U because 

it doesn't occur that often. 

And so a lot of times when you try and compress data, you assign variable length 

binary codes to the different entities that you're trying to code for, so 

that more frequently occurring elements end up with much shorter codes. 

And one way to do that, this is what I've depicted here, 

is related to a technique called arithmetic coding. 

It's kind of a close relative of Huffman coding, if you've encountered that before.

Play video starting at :17:35 and follow transcript17:35

So you can basically kind of superimpose this little binary tree. 

And again, the same sort of idea. 

You walk down the tree until you reach the point where things are unambiguous. 

So, for example, the code for E would be zero one, 

because if you take the zero step and the one step, 

now you live in a region of the unit interval that unambiguously codes for E. 

So if you assign E a code of 01, I guess A would be assigned a code of 00, and 

you probably need one more 0 before you're unambiguous. 

That lets you basically translate a string of vowels into a binary representation, 

and it lets you decode that binary representation back into a string of 

vowels, basically just by walking down the tree. 

And anytime you hit a leaf, that tells you what vowel you're talking about.

Play video starting at :18:24 and follow transcript18:24

I won't say too much more here, because we will cover topics like information theory, 

entropy, data compression and whatnot in our enrichment lecture in this module. 

So at this point, I think I'd like to just unstack all of these asides and 

come back to another prominent example of an application involving geometric random variables. 

So imagine that you want to just spread a message around a network of n machines. 

And one simple way to do this is to take the message, and in each step, 

you just send it to a random machine, and you just keep doing that. 

Think of the message as a token that just jumps around from machine to machine. 

And I'm interested in how many expected steps this takes before every 

machine has heard the message. 

If you want to think about it as a random walk around the network of machines, 

I'm looking for the so called expected cover time of that random walk.

Play video starting at :19:16 and follow transcript19:16

There are lots of applications that involve this sort of fundamental process, 

and it's an interesting process to study because it involves a random variable that 

actually decomposes into a set of geometric random variables instead of our 

usual indicator random variables. 

So the setup here is I'd like to analyze the expected total time it takes for 

the message to visit every machine. 

I'm going to break that up into geometric random variables that kind of 

correspond to the time taken in each so called phase of the algorithm. 

Where I have Tj is the amount of time it takes during the jth phase of 

the algorithm, where j minus one of my machines have heard the message and I am 

passing it around from machine to machine, waiting for the footprint to expand to. 

Now, J machines having heard the message, and these phases actually get slower and 

slower as I go. 

So the very first phase takes just one step, because the first step, 

you definitely contact a machine that hasn't heard the message and you're done. 

But towards the end, if you look at the last phase, in the last phase, 

N - 1 machines have heard the message.

Play video starting at :20:24 and follow transcript20:24

Only one machine hasn't heard the message, and you're sending the message around 

randomly in hopes that that one holdout machine hears the message. 

In each step, there's only a 1 out of N chance of success that you randomly send 

a message to that one final machine. 

And so the expected number of trials until success is actually going to be N in 

that case. 

That's a very inefficient phase. 

If you look at phase three, for example, in this phase, 

I guess two machines have heard the message, n - 2 machines have not, 

and you're passing around the message in hopes that one of those n - two 

hold out machines finally hears the message that would end the phase. 

And so here the probability of success is N - 2 out of N, 

because there's N - 2 kind of good machines that you could send a message to out of N. 

So the expected number of steps in that phase is again the reciprocal.

Play video starting at :21:14 and follow transcript21:14

It's N / (N - 2). 

So I just have to add up all of these expectations to get 

the total expected number of steps that this takes. 

And if you look at what happens, it's basically N, you factor out the N, 

you get N times a harmonic series. 

Harmonic series, as we know, adds up to something close to the natural log of N. 

And so that's what gives us N log N as our total expected number of steps. 

So final thing I wanted to do here is actually prove the randomized reduction lemma. 

That's actually straightforward and quite easy to do using 

linearity of expectation and geometric random variables.

Play video starting at :21:50 and follow transcript21:50

So imagine, just to put some concrete numbers on things that I have, 

an algorithm that in every step independently reduces the size 

of our current problem by one half, with probability at least one fourth. 

Remember that all I need is for these two numbers to just be fixed constants for 

the randomized reduction lemma to apply and 

tell me that I should take in expectation a logarithmic number of steps. 

So let's see why that's the case. 

If we look again at kind of phases of the algorithm, think about kind of the first 

phase where we're doing successive iterations of the algorithm, waiting for 

that first successful phase that causes a reduction. 

And since reduction happens with probability at least one fourth, 

we expect at most four steps before we hit our first reduction. 

And then again we expect another four steps before we hit our second reduction, 

and so on. 

How many reductions do you need before you're done?

Play video starting at :22:44 and follow transcript22:44

Well, every reduction reduces by half. 

And so after log base 2 of N reductions, you are definitely terminated. 

The algorithm has reached a base case at that point, and so you can upper 

bound the total number of steps needed by the algorithm by the number of 

steps needed in the first phase, kind of the steps up until the first reduction, 

plus the number of steps in a second phase. 

That's kind of the steps leading up to the second reduction after that, 

all the way up to X log base 2 of n, 

that's in the log base 2 of Nth phase, looking for that reduction. 

So after that many reductions, you're definitely finished with the algorithm. 

And we know that each of these expectations involves the geometric random variable. 

They're all at most 4.

Play video starting at :23:25 and follow transcript23:25

And so the total number of expected steps is at most 4 log base 2 of N. 

That's on the order of log of N, and that would still be on the order of log of N 

if I had started with different constants than 1/2 and 1/4, 

they just disappear as hidden constants in my big O running time. 

And so I have just proved the randomized reduction lemma in a fairly 

straightforward way, using geometric random variables. 

[MUSIC]![[screenshots/Screenshot 2025-09-06 at 9.41.33 am.png]]