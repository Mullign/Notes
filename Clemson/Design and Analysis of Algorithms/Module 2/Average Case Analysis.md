![[_chlepCtRX2C8mMZs4y8QA_88175ed5ff4f484387984b4eb61ec1f1_Average-Case-Analysis.pdf]][MUSIC] 

In this video, we will get quite a bit of 

additional practice using 

the analysis tools that we've already 

developed for analyzing randomized algorithms 

and we'll see how those very same tools 

can often also very easily analyze 

the average case performance of non-random algorithms. 

Sometimes those two concepts 

end up meaning something very similar. 

If we go back to quicksort, for example, 

we've already established that 

randomized quicksort runs in N log N 

time and expectation, 

and that if you use 

a more crude heuristic for choosing your pivots, 

then the running time can be quite a bit worse. 

One particularly ill-advised rule for choosing pivots is 

to always just choose whatever element is 

at the beginning of your array as a pivot. 

That's usually a bad idea because if you're 

sorting an array that's already sorted, 

which actually does happen a lot in practice, 

then your choice of pivot will always be 

like the minimum element in the array, 

which is a really bad choice for pivot. 

It doesn't make much progress when 

you do a partition on that pivot, 

and it does give you a quadratic running time. 

However, if you use that naive choice for 

pivot after first scrambling 

your array as a pre-processing step, 

then that converts basically the average case performance 

of this algorithm back to 

essentially what is randomized quicksort.

Play video starting at :1:25 and follow transcript1:25

Because you can argue that every single time 

you're choosing a pivot using the simple heuristic, 

you're now basically choosing 

a random element as the pivot. 

Here the average case analysis of 

our algorithm number 2 

basically boils down to randomized quicksort. 

The two are analyzed pretty much the same way. 

As a quick warm up, let's take 

a look at a simple mathematical process 

that will be used in quite a few 

of our analyses moving forward. 

Here I take an array, 

randomly permute the array, 

and I scan through it keeping a running maximum. 

I'm interested in how many times I 

reset that running maximum, 

and it turns out not too many. 

In expectation, you only expect to reset 

that running max a logarithmic number of times.

Play video starting at :2:8 and follow transcript2:08

In this example, I've drawn 

a little green check mark over 

every element that is the 

biggest element I've seen so far. 

That would be a reset for my running max. 

We've actually seen this process before. 

I think when we talked about linearity of expectation we 

showed an example of building 

a histogram in an online fashion, 

adding elements one by one in random order. 

There, every time you add 

an element that was the biggest one so far, 

that was bad news because it caused you to 

do an expensive update to the entire histogram. 

For an application like that, 

it could indeed be useful to know that you don't 

expect to have to rebuild the histogram that often, 

you don't expect too many resets of your running max. 

Let's show that this is indeed the case.

Play video starting at :2:50 and follow transcript2:50

There are a couple of ways we could do this. 

Maybe for practice, we'll 

use first linearity of expectation 

and then we'll use the randomized reduction lemma 

for an alternative argument. 

If we use straightforward linearity of expectation, 

we're trying to find the expected value of M, 

the number of times we reset our running max, 

and we can decompose that into a sum 

of simpler indicator random variables, 

each one telling us if 

a particular element resets the running max. 

By linearity of expectation, 

the expected value of M is just the sum of 

the expected values of those indicator random variables. 

Now all I need to do is figure out what is 

the expected value of one of these M_j random variables. 

Remember that the expected value 

of an indicator random variable is 

nothing more than the probability of 

the event associated with that indicator random variable. 

Here the event at the jth element 

is indeed the largest among the first j element, 

that has a green check mark on 

it in our previous picture.

Play video starting at :3:51 and follow transcript3:51

That's an easy probability to get 

a handle on because each of 

the first j elements is equally likely to be 

the maximum because it's 

a random permutation we're dealing with. 

This is just going to be 1/j 

because the jth element is just 

as likely as any of the other elements 

in the first j to be the maximum. 

Now I just add things up 

and I get an interesting looking series. 

I get 1+1/2+1/3, 

all the way up to 1/N. 

This series is actually a pretty common series. 

It has a name. It's called a harmonic series.

Play video starting at :4:27 and follow transcript4:27

Shows up in quite a few places 

and it's known that if you add this up, 

you get something extremely close to 

the natural log of N within 

plus or minus a very small constant offset 

of natural log of N. Indeed, 

the answer that we get is on the order of log N, 

as we were hoping to see. 

That's a proof using linearity of expectation. 

What about using the randomized reduction lemma? 

Is there indeed some sort of parameter 

baked into this problem that we can show 

is reducing itself according to 

the structure required by the randomized reduction lemma? 

It turns out that there actually is. 

Maybe just for simplicity, 

I'll drop in like a dummy 

infinity at the end of the array.

Play video starting at :5:10 and follow transcript5:10

That will serve as the final maximum 

and the starting point 

in this process that I'm going to define, 

I'm going to basically walk backwards along 

the entire chain of elements that 

were the elements that reset my running maximum. 

I'm going to visit them all in reverse order, 

and I want to show that during that process I 

take only a logarithmic number of steps in expectation. 

That's actually really easy to do because 

if I'm sitting on a particular element, 

say element j, then where was the preceding maximum? 

If I take a step backwards from j 

to the element before me, 

where was that preceding maximum? 

It's equally likely to be anywhere before 

j because I'm dealing with again a random permutation. 

Maybe if I divide all the elements 

preceding j into two equal size sets, 

maybe call them A and B, 

then when I take a step backwards from j, 

I'm lucky if I take a step backwards into A, 

and there's a 1/2 chance that I do that because 

the preceding maximum was equally 

likely to be in A as it was in B. 

If I take a step backwards into A, 

then that's good news because that means that my index 

j is going to reduce to something that is at most j/2.

Play video starting at :6:27 and follow transcript6:27

Every single step, I have a 1/2 probability of 

reducing my index in 

the array to half of what it used to be. 

That satisfies the conditions of 

the randomized reduction lemma. 

In expectation, I take a logarithmic number of steps. 

Easy to show using a variety of different methods. 

For our first primary application, 

I wanted to take a look at multi-objective optimization. 

Here I have a candidate set of solutions. 

I'd like to find the best one, 

but that can be tricky sometimes because 

the solutions are measured 

according to different objectives.

Play video starting at :6:58 and follow transcript6:58

Here, for example, I have a bunch of 

football teams that are all 

measured according to offensive strength 

and defensive strength. 

How do I choose the best one? 

Well, it's easy to rule out certain teams. 

For example, the sloth 

carrying a football and our in state rival, 

the University of South Carolina, 

they are both strictly dominated by 

both Clemson and Ohio state in both objectives. 

We could rule them out. They're not as interesting 

if you're trying to find an optimal solution. 

But Clemson and Ohio state, 

they're actually kind of incomparable 

because one's better in one objective, 

one's better in the other objective, 

and this is fairly common.

Play video starting at :7:35 and follow transcript7:35

What you typically look for in 

a multi-objective optimization setting 

is not one interesting solution, 

but an efficient frontier of interesting solutions. 

These are called the non-dominated 

or pareto-optimal solutions sometimes. 

Again, these blue solutions are not interesting because 

the blue solutions are dominated 

by some other solution in both objectives. 

But the yellow solutions, 

they're actually possibly interesting 

because they give you 

interesting choices of the trade offs 

in the two objectives here; 

so cost effectiveness and time effectiveness. 

A lot of times when 

you have multi-objective optimization, 

the multiple objectives 

actually fight against each other. 

If you want to be good on one objective, 

you have to sacrifice on the other objective. 

This also shows up quite often in the world of 

machine learning with these receiver operating curves 

that you use to describe 

the performance of a predictive algorithm and so 

this basically shows you for 

different algorithmic choices and 

different parameter settings in those algorithms, 

how you're trading off between your 

true positive and your false positive rate.

Play video starting at :8:39 and follow transcript8:39

If you want to achieve a very low false positive rate, 

then you can do that by 

basically saying that everything is a negative. 

You're not going to predict positively for anything, 

you're going to get no false positives, 

but then you're not going to get 

any true positives either. 

If you tune your algorithm by changing its parameters, 

you can get a very high true positive rate as well. 

You can predict positive for everything. 

Unfortunately, that's also going to give you 

a very high false positive rate 

and so you typically end up with 

this trade off curve of predictive performance that you 

can pick any point along 

that curve by tuning your algorithm appropriately. 

In this example right here, I guess, 

the blue algorithm, this particular setting of 

parameters for the blue algorithm, would 

dominate this setting of 

parameters for the red algorithm. 

In this case, it's good to 

be higher and to the left because you want 

a low false positive rate versus 

higher and the right for this other example.

Play video starting at :9:36 and follow transcript9:36

A couple of examples from multi-objective optimization. 

Suppose in whatever problem we're looking at, 

that we would like to examine very 

closely all of these non-dominated yellow solutions. 

We're going to spend a lot of time 

looking at those in detail so we 

might be interested in how many 

such solutions we expect to see. 

In terms of average case analysis, 

suppose that we have n points that are just 

randomly chosen from maybe the unit square, 

and we would like to know in expectation, 

how many non-dominated yellow points are we going to see? 

Maybe actually there's 

an interesting algorithmic question here that 

we can talk about first before we 

look at the average case analysis. 

How would we actually even 

find those non-dominated points? 

If I give you n points in the two dimensional plane, 

what would be a simple and efficient algorithm that 

identifies all of the non-dominated points?

Play video starting at :10:31 and follow transcript10:31

There are actually a couple of easy ways to do this, 

at least easy in low dimensional spaces. 

This is another one of these 

computational geometry problems that 

suffers from the so called curse of dimensionality. 

In high dimensional spaces, 

this is a much harder problem. 

All you can really do there 

is just compare points pairwise. 

In fact, that's really, I guess, 

the brute force approach that you might think of first 

for solving this problem is in quadratic time, 

just compare every point to 

every other point and see if it's dominated. 

That would be an easy approach, 

but it would be n^2 in its running time. 

Hopefully, we can beat n^2.

Play video starting at :11:9 and follow transcript11:09

There are some ways that we can do this. 

One very simple approach, 

you could maybe call it a sweep line approach 

or a sort and scan approach. 

It even has flavors of incremental construction. 

All we're going to do is sort all of our points on 

x and scan across the points in that order. 

Visit them in increasing order of x. 

As we do that, we're going to 

identify the non-dominated points. 

Here's a snapshot in the middle of our algorithm.

Play video starting at :11:35 and follow transcript11:35

We've scanned over the set of points 

indicated here and we have 

a tentative set of non-dominated points. 

We've ruled out these red points. 

They've already been shown to be 

dominated by points we've scanned across. 

They've been deleted from consideration 

and we only have the yellow points still in play. 

As we scan through our points, 

we're going to store them in this case in 

a priority queue data structure as we can have 

talked about in our coding example from this module. 

We're going to store them in a priority queue 

because whenever you hit a new point, 

that new point now has the possibility of 

disqualifying points we've already scanned across. 

Imagine if you hit this blue point right here, 

that is now going to dominate and disqualify 

these three yellow points 

that have a smaller y coordinate.

Play video starting at :12:22 and follow transcript12:22

If we store all of our existing candidate points 

in a priority queue ordered by y, 

then every time you hit a new point, 

you're just going to keep calling 

remove min from that priority queue to keep peeling 

off the points that you're 

storing until you reach 

the y coordinate of the point you've just hit. 

Because every time you hit a new point, 

it disqualifies all of the points you've already seen, 

the lesser in x, that are below you 

in y because this new point 

dominates all of those points. 

That's all we do. We scan across the points, 

every point gets inserted into a priority queue, 

and at some point it might 

get removed from the priority queue. 

We do a total of n inserts at 

most n removements from the priority queue. 

Each of those operations in 

most priority queues takes only logarithmic time. 

That's going to be N log N for the scan, 

and I guess we sorted at the beginning, 

so that was another N log N.

Play video starting at :13:15 and follow transcript13:15

Our total running time here is just just 

N log N. Actually an even easier way, 

we could have found the non-dominated points 

would be scanning backwards. 

Again, we sort on x, 

but now we scan backwards on x, 

and all we do at this point 

is keep a running maximum in y. 

Every single time we hit a point that is 

a new maximum in y, that point is yellow. 

It is a non-dominated point. 

Now this connects the dots with 

our warm up exercise because the number 

of times we reset that running maximum 

is the number of non-dominated points. 

If our points are chosen effectively at random, 

then as we scan backwards in x, 

the y coordinates that we see, 

that's effectively going to be 

a randomly ordered sequence of numbers.

Play video starting at :14:2 and follow transcript14:02

The preceding analysis that 

we did or the reset max problem applies 

here and you only expect to see 

a logarithmic number of non-dominated points. 

Not too bad. For our next fun example, 

I thought we would revisit a problem that we saw 

in a few places in Module 1. 

That is the domination radius problem. 

Here you're given an array of 

heights of individuals all standing in a row. 

For every individual, you'd like to compute 

their left and right domination radii. 

We actually showed how to do this in only linear time in 

the coding demo of Module 1 using some clever insight.

Play video starting at :14:39 and follow transcript14:39

But here we're going to consider 

a much more simplistic algorithm that basically just from 

each individual scans left until you reach someone 

taller and scans to 

the right until you reach somebody taller. 

That, of course, runs in quadratic time in 

the worst case because if 

the individuals are standing in sorted order, 

then everyone's going to be scanning 

a very long distance in one of those two directions. 

Quadratic time in the worst case, 

what happens in the average case though? 

What happens if you run this naive algorithm, 

this overly simplistic algorithm on 

a random permutation of N heights? 

Something actually rather 

remarkable happens in that case. 

It turns out that there's almost a direct correspondence 

between that average case analysis 

and what happens with randomized quicksort. 

Let me try and explain this.

Play video starting at :15:28 and follow transcript15:28

Randomized quicksort, I've drawn 

the same picture here on the right that we 

saw earlier when we analyzed 

the expected time of randomized quicksort. 

On the left, I've drawn 

a sorted ordering of the elements 

that I'm sorting here on the bottom. 

Then on top of that is 

my randomly permuted instance 

of the domination radius problem. 

Let's talk about the mechanics 

here and see that it really 

is the same set of 

comparisons happening in both situations. 

For domination radius, we're ultimately going to end 

up doing N log N expected comparisons. 

In the domination radius problem, 

I would like to make the height of 

an individual correspond to in randomized quicksort, 

how early that element was chosen as a pivot. 

The tallest element in the domination radius problem, 

which could be anywhere in the array 

because that's a randomly permuted array, 

that would correspond to the very first element 

chosen as a pivot for randomized quicksort.

Play video starting at :16:26 and follow transcript16:26

In terms of mechanics, 

look at the tallest element 

in the domination radius problem. 

That's over top of a random element, 

and that element looks left and right. 

It compares against everybody in 

the entire array and then it 

effectively partitions the array 

because no one else can see past that taller element. 

It effectively acts as a blockade 

from that point onwards. 

The elements less than 12, in this case, 

are now separated from the elements bigger than 12, 

and they will never be able to see each other 

across the tall individual sitting on top of 12. 

The same thing happens in randomized quicksort. 

We pick a random element as our pivot, 

the same 12 element, 

and that gets compared to 

every single person in the array, 

and then it partitions the array in that process 

into things less than 12 and things bigger than 12.

Play video starting at :17:13 and follow transcript17:13

We've made the same comparisons and we've 

partitioned into the same sub-problems in both cases. 

Now the same process repeats on both sides. 

For example, on the left hand side, 

again, you pick the tallest individual, 

that individual will compare against 

every single person in the 

sub-problem by scanning left and right, 

and then effectively partition 

that sub-problem into two pieces. 

Again, the same thing happens in randomized quicksort. 

You pick a random element as your pivot, 

the same one that had 

the tallest spike on 

top of them in the domination radius picture, 

and then that element gets compared to everybody 

and then partitions its respective sub-problem. 

The two processes are pretty much analogous, 

and you actually make the exact same comparisons 

on both sides. 

You can conclude by this correspondence that 

the domination radius problem involves 

only N log N expected comparisons.

Play video starting at :18:5 and follow transcript18:05

This is nice, this is a good way to analyze 

things by maybe not reinventing the wheel or 

doing another low level analysis 

with random variables or randomized reduction or whatnot. 

If you can show that one problem 

is closely related to another problem, 

you can exploit that fact. 

Let's actually exploit that fact in 

another interesting way or the same problem. 

Again, I'm looking at 

the domination radius problem and now I want to 

use my insight that we developed for 

the reset max problem to analyze things here. 

What I'm going to do is consider, 

again, this is the average case analysis. 

Just look at a generic location at say position i in 

my array and I would like to 

look at scanning to the left from i, 

keeping a running max, 

how many times does that running max get reset? 

Since this is a randomly ordered array of heights, 

I would expect a logarithmic number 

of resets of my maximum.

Play video starting at :19:4 and follow transcript19:04

That's these yellow elements here that 

get progressively taller as I scan to the left. 

If I think about things, 

it is only those yellow elements 

that when they scan to the right, 

will actually compare against the element in position i. 

Everyone else is hidden from 

view from the element at position i. 

From position i, 

there's only a logarithmic expected number of elements on 

the left and only a logarithmic number 

of expected elements on 

the right that will scan 

outwards and compare with element i. 

I almost flipped things around 

instead of looking at who i compares to 

and of who compares to i in their respective scans. 

That's a logarithmic expected amount of work or 

comparisons involving each location 

in the array or N log N in total. 

Yet another interesting way that you can slice and dice 

things by using previous analyses for previous problems.

Play video starting at :20:1 and follow transcript20:01

There are actually many ways 

we could have analyzed this problem. 

Actually, before we look at another one, look at that. 

If we put points down here on 

top of all of the individuals, 

the yellow ones correspond to non-dominated points, 

so more connections between our concepts. 

We could have actually done another analysis 

using linearity of expectation, 

so just in the interest of 

getting as much practice as possible. 

Let's look at another way we could have analyzed 

the average case performance here 

of the domination radius problem. 

In this case, we're 

also trying to compute something fairly natural. 

I'm looking at this randomly permuted array of heights 

and I'm looking at one generic location in that array.

Play video starting at :20:47 and follow transcript20:47

From that location, let's say I scan to the right, 

I would like to basically compute 

the expected number of 

people I compare against when scanning to the right, 

and I'm going to show that that's logarithmic. 

That means for every location in the array, 

I expect to compare against 

a logarithmic number of people on both sides, 

and so that again is going to give me 

N log N total expected comparisons. 

Why is that? Well, I can break this up 

into a sum of indicator random variables. 

The distance I scan to the right, 

that's a complicated random variable. 

But I can decompose that into a sum 

of indicators, X_1 + X_2 + X_3, 

where basically X_1 tells 

me if I scan a distance of at least 1, 

and X_2 tells me if I scan a distance of at least 2, 

X_3 tells me if I compare to 

at least 3 people on my right and so on. 

In this exact picture here, 

X_1, X_2, X_3, and X_4 

would take the values 1 because I 

compare against those next four elements from 

this particular generic spot at index i.

Play video starting at :21:52 and follow transcript21:52

I don't compare to anyone beyond that because 

I'm blocked by somebody taller than me at that point. 

All I need to do is compute 

the expected values of these indicators, 

and it turns out that that 

actually gives me a harmonic series. 

That's where I get the order log N from. 

Why the harmonic series? 

Well, let's just look at one example here. 

Let's see what's the expected value of X_3. 

That's the probability of the associated event with X_3.

Play video starting at :22:20 and follow transcript22:20

The event that I scan to the right, 

a distance of at least three. 

If I scan to the right a distance of at least three, 

that means I scan over the top of two people. 

That means when I scan to the right, 

I scan over the top of two people. 

That means that I was taller than those two people. 

What that means is between me and those two people, 

I had to be the tallest entity. 

Here I have a set of three people, 

myself and those two people 

I'm looking at scanning over the top of, 

and I'm looking at the event that 

I am the tallest of these three people and that 

happens with probability one out of 

three because in any set of three people, 

it's equally likely that I'm the tallest of those three. 

Relatively simple analysis here 

using linearity of expectation.

Play video starting at :23:8 and follow transcript23:08

Now, interestingly, 

remember that there's a fairly direct correspondence 

between the average case analysis of 

my domination radius problem and 

randomized quicksort in terms of its expected analysis. 

I could have actually taken 

the preceding two analyses 

here for the domination radius problem, 

and I could have actually ported them back to 

get alternative analyses for randomized quicksort, 

and I won't go into the details in too much depth here, 

I'll just highlight what it would look like. 

With randomized quicksort, 

if you look at the elements 

of the array that you're sorting, 

look at them in sorted order, 

and look at a generic element, 

I can basically say, well, 

how many pivots would have compared against me? 

You'll end up with pretty much a very similar picture 

to what we had with our reset max example, 

you'll get a logarithmic expected number of pivots on 

both sides that would have compared 

against any generic element in my array. 

That gives you your N log N and 

expectation number of comparisons. 

You could have also done the linearity of 

expectation type of analysis 

that we had just done as well. 

For any element in your array, 

you can argue that it gets compared in 

expectation to a logarithmic number 

of elements above it and below it in value.

Play video starting at :24:29 and follow transcript24:29

If you looked at all the elements in sorted order, 

and the analysis here is pretty much exactly 

analogous to what we 

had done in the domination radius problem. 

One final note. We will actually revisit 

these pictures and this correspondence 

in about two modules when we talk about data structures. 

We will actually go back to 

randomized quicksort, and again, 

show an interesting correspondence with 

randomly built binary search trees 

and show that we'll be able to 

balance a binary search tree 

using a very clever application of 

randomization that is almost 

directly mapped to what randomized quicksort is doing. 

We'll come back to these topics again in 

the future and see some other interesting relationships. 

[MUSIC]![[screenshots/Screenshot 2025-09-05 at 9.16.44 pm.png]]