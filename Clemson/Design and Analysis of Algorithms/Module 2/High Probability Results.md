![[ePN_fy0ERBuNl9OMlDUYyQ_0c2e2391c6f04d1c82f747b8ae3a80f1_NEW-High-Probability-Results.pdf]]I've been using the phrase with high probability, 

a fair amount in this module already, 

it is probably an appropriate time to 

define what that means more properly. 

Along the way, we'll also see 

a number of interesting ideas 

and tools we can add to 

our toolbox for analyzing randomized algorithms. 

To begin with, let's go back to the basics and talk 

about what is an event in probability theory. 

When you have some random trial or a random experiment, 

the fundamental result of that is called an outcome. 

If I say roll a six sided die, 

there are six fundamental outcomes, 1-6. 

An event is just a set of outcomes. 

Maybe event A here is the event that I roll 

an odd number that contains the outcomes, 1,3 and 5.

Play video starting at ::53 and follow transcript0:53

Since events are just sets of outcomes, 

I typically will use set notation 

to describe relationships between events. 

A intersect B, that's the event 

that both events A and B occur. 

A union B, that's the event that 

one or the other or both occurs. 

There's something interesting 

mathematically that you can say 

about both intersections and unions of events. 

Let me start with maybe unions of events. 

If I want to calculate the probability 

of a union of two events, 

the probability that either A or B happens, 

then that's easy to do. 

In fact, the Venn diagram 

here in the corner suggests how to do it.

Play video starting at :1:31 and follow transcript1:31

You take the probability of A plus the probability of B, 

and then you've subtracted 

out the part you've double counted. 

You've double counted the part in their intersections. 

I subtract out the probability of A intersect B. 

Sometimes just as a crude upper bound, 

we just take the probability of 

a plus the probability of B 

and ignore the fact that we're 

double counting the intersection. 

This is sometimes called the union 

bound or Boole's inequality, 

and it's used very often 

in randomized algorithm analysis. 

In fact, we often use 

the same idea when we're 

looking at the union of not two events, 

but of n events. 

If we have a crazy looking Venn diagram that 

describes the relationship between n different events, 

Then we can exactly calculate the probability of 

their union using the principle of inclusion exclusion.

Play video starting at :2:22 and follow transcript2:22

It's a nice idea in mathematics, actually, 

where you add up the probabilities 

of the events just like before, 

but now I've overcounted things. 

I have to subtract out the probabilities 

of all of their pairwise intersections, 

but now I've actually undercounted things. 

I need to add back in the probabilities 

of all the three tuples of 

events and then subtract out 

the probabilities of all the four tuples of events, 

and I alternate adding and subtracting in this fashion. 

That will actually give me an exact expression for 

the probability of this union of n events. 

However, it's a pretty complicated formula. 

It involves exponentially many terms. 

Oftentimes here, we also just 

use the cruder union bound or 

Boole's inequality to get an 

upper bound on the probability of that union.

Play video starting at :3:9 and follow transcript3:09

We just pretend that all of 

these complicated terms don't exist and we upper 

bound the union of N events by 

just the sums of their respective probabilities. 

Let me tell you maybe one very prototypical use case 

for this type of bound. 

Imagine that I have 

a complex machine made up of n individual parts. 

If I look at any one part, 

the probability that that one part itself fails is say 

1/2N and I'm interested 

in what's the probability that the whole machine fails? 

Well, the machine fails if any one of its parts 

fails and so the event that the entire machine fails, 

that's actually a union of n events. 

It's the union of the event that Part 1 

fails and the event that Part 2 fails, and so on. 

I can use the union bound to 

upper bound that probability by 

just the sums of the probabilities of 

failure of the individual n events.

Play video starting at :4:3 and follow transcript4:03

Each of those is at most 1/2N, there's n of them, 

and so overall, 

my machine fails with probability at most 1/2. 

Now, if I look at this more in 

the context of algorithm analysis, 

I don't have a machine with parts, 

but instead maybe I have an input 

consisting of n different elements of data. 

Now instead of a part failing, 

I could think about what's the probability that 

my randomized algorithm incorrectly 

processes some element of data? 

Maybe there's a failure on some element of data, 

a probability that most 1/2n 

and using the same analysis, 

I can conclude that the entire algorithm 

fails with probability at most 1/2 

because that's a union of the events 

that it fails to process Element 1 correctly, 

and it fails to process Element 2 correctly and so on. 

We'll use union bounds a lot for this type 

of application when analyzing a randomized algorithm. 

Let's now turn our attention to 

probabilities of intersections of events. 

Looking at the probability that both A and B occur.

Play video starting at :5:7 and follow transcript5:07

Very common situation here is that we can decompose 

that probability into a product 

of the probability of A and the probability of B. 

If and only if A and B happened to be independent events. 

Independence means that if you have 

knowledge of whether or not A happens, 

that does not have any impact on 

the probability of B and vice versa. 

A very standard use case of this fact 

in algorithms is that we can improve 

the success probability of a Monte Carlo 

randomized algorithm by just running 

it for multiple independent trials. 

Let's look at a concrete example of this. 

Suppose I have a method for processing some file, 

and that method, it's a Monte Carlo randomized algorithm. 

I could potentially fail, and it could 

potentially fail with probability up to at most 1/2.

Play video starting at :5:55 and follow transcript5:55

That's really not a great 

failure probability in practice, 

but I can improve it substantially by just 

running multiple independent trials of the same method. 

Imagine that I run this algorithm 

for log_2N independent trials. 

Now, I only fail if 

every single one of those attempts fails. 

Otherwise, I've managed to 

process the file somewhere along the way. 

Now my overall failure probability 

is upper bounded by 1/2 times 1/2, 

times 1/2 log_2 N times, 

and 1/2 to the power of log_2N is otherwise known as 1/N. 

This is a much more 

palatable bound on failure probability. 

I should probably mention what N means here.

Play video starting at :6:37 and follow transcript6:37

Normally, N is the input size of a problem. 

I don't necessarily have an N or an input size here. 

N is just a parameter that I'm 

using to illustrate the trade off between 

the number of times I have to run 

the algorithm and 

the resulting failure probability that I get. 

To get a failure probability of the form 1/N, 

I only have to run this algorithm 

a logarithmic number of times in N, which is quite nice. 

This actually also takes us in the direction of being 

able to define what we mean by with high probability. 

Before that, let me just add one more small detail. 

Suppose instead of log_2N, 

I run the algorithm for 17 log_2N independent trials, 

that's still on the order of log N. If 

you just trace the 17 through our math, 

it ends up in the exponent 

of the N at the end of the day.

Play video starting at :7:28 and follow transcript7:28

Our failure probability is now 1/N^17. 

If you want to failure probability of the form 1/N^99, 

you would just have to run 99 log_2N independent trials. 

Finally, we can define 

what we mean by with high probability. 

This has become a convention, 

where when I say something 

is successful with high probability, 

it means that the failure probability 

is upper bounded by something inverse polynomial, 

like what we have here, 1/N to a constant. 

With high probability means that 

your failure probability is of that form, 

where interestingly, that constant can 

typically be set to anything you want it to be set to. 

Here, if I wanted 

a failure probability of the form 1/N^99, 

I can do that by just running 

99 log_2n independent trials, 

and then 99 actually disappears as 

the hidden constant in my big O running time. 

That's a hallmark of this notion of with high probability is 

the ability to set the constant 

here arbitrarily to whatever you want it to be.

Play video starting at :8:35 and follow transcript8:35

However strong you want the bound to be, 

you can achieve that by choosing a suitable constant 

tucked away inside the big O 

of your describing your running time. 

What if I now have N files 

to process instead of just one? 

What I'm going to do is just 

run the preceding algorithm that runs, 

17 log_2N independent trials per file. 

I'm going to run that on each of my N files. 

Here the N means 

the same thing in both cases. I have N files. 

That's the same n as in the 17 log_2 

of independent trials I'm running on each file.

Play video starting at :9:12 and follow transcript9:12

My overall running time increases to N log N. 

What happens to my failure probability? 

Now I'm interested in the failure probability 

in general across all n files. 

That's actually, like we talked about before, 

that's a union of events, 

the union of the probability that I fail on File 1, 

or that I fail on File 2, 

or that I fail on File 3, and so on. 

I can use the union bound to 

upper bound the probability of failing on 

any file by just N times the probability 

of failure on one file, 

which using the bound above was 1/N^17. 

That gives us an aggregate failure probability 

of the form 1/N^16. 

The cool thing here is that this 

is still a high probability 

bound because it is of the form 1/N to a constant, 

or I can make that constant whatever I want it to be 

by just choosing a suitable constant 

from the original algorithm.

Play video starting at :10:6 and follow transcript10:06

If I wanted this constant to be 1/N^16, 

I just have to think backwards and run 

17 log_2N iterations on each of 

my individual files to get 

a per file failure probability bound of 1/N^17, 

that when I apply a union bound to that gives me 1/N^16. 

I still get a high probability bound of success 

for the aggregate algorithm 

when run on N individual files. 

That's a really nice feature of 

our definition of with high probability, 

is it survives a union bound over N things and 

comes out the other side still 

as a high probability bound. 

That gives us a little bit of insight into maybe why 

this is a good choice for what we should 

mean with high probability. 

There are a couple of different 

possible bounds we could have 

considered for a high probability bound. 

We could have just chosen a 

small constant or something like 

o1/log n or something like inverse exponential. 

There are many different possible choices.

Play video starting at :11:9 and follow transcript11:09

In fact, a constant really isn't great here. 

We really do want a bound that 

gets stronger and stronger as our input size increases. 

Scalability was important 

when we talked about running time. 

It's also important when we 

talk about failure probability 

because if you run 

an algorithm on a very small input size two or three, 

there may just not be that many 

possible outcomes that can happen. 

If just one of those is bad, 

then your overall probability of failure might actually 

inevitably be quite high on small inputs. 

The best we can usually hope 

for is a bound on failure that 

gets stronger and stronger as input size increases. 

What's the right dependence 

between failure probability and input size?

Play video starting at :11:54 and follow transcript11:54

Well, I think a nice level of dependence is when 

you have a failure probability of 

the form 1/N to a constant, 

this inverse polynomial bound, 

specifically because that is strong 

enough to survive a union bound. 

That lets us do some really 

nice things with our analysis. 

For example, let's go back 

and look at the randomized reduction lemma, 

our old friend that we've used in 

many different situations for 

analyzing expected running time. 

Imagine that you have an algorithm 

that starts with an input of size n, 

and in every iteration has 

at least a constant probability of 

reducing your effective problem size 

to some constant fraction of what it used to be. 

The randomized reduction lemma shows that 

this algorithm takes only a logarithmic number 

of expected iterations. 

We've used this for a wide range of purposes, 

maybe notably to show that a generic input element in 

randomized quicksort undergoes a 

logarithmic expected amount of work. 

It turns out that 

the randomized reduction lemma not 

only gives you a bound that holds in expectation, 

it also gives you a bound that 

holds with high probability.

Play video starting at :13:2 and follow transcript13:02

Same conditions. If if your algorithm 

satisfies the conditions of 

the randomized reduction limit, 

you get either type of bound, 

whichever one you're trying to apply in your analysis. 

You could, for example, 

show that randomized quicksort spends log in 

time with high probability on a generic input element. 

You could show that randomized 

binary search runs in order log in time with 

high probability with 

the exact same randomized reduction lemma 

and that actually opens up, 

as I was mentioning, another avenue 

for analyzing algorithms quite easily. 

If we look at randomized quicksort, 

for example, now we have two flavors of analysis. 

We can analyze the expected running time, 

which we did as follows. 

We used the randomized reduction lemma 

to argue that per element, 

we're spending log n expected time, 

and then we used linearity of 

expectation to add that up across all n of 

our elements to get 

a total expected running time bound of 

n log n. If you would 

rather do a high probability analysis, 

then what we would do instead is maybe use 

the same randomized reduction lemma 

to argue that per element again, 

we spend order log in time with high probability.

Play video starting at :14:16 and follow transcript14:16

But now we need a different tool to 

aggregate that across all n elements. 

That tool here is the union bound. 

We can take a union bound over all n elements and 

argue that you take log n time on element one, 

union with the event that you take log n 

time with high probability on Element 2 and so on. 

We can take a union bound over 

all the elements and conclude that 

the overall running time is n log n, 

also with high probability because 

our definition of with high probability is 

designed so that it survives a union bound over n 

things and comes out the other side 

still as a high probability bound. 

Two very distinct flavors of analysis that we 

can apply to many different randomized algorithms. 

This is an example, our high probability analysis is 

an example of what you could call 

a tail bound in probability theory. 

A lot of times when you have a probability distribution, 

you're interested in how quickly it dies off, 

how much mass is in the tail of the distribution.

Play video starting at :15:20 and follow transcript15:20

If I flip 100 fair coins, 

I might be interested in what's the probability 

that I have 75 or more heads, 

of how much mass is in that tail. 

It turns out very little in this particular example. 

I could also ask for a randomized algorithm, 

show that the probability that the running time is on 

the order of log n is extremely high, 

that failure probability is extremely 

low of the form 1/N to a constant. 

That's also asking about a tail bound, 

because if you look at the probability distribution 

of the running time of that algorithm, 

you're trying to show that there's 

a minuscule amount of probability in 

the tail of that distribution out 

past the order log n mark, 

the amount of mass being 1/N to a constant. 

We have a couple of tools in probability theory that are 

very useful for analyzing 

tail bounds on random variables. 

One of the simplest is called Markov's inequality. 

This is a very straightforward, 

very general tool that 

we definitely want to have in our toolbox.

Play video starting at :16:24 and follow transcript16:24

It just says that if you have a non 

negative random variable x, 

the probability that if you sample from 

x's distribution that you get 

something more than k times what you expect, 

that probability is at most 1/k. 

If you have a running time in 

expectation of t for some randomized algorithm, 

the probability that the algorithm runs 

for say more than 5T time is at most 1/5. 

The probability that you run for 

more than 50T time is at most 1/50. 

It's a very natural type of bound. 

If we apply this to our example of coin flips. 

We flip 100 coins, 

and we're interested in the probability 

that you have more than 75 

heads. So 75 that's three halves 

times the expected number of heads, which is 50.

Play video starting at :17:11 and follow transcript17:11

Using Markov's inequality, 

you could say that the probability that you have 

more than 75 heads is at most 1/3 halves or 2/3. 

That's actually a very loose 

upper bound for this particular instance. 

In many cases, Markov's inequality 

does give you a very loose upper bound, 

but it's generic enough, 

this tool that it's still very broadly applicable. 

Doesn't require too many conditions. 

All it requires is a non negative random variable. 

It applies in a wide range of situations. 

Let's go through a couple of 

prototypical examples where we 

could apply Markov's inequality.

Play video starting at :17:49 and follow transcript17:49

Imagine for a minute that we have a quadratic time 

algorithm that takes linear expected space. 

Imagine it's a 4n expected memory usage. 

Imagine that we're in an environment 

where memory is very precious and we 

really can't tolerate more 

than a linear amount of memory usage. 

We really would rather have a worst case 

bound on memory usage, 

even if that has some impact on our running time bound. 

We can actually achieve this by running 

our algorithm and tracking its memory usage. 

If the memory usage goes above 8 n, 

so more than twice what you expect, 

then you just terminate the algorithm 

and start rerunning it from scratch. 

We're going to basically run 

independent trials of our algorithm until 

we successfully have a trial that uses at most 8n memory.

Play video starting at :18:36 and follow transcript18:36

Because of Markov's inequality, 

the probability that any given trial uses 

more than twice the expected amount 

of memory, that's at most 1/2. 

Every trial fails with probability at most 1/2. 

It therefore succeeds with probability 

at least 1/2 and so now using geometric random variables, 

the expected number of trials 

until we have a success is at most two. 

Our running time is still 

quadratic just in expectation because we're 

running an expected number of 

trials of two of the original algorithm. 

We could also have done a high probability analysis 

here using pretty 

much the exact same mathematics 

from earlier in this discussion. 

If you run a logarithmic number 

of independent trials of the algorithm, 

then you can argue that with high probability, 

one of those trials should have succeeded because 

the probability of failure is again at 

most 1/2 on each trial. 

If you run logarithm many such trials, 

that drives down the failure probability to 

something at most 1/N to a constant of your choosing.

Play video starting at :19:37 and follow transcript19:37

For another nice application of Markov's inequality, 

we can use it to develop 

another flavor of the randomized reduction lemma. 

Remember the original conditions of 

the randomized reduction lemma 

require that every iteration of 

our algorithm has to have at least a constant probability 

of reducing our problem size by some constant fraction. 

What if instead, each iteration of our algorithm 

only demonstrates reduction in expectation. 

For example, the expected problem size after 

the iteration is at most 0.6 times the original size. 

We expect to shrink by 0.6 factor in each iteration. 

We can use Markov's inequality 

in this situation to show that 

this algorithm would have also 

satisfied the original conditions 

of the randomized reduction lemma. 

The result is that you again, 

would experience a logarithmic 

number of total iterations, 

both in expectation and with 

high probability. How do we show this?

Play video starting at :20:35 and follow transcript20:35

Well, I'm going to just pick a number 

between 0.6 and 1, like say 0.8, 

and look at the probability that 

our new problem size is more than 0.8 times the original. 

We expect it to be less than 0.6 times the original. 

I can phrase this as what's the probability that 

the new problem size is more than 4/3 

times what you expect it to be. 

Due to Markov's inequality that probability is 

at most 1 / 4/3 or 3/4. 

The probability that your new problem size 

is bigger than 0.8 times the original. 

That's at most 3/4. 

I can compliment this and say, 

what's the probability that 

the new problem size is less than or equal to 0.8.

Play video starting at :21:17 and follow transcript21:17

That's going to be at least 1/4. 

That is a statement of 

the original conditions of 

the randomized reduction lemma. 

I have these two constants, 

the probability of a reduction and 

the amount of the reduction and so this is nice. 

We can now apply the randomized reduction lemma 

in even more settings. 

Sometimes, Markov's inequality is great, 

but sometimes you need to use 

a sledge hammer to solve a problem. 

In this case, the sledge hammer is a set of 

bounds collectively referred to as turnoff bounds. 

They are extremely strong bounds, 

often used to prove high probability results.

Play video starting at :21:53 and follow transcript21:53

But because they're so strong, 

they only apply in a more narrow set of circumstances, 

particularly when you have a random variable x that is 

given by a sum of independent indicator random variables. 

Our coin flip example would work here if we flip 

n coins and we're interested in how many heads we flip, 

then you could have an indicator random variable 

for every single independent coin flip. 

Random variables like this that decompose into a sum of 

indicators they are called 

binomially distributed random variables, 

and it's known that a binomial distribution 

is very tightly concentrated around its mean. 

It drops off really quickly, 

exponentially quickly as you go away from 

the mean and so there are 

different flavors of turnoff bounds 

that depend on whether you would like to prove a 

bound on like the additive deviation from 

the expectation or a 

multiplicative deviation from the expectation? 

But they all generally have 

this exponential decay baked into them. 

If you'd like to get a bound on the probability of 

seeing more than 75 heads in 100 coin flips, 

you can phrase that as what's the probability 

that you have 25 more heads than you expect? 

I guess that means we're using the 

first of these different turnoff bounds.

Play video starting at :23:8 and follow transcript23:08

That if you plug in 25, 

tells you that the probability 

of seeing more than 75 heads is 

actually quite small, 0.000004. 

Turnoff bounds are incredibly powerful that they 

do only apply to a limited number of circumstances. 

Now, one of the nice applications 

of turnoff bounds is you can 

actually use them to 

prove the randomized reduction lemma. 

Specifically the one that gives you 

a high probability result and unfortunately, 

the number of steps here is a little bit high. 

The proof actually takes two slides. 

I won't go through it in detail. Don't worry.

Play video starting at :23:45 and follow transcript23:45

I'll just leave it on the slides for those who are 

interested to be able to work through the details. 

Nothing here is particularly complicated. 

It just takes a little bit of 

work to set things up in a way 

that we can then apply a turnoff bound successfully. 

This is one motivation for why we created 

the randomized reduction limit in the first place so that 

we don't have to go through this level of 

detail whenever we want 

to prove a high probability result. 

We can often use a much simpler 

randomized reduction based argument instead. 

But in some situations, 

it's nice to know about turnoff bounds because sometimes 

applying them directly is 

the right thing to do for a particular application. 

We've now seen a number of tools that we can use to 

analyze tail bounds and high probability results, 

so our toolbox now has a wide range of tools 

we can successfully use to analyze randomized algorithm.