![[I1t3f47aRZeOHtuIVKxh-Q_81a219100a8542ce892d1328599205f1_NEW-Assignment-1-Overview.pdf]]
[MUSIC] 

This video describes the details behind our first coding assignment of the class. 

And, of course, it would be remiss of me if I didn't also sprinkle in a few fun 

algorithmic tidbits along the way as well. 

We will have a couple of programming assignments throughout this course with 

a couple of goals in mind. 

First of all, this will help us reinforce the lecture content. 

I think there's a lot of benefit to seeing algorithms described not only at 

a high level in abstract mathematical terms, as we sometimes do in lecture, but 

also at a low level in actual code. 

That's one of the reasons we have implementation exercises alongside every 

module in this course. 

We also have tried very hard to pick example problems for 

the coding assignments that really do showcase the applicability of algorithms 

in modern computing applications.

Play video starting at ::55 and follow transcript0:55

So we've tried to pick very relevant applications in 

today's data-driven world that really call out some of the cool and 

exciting things that algorithms can really accomplish. 

And then finally, 

this is a great opportunity to just simply improve your implementation skills. 

Algorithmic coding is perhaps some of the most challenging coding you can do because 

you're trying to translate some very abstract and 

complicated ideas from your head into code. 

This can be a wonderful sandbox for practicing and 

improving your implementation skills. 

We do have an automatic grading environment set up so 

you can submit your code and get pretty much instantaneous feedback on how many 

test cases you get right and how much partial credit you're getting. 

That will hopefully help you develop your programs and 

improve their performance so that you get very close to a full score. 

Although, we've also designed our problems so 

that maybe getting a 100% is actually kind of challenging.

Play video starting at :1:52 and follow transcript1:52

Real world problems, they're not toy problems. 

They have a little bit of messiness involved. 

And so some of our problems are somewhat open ended, and so 

there will be maybe a little bit of challenge involved with getting like 

a fully 100% score on the homework. 

But, if you do the things you're supposed to do, it shouldn't be too hard to get 

a reasonably high score. Definitely high enough to get a decent grade in the class. 

We have tried to allocate a reasonable amount of time for everyone 

to work on the assignments; two, and hopefully even three weeks per assignment. 

That might make some of our assignments overlap slightly, but we wanted to err on 

the side of giving everyone plenty of time and giving generous deadlines so 

that you'd have a proper amount of time to devote to each assignment.

Play video starting at :2:33 and follow transcript2:33

Our first assignment is based on the humble binary search. 

We have three parts to the assignment, all of which are variations on binary search. 

The first part is simply: write binary search, kind of as a warm up so 

that you can get your coding legs back underneath you and 

understand how the grading environment works. 

So, how this will work is we will give you a short template file of starter code 

in one of the three languages that we support with this class. 

That would be C/C++, Java, or Python. 

You will modify that file to add in your code that solves whatever the problem at hand is, 

and then you will submit that one file. 

So, you'll always just submit one file. And, there are comments in the file that kind 

of go over where you should be adding your code, and what you should be printing 

out, and how you should be interacting with the grader, and things like that.

Play video starting at :3:21 and follow transcript3:21

But, in general, 

there's going to be an interface where you can talk to the grader. 

In this case, there's a function called call_grader and you pass it in index i and 

it will give you back the value of the array at that particular index i. 

You're only allowed, in this case, to make, at most, 32 calls to the grader. And, 

that should be plenty, if you are, in fact, implementing binary search. 

So, this is what kind of enforces the fact that you have to implement binary search 

to succeed at this problem, because the grader will only answer you for 

32 calls and then it will stop answering you from that point onwards. 

There's also a function called call_grader_local that will let you test 

your code locally, not in the Coursera grading environment. 

At the end, when you have found the index in your array of a value closest to your 

target value, then you just print out that index.

Play video starting at :4:11 and follow transcript4:11

That's the answer. 

And, it's very important to print out exactly the answer and only the answer, 

because, otherwise, the grader could be confused if you print out a bunch of, say, 

debugging output as well. 

So, this should be a very simple starting exercise, the first of the three 

parts of our current assignment, in terms of just a bit more structure. 

So, we have designed all of these assignments so 

that you can run your code locally and then you can also upload your code and 

it can run in the Coursera environment. 

It will run slightly differently in both environments because, when you run it in 

the Coursera environment, 

you'll be using the call_grader function, which talks to, basically, a function that 

we've written on our side that is part of the grading infrastructure. 

When you're running things locally, instead of using call_grader, 

you're going to use a function called call_grader_local, 

which is written into your template code and, 

basically, implements the grader interface for a very simple test case, 

so you can kind of practice locally implementing your code. 

In this case, when you call call_grader_local, 

it's going to assume a very simple ten element array with the values 1000, 

2000, up to 10,000, and a target of 8400, which is our course number.

Play video starting at :5:22 and follow transcript5:22

So, that will give you the ability to at least test out your program. 

The index within the array that should be closest would be the one that corresponds 

to the value of, I guess, 8000. 

And so, if you're talking about zero based indexing, 

that would be index seven within the array. 

If your program prints out seven, that would be considered the correct answer 

on this simple test case. We'll have a number of test cases, 

typically, with every single problem or part of a problem. 

In this case, we'll have ten test cases. 

The first one is not counted because it's the same as the one that I just described, 

that's kind of there for local testing.

Play video starting at :5:54 and follow transcript5:54

And then, the nine other test cases get progressively more difficult, 

larger and larger array sizes. 

In this case, your score is either a 100 or a zero on every test case because you 

either get the right answer or you don't get the right answer. 

There will be some problems where partial credit is awarded and 

you'll get a score between 100 and zero. 

Communication between your program and 

the grading environment is often done through environment variables. 

So, the grading environment will set an environment variable for N and T. 

So N is the array size and T is the target that you're searching for in the array, 

and that's how your program will learn those parameters 

when it starts. You'll actually see code in the grading stub that 

you're given that pulls those values out of the environment so 

you don't have to worry about how that's actually done, 

but that's how we communicate some information to your program so that it 

knows some of the relevant parameters of the problem it's trying to solve.

Play video starting at :6:47 and follow transcript6:47

Let's talk about binary search for just a second 

because this assignment is all about the wonders of binary search. 

It may seem like a simple algorithm that you can talk about in five minutes, as 

the very first algorithm in an algorithms course, but 

binary search has a lot of really, really cool extensions that you can consider. 

We've actually talked about some of them already, and 

we'll see quite a few later on in this course as well. 

So, I believe, when we talked about average case analysis, we talked about 

interpolation search, which is basically binary search that makes more informed 

guesses as to where it expects to find the element that you're looking for, 

assuming that the elements have been drawn from a known probability distribution 

so you can make informed guesses about where you expect to find the element 

you're looking for. 

And, if properly implemented, 

you can actually prove, with some slightly messy mathematics, that the expected 

running time of interpolation search is actually log of log of N, 

which is actually much faster than the log N running time of binary search. 

We also kind of talked about the rough reasoning behind that, 

that, kind of, you're roughly reducing your problem size from N to square root of N to 

square root of square root of N, roughly, in each iteration. 

And, anytime you do that, if you can kind of reduce from N, to root N, 

to root root N, and so on, 

that leads to a log of log of N, number of iterations in total.

Play video starting at :8:7 and follow transcript8:07

Another situation where you actually get that exact same running time is another 

fun case of binary search where you're content with an approximate answer. 

So, instead of getting the exact index of the target, 

suppose you're okay with having a small multiplicative error. 

So, the ratio between your index and the correct index, maybe, is like 1.01, at worst. 

You're off by like 1% in a multiplicative error sense. 

What that kind of means is that you run binary search until 

the range containing your answer is quite narrow. 

So, if you look at the ratio between the upper and the lower bound of your range, 

that's say, at most, 1.01, that means you're going to be off by, at most, 1% no matter 

where you pick your answer within that range. 

And, it's actually really easy to achieve this sort of, for 

any constant multiplicative error of your choosing, 

you can run binary search and get down to that multiplicative error by simply using 

the geometric mean as your next guess instead of the arithmetic mean.

Play video starting at :9:6 and follow transcript9:06

Normally, in standard binary search, your next guess is the average of the upper and 

the lower endpoints of your range. 

With the geometric mean, it's the square root of the product of the upper and 

the lower endpoints. 

And you can show that, if you use that choice, then this error measurement, 

the ratio of the upper to lower bound, 

that actually just square roots itself at every step. 

That's actually really easy to see. 

And, because you're square rooting and you start with an N divided by one, 

you're square rooting it all the way down to some constant target error bound of 

your choice. 

That's why you get this log of log of N number of iterations. So you can 

get an approximate answer with binary search much faster than an exact answer.

Play video starting at :9:47 and follow transcript9:47

When we study dynamic programming and optimization later on in the class, one of 

our example problems is going to be binary search with asymmetric guessing penalties. 

So, maybe you're penalized $1 for every guess that's too low and $99 for 

every guess that's too high. 

Maybe guessing too high has more dramatic consequences, 

like it destroys your sample or something. 

And so, that's actually a pretty realistic problem, 

and we'll see how to optimally come up with a guessing strategy that minimizes 

the worst-case amount of money that we're going to spend. 

And then, finally, 

binary search is typically articulated as searching a range for a target value. 

What if you don't have an upper bound on that range? 

What if I just say I'm searching for a positive integer, but 

I don't know how big it might be?

Play video starting at :10:30 and follow transcript10:30

That kind of changes the ballgame quite a bit. 

A very standard way that you do this sort of guessing is you guess 1, 2, 4, 8, 16. 

You keep doubling your guess until, eventually, you're too high and 

now you have a range. And, you can binary search that range. 

And, since you kind of doubled your way up to the upper bound, 

that was kind of a logarithmic number of guesses. 

And then, you have the logarithmic number of guesses in binary search. 

So, you end up spending about two log N guesses.

Play video starting at :10:55 and follow transcript10:55

And, you can actually do better than that, if you're very clever. 

But, this has a surprisingly wide range of applications as well. 

You could actually connect this with schemes for encoding integers for, 

like, a communication over a digital communication wire 

where you're transmitting N in some sort of a binary representation. 

Because, if you think about it, the problem of, "How do I write N in binary 

or some sort of binary representation?" That's kind of equivalent to, "How can 

I guess N with a protocol that involves binary questions like too high or too low?" 

If you think about the binary number that represents N, that is actually what 

you get when you run binary search and you answer too high or too low, and 

a zero bit is kind of a guess of too high, and a one bit is a guess of too low. 

So, that basically is equivalent to describing N in binary.

Play video starting at :11:48 and follow transcript11:48

So, any sort of protocol for guessing N can actually be 

translated into a means of encoding N as a binary string. 

And, some of the best encoding schemes for encoding integers for 

transmission over a digital communication wire, 

they're based on these sorts of extended binary search ideas. 

So, lots of exciting things you can do with just regular old binary search. 

But, I should probably get back to the assignment at hand. 

Our assignment is based on the use of binary search in optimization. And, 

we'll actually study a couple of ways that binary search ties in with optimization, 

once we get to optimization later on in the semester. 

One very obvious way is that if you're trying to, say, maximize a function, 

then a lot of times you can maximize a function via a method that basically kind 

of evokes binary search.

Play video starting at :12:39 and follow transcript12:39

So, in this case, on the left here, 

I'm maximizing what's called a unimodal function over one dimension. 

And so, unimodal function basically increases up to a point and 

then decreases. 

And so, how can you maximize such a function? 

Well, one way to think about it is if you have a pair of brackets 

that surround the optimal solution of your function, you're kind of like, moving 

those brackets in to kind of close in on the optimal solution. 

And so, in every step, 

you can maybe take the bracket that has the worst function value and 

scoot it inwards a little bit to kind of close in your set of brackets 

so they continue to enclose the optimal solution, but 

the range gets smaller and smaller. 

You can actually do the same thing in higher dimensional spaces. 

So, if you imagine a function defined over a two-dimensional space, 

imagine, over this triangle, there's like a surface over top of it that 

describes the function that you're trying to maximize.

Play video starting at :13:31 and follow transcript13:31

And so, we're trying to find two parameters now that maximize that function. 

How do we bracket an optimal solution? 

Here, it actually takes a triangle to bracket our solution. 

And, in general, in D dimensions, you get essentially a triangle with D + 1 corners. 

It's called a simplex in higher dimensional space. 

But you use that to bracket your solution. 

And in every step, you simply take the corner of your triangle, your simplex, 

that has the worst function value, and you move it a little bit in the direction of 

the other corners, kind of compressing in your triangle your simplex 

as you kind of home in on the optimal solution value.

Play video starting at :14:8 and follow transcript14:08

This is sometimes called the Nelder-Mead algorithm, or simplex search, 

because you're kind of refining a simplex that brackets your solution over time. 

Sometimes, it's also called the amoeba search algorithm, kind of playfully, 

because you can regard this little triangle as a single celled amoeba 

that's kind of, like, scurrying around, trying to close in on a food source. 

If you want to be more exotic about how this works, 

you can actually move this bad corner point even more aggressively, 

so it moves past the average of the other solutions and 

actually makes the triangle tumble end over end. 

So, the triangle can actually move. 

It doesn't just have to shrink around the optimal solution. 

It can actually kind of tumble around in the plane until it finds a good solution, 

and then it can close in on that solution. 

The hungry amoeba is on the prowl, and it's always connected to its 

environment on these legs that define the corner points of the simplex.

Play video starting at :15:2 and follow transcript15:02

And, one of the legs always picks up and moves to a new place in space. 

So, this is kind of the vision that we're going to go with. 

We're going to try and 

optimize a function, using binary search. To make things as simple as possible, 

we're going to stick with one dimensional functions and 

we're going to stick with unimodal functions. 

So, a function that increases up to a point and then decreases so 

it has a well-defined maximum at some point. And, we're going to be optimizing 

those functions over the unit interval from x equals 0 up to x equals 1. 

So, how might we do that with binary search?

Play video starting at :15:36 and follow transcript15:36

Well, a couple of ways we could think about doing it. 

One, is you could look at the middle of the function, kind of the midpoint, 

the one half point, and you could evaluate the function at two very closely spaced 

points at that midpoint. 

And, if you do that, that will approximate, it will allow you to approximate the slope 

of the function in the middle or, essentially, its derivative, 

and, based on that, you can tell which direction the function is increasing. 

So here, with the two evaluations in the middle, 

you can see the function is increasing if you go to the left. 

So, clearly, you should recurse to the left. 

That's where you're going to find the maximum of the function. 

So, with two very closely spaced evaluations, you can decide to go left or 

right, very much like a standard binary search would. And, you're going to kind of 

get closer and closer to the optimal solution as you continue to iterate.

Play video starting at :16:21 and follow transcript16:21

You could also use what's called sometimes Ternary search. 

In fact, the previous example was an example of ternary search 

just with points that are very closely spaced together. 

A lot of times we evaluate at two points in our range that 

are kind of evenly spaced out. 

So we divide the range up into three segments with those two points— 

That's why it's called ternary search instead of binary search. 

So, if you pick maybe the one thirds point and 

the two thirds points in your current interval, and 

you evaluate the function at those places, and you look at those function values, and 

you look at the function value at the beginning of your interval and 

at the end of the interval, then, based on the relationship of those values, 

you can actually figure out whether you can safely exclude the last third or 

the first third from consideration. 

Here, we can actually safely rule out the last third because, if you imagine, 

you know, what would it take for the optimal solution to be in this last third? 

Well, since there's a decrease from this point to this point, the function would 

have to increase again to have a maximum appear in that last third, 

and that wouldn't be possible if the function is indeed a unimodal function.

Play video starting at :17:29 and follow transcript17:29

So, you can easily just look at the relationship between the values at 

the start, the end, and this kind of first and second 3rd. 

It doesn't have to be exactly the one third or two third point. 

It can be any two points within your interval. 

But then, you can restrict your search by removing from consideration either 

the first segment here or the last segment and 

recursing on the remaining two segments. 

And then, you'll repeat the same procedure within those two segments, 

again picking two points for evaluation. 

There's actually a really cool variant on this. 

Sometimes it's called golden section search or Fibonacci search, 

where you actually use the golden ratio.

Play video starting at :18:7 and follow transcript18:07

This number 1 plus root 5 over 2 it's approximately the ratio of two consecutive 

Fibonacci numbers. 

It shows up in the surprising number of places in nature. 

It's kind of like an e or pi in that regard. 

So, what you do is you actually do ternary search, 

but with the two points that you choose spaced out just right so that the ratios 

between these segments, well, the segment lengths are kind of in ratios, 

phi to 1 to phi, where phi is the golden ratio. 

If you do that, then when you recurse in the next iteration, then one of your 

two points will actually line up with one of the points from the past iteration, 

meaning that you don't actually have to reevaluate the function at that point. 

So, you kind of save one function evaluation per step if you use this kind 

of clever idea of golden section search. 

So you make a lot more progress per function evaluation than you would with 

a standard ternary search.

Play video starting at :19:3 and follow transcript19:03

Just kind of a fun aside, it's a very clever idea. 

So now, we can talk about the second part of our assignment. That is basically 

to implement ternary search, or whatever variation or flavor of ternary 

search you would like for finding the maximum of a unimodal function. 

The function is, again, going to be described by just an array, and 

you're going to be able to interact with that array, again, using a call_grader function 

just like with the first part. 

So, you call call_grader on i and it will tell you the value of the array in 

position i. And, you're allowed only, at most, 64 function calls, 

similar to the upper bound that we had with binary search. 

Using that many function calls, 

you should be able to home in on the array value that has the maximum.

Play video starting at :19:50 and follow transcript19:50

That's your goal, is to find the index of the array element that is the largest. 

If the contents of the array are indeed a unimodal function. 

So, all you have to do is implement this idea of ternary search. 

I would recommend maybe just starting with the simple idea of breaking your search 

interval into three even sized pieces, and using whatever appropriate logic to rule 

out the first or the last piece, and then recursing on the interval that remains. 

That should be enough to give you full credit for this part. 

So, a similar implementation structure as with the first part. 

So, you'll be submitting one file and, at the end, you should print out just one 

number which is the index of the maximum element in your array.

Play video starting at :20:33 and follow transcript20:33

You'll have, again, ten test cases. And, you'll get a score of 100 or 

zero, if you're correct or not, 

because there is exactly one array index that is the maximum in all cases. 

You'll, again, have the ability to run locally on a simple example if you want. 

So, hopefully you can develop your code locally, and 

then submit it to the grading infrastructure when it's ready. 

Alright, so, now we're ready to talk about the final part of the assignment. 

That's kind of the more open ended, more challenging part. 

And this one actually does have a very, you know, kind of critical, 

real world motivation behind it.

Play video starting at :21:7 and follow transcript21:07

So, the setting here is that we have some sort of very complex model or 

simulation, and we're trying to find the right way to set a key parameter for 

that model or simulation so that it outputs the optimal thing, basically. 

So, maybe a use case that we could use as a running example here is we're making 

some sort of a biomedical model that simulates the effect of 

a cancer treatment, for example, maybe a radiation treatment or 

maybe some sort of a drug that's supposed to treat cancer. 

And so, the critical parameter here is the amount of dosage level. 

How much radiation? How much dosage of the drug should you feed to the patient? 

And then, what you can then get as output of the simulation is, basically, 

the response telling you how effective that level of dosage was. 

So, if you don't give enough dosage, 

then you don't do enough to get rid of the cancer cells.

Play video starting at :21:58 and follow transcript21:58

But, if you give too high of a dosage, then you also have an adverse outcome because 

it affects the surrounding tissue, and that's also bad news. 

And so, there's kind of a sweet spot where you give just enough dosage to mitigate 

the cancer cells, but not harm as much as possible the surrounding tissue. 

And the simulation that you're running is capable of telling you 

roughly, from a given dosage level, what the response is likely to be. 

So, our goal is going to be to maximize this unimodal function. 

Now, we're talking about maximizing a real valued function over a unit interval, 

over the range from zero up to one. 

In most cases, in many cases, including this one, 

it can be very expensive to evaluate your model. 

If this is a very complex simulation or a finite element model or what have you, 

then it might take hours or days or much longer to just run the model once.

Play video starting at :22:50 and follow transcript22:50

And so, kind of running a bunch of iterations of binary search would take 

a long time. 

And so, what we might do instead is we might actually run several kind of 

concurrent copies of the simulation at different dosage levels, 

kind of running them in parallel or in a distributed setting. 

You just run them all on different machines. They don't depend on each other. 

We're going to actually test, probe the function at a number of 

different places, at, say, K different places. 

So, we're allowed to actually kind of do a parallel version of binary search, 

and our program will be given this value K. 

So, each iteration, you'll actually be able to probe the function at not one place, 

but at K different places in parallel.

Play video starting at :23:32 and follow transcript23:32

And then, we'll be able to do that for a number of rounds. 

So, we run all these simulations in parallel, 

that takes several weeks of compute time, and then you get back all those answers. 

And, based on all those answers, you can somehow rule out parts of your search 

space and restrict the search to a much smaller interval. 

And then, again, you can pick K values to probe and run those in parallel. 

And you can do this for up to R rounds, 

where R is probably a small number because it's so expensive 

to evaluate the model or the simulation. 

And, our goal is to come as close as possible to the optimal solution of 

the function using those K times R evaluations. 

R rounds, where each round, you're allowed K evaluations of the function.

Play video starting at :24:14 and follow transcript24:14

So, the setup here is going to be similar to before. 

We want to find the value of x, which is going to be a double, a real number, in 

this case, between 0 and 1, that leads to a maximum value of our unknown function f. 

The only way that we can learn about that function f is to kind of probe it by 

calling the call_grader function. 

And here, instead of call_grader, giving you one function value back, 

you can ask it to probe K values at the same time. 

So, you give it a vector of K different values of x that you'd like to 

get the answer for; 

it'll give you back f(x) at those K different values. 

And then, you can do this for 

up to R rounds before the grader stops talking to you. 

And, at that point, you have to return what you think is the best value of x.

Play video starting at :24:56 and follow transcript24:56

And here's where you will get partial credit based on how close you are to 

the true optimal value of x. 

If you get, like, I think, within 10 digits of accuracy, 

I think that's worth 100 points. 

But, we have a scoring function behind the scenes that will give you a score 

based on how close your value is to the true optimal solution for x. 

Now, to make this even more realistic, we've introduced kind of a fun curveball, 

where when you call the call_grader function, 

it will evaluate the function at every value that you want for x, 

but it won't just give you back f(x). 

You'll actually get back f(x) plus or minus a little bit of noise. 

Because a lot of times when you run a simulation or a model, 

there's some sort of like Monte Carlo simulation going on in that model. 

And so, the randomization involved with that simulation might give 

you slightly different answers in each run of the model, 

even if you run it on the exact same parameters each time.

Play video starting at :25:52 and follow transcript25:52

And so, this is very realistic. 

It's a real world situation where things are, unfortunately, noisy. 

So, we can't actually see the actual function f. 

We can only see f plus a little bit of noise. 

And, we would still like to come up with relatively robust and stable ways of 

estimating the value of x that corresponds to the true maximum of this function f 

which we know on the grading system, because we have an actual f function in 

mind behind the scenes that we're giving you only noisy viewpoints on it. 

So, when you ask to evaluate it, you get back f(x) plus a little bit of noise. 

You never get to see the actual function f. But, we know what the actual function 

is, so we know how to assess the answer that you hand back at the end of the day.

Play video starting at :26:37 and follow transcript26:37

So, here the same scoring is going to be used. 

You're going to be scored on how close to the optimal solution you are, 

and you'll be given 20 test cases. 

The first five involve no noise at all, so 

those should be the easiest to home in on the optimal solution. 

The next will involve a little bit of noise, then a little bit more noise. And 

then, the last cases will involve a lot of noise. 

It'll be the hardest test cases. 

It will likely be especially challenging with the harder test cases 

because your function may not even start looking unimodal anymore.

Play video starting at :27:7 and follow transcript27:07

If you evaluate it at K places, 

it may not even have a unimodal profile because of the noise. 

And so, you'll have to think very carefully about how you restrict your search and 

kind of narrow your search to smaller and smaller intervals, 

given the presence of this noise is going to make it harder to follow 

the same rules that you were following before to narrow your search, basically, 

because the function may not quite look as unimodal as it did with no noise. 

So, this will be hopefully a fun, somewhat open ended version of the problem. 

You could also probably make this into a full fledged research problem, 

if you wanted to take it to the next level. 

But, if you do something quite reasonable in solving it, then you should be able to 

get certainly enough points to earn a decent grade on the assignment. 

But, hopefully, this gives you a fun chance to be creative and 

try different solution approaches and see which one works the best. 

So this is Assignment 1, and wishing you the best of luck in your implementation.