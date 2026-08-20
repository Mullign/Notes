Let's start building our toolbox of methods 

for analyzing performance of randomized algorithms, 

starting here with a discussion of average 

or expected running time performance. 

To do that, we're going to start with 

a very simple concept. 

That is: a random variable. 

As everyone here learned, 

hopefully in elementary school, 

a regular variable like x is 

just a placeholder for some specific value. 

So, similarly, a random variable is a placeholder 

for a value that materializes 

as the result of a random experiment. 

It's best to think of a random variable as actually 

representing an entire probability distribution. 

Maybe you can think of the 

value of the random variable as 

what you would get if you were to 

sample from that distribution.

Play video starting at ::49 and follow transcript0:49

For example, I could define a random variable X as 

the number that you see when you roll 

a six-sided die. And, in that case, 

X's underlying probability distribution 

would be a uniform distribution between one and six, 

and its expected value—or 

center of mass—would be three and a half. 

I could also define a random variable H, 

which is the number of heads you see when you 

flip a fair coin 100 times. 

H would have a distribution 

—it's called a binomial distribution— 

but with an expected value —or a center of mass—at 50. 

Of course, in this class, 

we're excited about analyzing randomized algorithms, 

so we're often going to define a random variable that 

corresponds to the running time 

of a randomized algorithm. 

In this case, for example, 

T is defined as the running time of 

randomized Quicksort when you 

apply it to a length-N array. 

Now, a random variable like T is likely 

to have a rather complicated underlying distribution, 

but, later on in this module, 

we will see that the expected value of T— 

the center of mass of that distribution— 

is on the order of and N log N.

Play video starting at :1:53 and follow transcript1:53

I've been using the phrase "expected value" 

a couple of times. 

Let's formally define what we mean by that. 

It's actually a very intuitive concept. 

It really is just the center of mass of 

a probability distribution. And, mathematically, 

that is nothing more than just a weighted average. 

So, the definition of expectation 

is that the expected value of 

a random variable X is 

just a sum over all the possible values, 

v, that X can take, 

weighted by the probabilities of 

X taking those respective values. 

As a couple of examples for computing expectations, 

let's define D as the maximum 

of the two numbers that you get when 

you roll a six-sided die twice.

Play video starting at :2:35 and follow transcript2:35

Here is the distribution underlying 

the random variable D. You see that it's, for example, 

very unlikely that D takes the value, 

one, because for that to happen, 

you'd have to roll a one twice, 

and that only happens with probability one out of 36. 

What's the expected value of D? 

Well, you just sum up 

all the possible values one through six that D can 

take and weight them by 

the respective probabilities of D taking those values, 

and what you end up with is 4, 17/36. 

It's— I guess, it's indeed where you'd 

expect to find the center of mass of that distribution. 

An even simpler example of 

a random variable is this random variable H right here. 

This is sometimes called 

a Bernoulli or an indicator random variable.

Play video starting at :3:21 and follow transcript3:21

It's a very common type of 

random variable that we'll see 

a lot throughout this course. 

Basically, it's a binary-valued random variable 

that just takes the value, one, 

to indicate whether or not 

a particular event has happened— 

in this case, flipping heads on a fair coin. 

So, H takes the value one if 

that happens, and zero if otherwise. 

I like the word indicator because it really 

indicates whether or not an event has happened. 

And, for these indicator random variables, 

computing expectation is really 

trivial because they only take two possible values. 

The expectation is one times the probability 

of the event for which they serve as an indicator, 

plus zero times— I guess, 

we don't even care because it's zero times something. 

So, what you get is that the expected value of 

an indicator random variable is 

just the probability of 

the event for which it serves as an indicator.

Play video starting at :4:12 and follow transcript4:12

That's a useful general principle to remember. 

One quick note, in terms of terminology 

—because I often see students making mistakes here— 

if you write probability of something, 

that something ought to be an event, 

like flipping heads on a coin 

or rolling a number 

higher than three on a die or something of the sort. 

If you write expectation of something, 

that something should be a random variable. 

So, be careful not to write expectation of an event, 

like expectation of flipping heads on a coin. 

Or, be careful not to write 

probability of a random variable. 

Those things don't make mathematical sense. 

Now, if you want to compute 

expectations of random variables, this formula, 

the definition of expectation 

is a perfectly reasonable thing to 

use for simple random variables 

like indicator random variables.

Play video starting at :5: and follow transcript5:00

It is not so useful if you're talking 

about the running time of randomized Quicksort, 

where the structure of 

such a random variable is extremely complicated. 

It's really hard to calculate 

the probability that the running time 

of randomized Quicksort is equal to some specific value. 

So, for complicated random variables, 

we need to move beyond just using the definition and we 

need more tools for helping us calculate expectations. 

Our go-to method here is 

a method called linearity of expectation. 

It's very powerful and very general. 

We're going to use it quite a bit over this semester. 

It stems from the fact that expectation 

is a linear operator.

Play video starting at :5:38 and follow transcript5:38

If you have the expectation of a constant times x, 

you can factor out the constant. 

If you have the expectation of 

a sum of two random variables, 

that can be decomposed into 

a sum of their respective expectations. 

This is actually really easy to show. If you 

just go back to the definition and rearrange the terms, 

you can actually prove these things quite easily. 

Now, the power of linearity of 

expectation lies in the fact that it always applies. 

There are no conditions like 

independence or whatnot that are required. 

It applies to any random variables, 

so it's a very general technique 

that we can use in many different situations.

Play video starting at :6:18 and follow transcript6:18

And, the way we typically apply it is we take 

a complicated random variable and we 

decompose it into components that are much simpler. 

So, maybe we take the running time 

of randomized Quicksort and 

we break that down into a sum 

of indicator random variables. 

And, that lets us compute 

the expected value of the complicated random variable 

as a sum of the expectations of 

the much easier-to-compute simple random variables. 

Just as an example of how that works, 

go back to our random variable H, 

which is the number of heads if you flip 100 coins. 

Of course, you're going to expect 

the answer to come out to 50. 

Your intuition is usually right when it comes to 

expectations, but how would we do that? 

We could, of course, go back and use the formula, 

but you'll find yourself in a bit more of 

a mathematically complicated situation 

than you might have hoped for, if you had done that.

Play video starting at :7:5 and follow transcript7:05

It's possible, but a 

bit more mathematically overwhelming. 

—Much easier is to decompose H into 

a sum of 100 indicator random variables, 

one for each individual coin, that tells us 

one or zero if that coin came up heads. 

Now, just applying linearity of expectation, 

you see that the expected number of heads in 

total is the sum of these indicators. 

Remember, that this expectation of 

an indicator is just the probability 

of its associated event, 

which in this case is 1/2. 

One hundred times 1/2 gives us 50, 

much easier than using the definition directly. 

So, I think the best thing to do at this point is just 

to get some practice using linearity 

of expectation to manipulate and calculate 

expectations of more complicated random variables. 

Let's go to our whiteboard 

and just work through a couple of examples. 

A couple of simple ones to start with— 

Suppose that you have N people that are all wearing 

hats. And, they take their hats off, 

they throw them up in the air, and 

everyone catches a random hat— 

So, you basically permute the hats.

Play video starting at :8:8 and follow transcript8:08

And, you'd like to know: What's the expected number of 

people that receives their original hat if you do this? 

If we switch over to our whiteboard, 

here we are trying to calculate the expectation of 

a possibly complicated random variable X that 

tells us the number of people receiving 

their original hat when N hats are permuted. 

It's always important, when you use random variables, 

to clearly define what your random variables mean, 

otherwise, you can get yourself in trouble trying to 

figure out their expectations if you're 

not quite sure what they actually mean. 

If you'd like to calculate the expected value of X, 

we can do that with linearity of expectation after we 

decompose X into a sum of simpler random variables. 

Here, I'll define an indicator random variable 

for each of the individual people. 

So, X is going to decompose into a sum of X_1 through X_N, 

where each of these indicator random variables, 

X_j, is going to be a one or a zero, 

a one indicating if 

the jth person receives their original hat 

and zero otherwise. 

What's the expectation of one of 

these indicator random variables X_j?

Play video starting at :9:30 and follow transcript9:30

Well, remember that the expectation 

of an indicator random variable is 

just the probability of 

the event for which it serves as an indicator. 

That's the event that 

the jth person receives their original hat. 

That's what we need to find the probability of. 

And, that's really quite trivial 

because there's N different hats. 

And so, there's a 1/N chance that you 

receive your original hat if they're randomly permuted. 

Now, using linearity of expectation, 

you know that the expected value of 

X is just the expected value 

of X_1 up through the expected value of X_N, 

all added up. And, that's just adding up 1/N N times, 

so you expect one person to receive their original hat.

Play video starting at :10:12 and follow transcript10:12

So, relatively straightforward, so far. 

Let's look at another example. 

This is pretty common in probability theory. 

You often have these balls and bins type problems. 

Suppose you throw N balls randomly into M bins, 

what's the expected number of 

balls landing in a specific bin? 

Of course, the answer is going to be N/M, 

but we'd like to show that more mathematically here. 

This might actually be a relevant problem 

in the world of algorithms if you have 

a load-balancing application where you have 

N jobs that you're 

randomly assigning to a set of servers.

Play video starting at :10:48 and follow transcript10:48

You'd like to know what's the average load 

imposed on any given server. 

If we want to show this 

in a bit more mathematically formal way, 

then we're trying here to 

find the expectation of a random variable X, 

where X represents the number of balls landing in— 

let's just say the first bin: Bin number 1. 

What's the expectation of X? 

Well, to figure that out, I can take, again, 

X and decompose it into 

a sum of much simpler random variables. 

They're going to be, again, 

indicator random variables— one for every ball. 

And, each one of those random variables 

is going to be valued with a one or a zero. 

The one is just going to indicate that a particular ball, 

the jth ball, lands in 

the bin in question— in the first bin.

Play video starting at :11:30 and follow transcript11:30

So, one if the jth ball lands in the first bin. 

And, zero otherwise. 

Now, all I need to do is calculate 

the expected value of one of these X_j's. 

Again, that's the probability of 

the event for which it serves as an indicator— 

so the probability that 

the jth ball lands in the first bin. 

And, I guess, there are M different bins, 

so the probability that 

any ball lands in the first bin is just one out of 

M. Now, easily, using linearity of expectation, 

the expectation of X is the sum of 

the expectations of these indicator random variables. 

And so, that's going to be N*1/M or N/M, 

exactly the result that we would have trivially expected.

Play video starting at :12:21 and follow transcript12:21

These are a few very simple examples, 

just illustrating how we go through 

the motions of applying linearity of expectation. 

Let's maybe look at maybe a more algorithmic example. 

Suppose that we want to build a histogram. 

Here's an example from the world of data analytics. 

You have N values, 

v_1 through v_N, 

and you'd like to just build a 

histogram with some number of bins— 

maybe 10, or 15, 

or 20 bins. That's really easy to do. 

You can scan through your values, 

find the biggest one, and 

that defines the range of numbers.

Play video starting at :12:53 and follow transcript12:53

Let's suppose the numbers are all non-negative, 

so they range from zero up to 

whatever that maximum value is. 

You can divide that range up by 

however many bins you have and then just scan through 

the values one more time and increment the counts 

of how many things land in each bin. 

In just linear time, it's pretty easy to 

calculate and create a histogram like this. 

However— Let's add some interesting twist to it. 

What if the values are arriving 

online in real-time, one by one, 

and you'd like to maybe keep a histogram 

like this up to date moment by moment? 

Maybe you're visualizing it as the numbers come in and 

you'd like to see in real-time 

how the histogram is changing. 

Maybe, for example, you're visualizing 

daily temperature data and you'd like to 

have an animation that shows that, in the summer, 

you have a lot of 

higher temperatures and then, as 

you transition more to fall and winter, 

you start getting more and more lower temperatures, so 

the shape of the histogram is 

going to change in real-time.

Play video starting at :13:51 and follow transcript13:51

How much total time would you spend keeping 

the histogram up-to-date as 

each successive value arrives? 

This is going to take a little bit 

more work because we can't just 

do one calculation in 

a big batch at the end that builds the histogram. 

We have to keep the histogram up-to-date as we go. 

If we think about it, it's 

a pretty easy process for 

each value that arrives in sequence, 

usually, you only have to spend 

a constant amount of work because you have to figure out 

what bin that value goes into and 

just increment the count for that particular bin. 

It just takes you constant time 

to process most of the incoming values. 

The exception is that, if the value 

that comes in is a new maximum, 

—it's the biggest value that you've seen so far— 

then that basically causes you to do a lot of work. 

You have to rebuild the entire histogram from scratch, 

in that case, because that redefines the bin boundaries.

Play video starting at :14:45 and follow transcript14:45

Because the bin boundaries are 

defined by taking the range from zero up to 

the maximum value and equally 

subdividing that up into a certain number of bins. 

If the maximum value changes, 

then the definition of the bin ranges, 

that also changes. 

And so, you have to go through all the values you've 

seen so far and redeposit 

them into their correct bins because, now, they 

belong to possibly different bins 

than they were in before. 

And so, you recompute the counts of all the bins. 

That's going to take you order of j time, I guess, 

if this is the jth value that's caused this 

rebuild to happen. So, what happens here? 

Well, in the worst case, things are actually pretty bad 

because, say you're processing 

a series of values in increasing order.

Play video starting at :15:27 and follow transcript15:27

Every single value in that case is going to be 

the new maximum and is going to 

cause the expensive case to happen. 

In that case, you're actually going to get 

a quadratic worst-case running time. 

But what about something more on 

the level of an average performance analysis? 

Here, the algorithm that we're 

dealing with is not a randomized algorithm, 

but we're going to consider the 

randomization to be in the input. 

This is more of an average case analysis. 

What happens, for example, 

if the N values arrive in random order?— 

So, you randomly permute them and then feed them in, 

one by one, into this algorithm. 

What do we expect the running time to be in this case?

Play video starting at :16:6 and follow transcript16:06

If we go and just do the math here, 

we would like to find the expected total running time we 

spend processing these values 

as they arrive one by one in an online fashion. 

But, what is that expectation? 

Well, again, I can decompose that 

into a sum of hopefully simpler things. 

So, T is going to be decomposed into a sum of T_1 up to T_N. 

In this case, these aren't going 

to be indicator random variables, 

but rather these are just going to be the times we 

spend processing each of the N different elements. 

This is actually going to hearken 

back to what we talked about in 

the first module of looking at 

running time on a per-element basis. 

Here, each of these T_j's is going to be defined 

as the running time that you 

spend processing just the jth value as it arrives.

Play video starting at :17:6 and follow transcript17:06

So, what is that running time? 

We've already talked about that. 

The running time for processing the jth element— Well, 

it's expensive if that 

jth element is the maximum you've seen so far. 

Remember, that's going to be on the order 

of j because you have 

to reprocess all the elements 

up to that point in that case. 

Oder j if V_j is 

the maximum of V_1 

up through V_j. —if 

it's the biggest thing you've seen so far. 

Otherwise, it's just constant time. 

What is the expectation of one of 

these T_j random variables going to be?

Play video starting at :17:46 and follow transcript17:46

Well, there's only two possible cases. 

According to the definition of expectation, 

it could possibly take the value order 

j with a probability of— 

Well, what's the probability of this particular event? 

That V_j is the largest thing that I've seen so far. 

And then, the other case is it could take constant time, 

and that's weighted by the probability of 

that not happening. 

Just to simplify things, 

I'm going to say that that probability is at most one 

because any probability is at most one. 

This term right here is still going to contribute 

just order 1, a constant. 

Really, the key is, what's the probability of V_j, 

the jth element that I 

process, being the largest one so far?

Play video starting at :18:33 and follow transcript18:33

That's actually pretty easy to see because each of 

the elements, from V_1 up through V_j,— 

Each of those is equally likely to be the maximum in 

that range because I'm dealing 

with a completely random permutation. 

There's exactly a 1/j chance 

that V_j is the largest of those j elements. 

The 1/j here cancels the order j running time, 

and so this term also 

ends up contributing just a constant. 

Each of these expected values 

of all the T_j's is constant. 

You expect a constant amount of work 

to be spent on each individual element. 

It's interesting, because of the cancellation here, 

each element gets more and more 

expensive if the expensive case happens, 

but it becomes less and less 

likely that those expensive cases happen. 

Those things offset, and you actually end up spending 

only a constant expected amount of 

work on each individual element.

Play video starting at :19:30 and follow transcript19:30

So now, it's easy to finish off our analysis. 

The expected value of T is just the expected values 

of how much work we spend per element on each element. 

And, that was a constant amount per element times N elements. 

And so, that's going to give us just a linear time 

in expectation overall. 

This is actually quite interesting. 

There's a somewhat dramatic discrepancy between 

the worst case and the average case running time here. 

Maybe this motivates us to be very careful when we do 

empirical analysis of algorithms because 

a lot of times if you're —just for simplicity— 

maybe feeding random inputs to 

your algorithm to measure the performance, 

you might see a much better performance in 

those cases than you could in the worst case.

Play video starting at :20:16 and follow transcript20:16

So, just a cautionary tale here.![[TCFA525HR9GW5Hfcqd91fw_c033d332c23c48d18ae14e18b7079ff1_Expected-Running-Time.pdf]]