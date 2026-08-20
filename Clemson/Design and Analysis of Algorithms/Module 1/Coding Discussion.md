[MUSIC] 

One of the goals in this class is to look at algorithms, not only in terms of their 

high level mathematical analysis, but also in terms of actual implementations. 

I think there's a lot of benefit to this sort of balanced outlook where you see 

both sides of the algorithmic picture. 

A lot of times my students tell me, you know, "hey, 

I understood at a high level the concept that you talked about in lecture, but 

I'm having trouble translating that idea from what's in my head into actual code." 

And so, the goal here with these implementation lectures that we're going 

to include with all of our modules is to do exactly that. 

We're going to show how the algorithmic ideas of the current module can, hopefully, 

be translated into code in what is, hopefully, a straightforward fashion. 

So, that's basically what we're going to do here. 

In all of these coding lectures, I'm just going to write some code and 

think out loud and kind of walk through the process of implementation.

Play video starting at :1: and follow transcript1:00

And, we'll also get a chance to review, hopefully, 

some of the major concepts that we've talked about in the module. 

So in this module, I thought, it's the module on fundamentals. 

We've covered a lot of ideas. 

We haven't really covered one central idea that would be an obvious choice for 

implementation. 

So, I thought maybe, as a warm up, we could structure this discussion kind of 

like a mock technical job interview. 

As you guys know, technical job interviews often involve problems that are very 

algorithmic in nature. 

Some of them look like they've been pulled directly off of a programming contest, 

for example.

Play video starting at :1:34 and follow transcript1:34

So, it actually can be very advantageous to be comfortable thinking on your feet, in 

the context of a technical job interview, working through the design, analysis and 

implementation of a solution. 

So, that's kind of what we're going to think about doing today. 

I've picked a problem that some of my students have actually been asked in real 

technical job interviews. 

It's the old rectangle in a histogram problem. 

And this problem also, I think, 

showcases a couple of key ideas from this module as well. 

So, hopefully, it's a good problem to discuss. 

The problem itself is, given a histogram as input, 

so N number is describing the heights of the bars in the histogram 

tell me what's the largest rectangle I can fit into that histogram?

Play video starting at :2:14 and follow transcript2:14

So, the rectangle of maximum area? 

So, that's the problem. 

Whether or 

not this is the world's best technical job interview question is probably debatable. 

It would really surprise me if an interviewee was able to come up with, on 

the spot, the best possible algorithm for solving this 

maybe, unless they've seen it before. 

But, maybe that's not the point of a technical job interview. 

Maybe the point really is to just observe somebody's thought process when faced with 

a novel problem. How do they think through the process of solving the problem and 

implementing it in code?

Play video starting at :2:46 and follow transcript2:46

So, that's what we're going to do here. 

If I'm now an interviewee and I see this problem, 

what thoughts start to go through my head about how I would address it? 

So, I have to find the best rectangle. 

How do I do that? 

Well, maybe I need to loop over a large number of candidate rectangles and 

take the best one. 

So how do I do that? 

How do I enumerate all of the prospects for 

what could potentially be the optimal rectangle?

Play video starting at :3:12 and follow transcript3:12

Well, I guess, rectangles, they're characterized by four sides: the bottom, 

the top, the left, and right. 

All possible rectangles that I would be considering live on the same base. 

So, the bottom isn't interesting, but I still have the left side, 

the right side and the top. 

And so, maybe as a starting point, I could just loop over all choices for 

the left and the right sides of all possible candidate rectangles. 

Once I've done that, once I fixed the left and the right hand sides, 

the top is actually apparent because the top of the rectangle 

I want to make it as tall as possible. 

It would be, I guess, the minimum height of the bars that go between L and R. 

So, that's my first thought, my first attempt here.

Play video starting at :3:50 and follow transcript3:50

Loop over all choices for left and right; 

within those choices, find the height of that candidate rectangle; 

compute the area of the candidate rectangle; 

and just remember the best area that I've seen so far. 

So, let me maybe start implementing that, and we'll see where that takes us. 

A few notes on just coding, I guess. My language of choice, 

the one I'm most comfortable with, is C++, 

so I'll be writing all of my implementations in C++. 

You're, of course, welcome to use whatever language you like in your implementations. 

I'll try and write my code in simple terms so it's easy to understand and 

translate into other languages. 

I'm probably also going to be foregoing a lot of best practices when it comes 

to software engineering.

Play video starting at :4:32 and follow transcript4:32

And this is in the interest of just writing simple implementations that showcase 

the essence of the algorithms that we're trying to implement. 

I'm going to possibly use global variables; 

I may not always check return values of functions; I may not code defensively 

All sorts of things that you would probably want to reconsider if you were 

writing actual, production level code. 

That's not the point here. 

I'm also a little bit old fashioned. 

I like to use the emacs text editor, so 

I'm going to make a file called hist.cpp and start writing code there. 

You're, of course, welcome to use whatever development environment you 

are more comfortable with. 

It's definitely highly recommended to learn a development environment well, so 

that will help you a lot with your implementations.

Play video starting at :5:15 and follow transcript5:15

So, let's go ahead and get started. 

I guess, the first thing that you always do with any implementation is you want to 

read the input in. And so, I have to finally start making some choices. 

What's an appropriate data structure to use to store my input? 

And, I might just use a C++ vector, a vector of integers. 

Maybe I'll call it H, 

because these will be the heights of the bars of in my histogram. 

Remember, that a vector is an array that automatically upsizes itself as you're 

adding elements to it one by one.

Play video starting at :5:44 and follow transcript5:44

And, that's probably appropriate because I may not know in advance how many elements 

I'm going to be adding from my input. 

So, the code that's actually going to read the input and 

push everything into the vector would look something like this. 

As long as I can read something in from the input, 

I'm just going to tell the vector to add it at the end. 

So H.push_back(x). So, that reads in the input. 

How much time does that take? 

Remember from our discussion on data structures that most operations on 

a vector are very fast.

Play video starting at :6:14 and follow transcript6:14

Most of the time, when you add a new element to the end of the vector, 

it's just constant time. But, occasionally, the vector needs to pause and 

upsize its memory, and that's rather slow. 

But, remember that that amortizes out over a sequence of operations, 

so this actually takes constant amortized time per pushback operation 

So, linear time in total. 

So, so far we're in good shape. 

I guess a little bit of maybe just housekeeping 

If I'm using vectors, I probably need to include the header file for vectors, and 

if I'm using stream input from using cin, I think I also need to include iostream. 

Okay, and then, I guess, also technically, the name of vector 

It's a construct from the standard library, 

so the vector is actually called std colon colon (::) vector, and 

cin is actually called std::cin. 

To maybe avoid having to write std:: all over the place, I'm just going to 

adopt the standard namespace. I'm going to say, using namespace std, 

and then I don't need to write std:: all over the place.

Play video starting at :7:20 and follow transcript7:20

This is also, I think, sometimes frowned upon as a software engineering practice, 

but, again, our goal here is simplicity and 

making the algorithms appear as simple as possible. 

Okay, so I've read the input. 

I guess I need to print the output. 

So, I'll just print out what I get when I solve the problem. 

And, of course, now I'm done. 

I like to, by the way, leave my main function relatively uncluttered and 

code in somewhat of a top down fashion, so filling in low level details as I go. 

So, I've written everything at a high level now, and 

all I need to do is write my solve function.

Play video starting at :7:55 and follow transcript7:55

So, let's just go ahead and do that. 

That should be pretty straightforward, 

given the simple algorithm that we're using as our starting point. 

So remember, my solve function is going to just loop over all possible left and 

right endpoints, 

so I should just have a double for loop here. 

So, loop over all choices of L, starting from 0 and 

going up to N I guess the size of my histogram. 

I guess I haven't even defined N, so maybe I'll set N to be the size of my histogram. 

This is something that I could have just written H.size instead of N, but I suspect 

I'm probably going to be using N quite a bit over the course of the algorithm. 

And so, a lot of times if you're using a complicated expression, 

many times, it makes the code look a lot simpler to give that complicated 

expression just a simpler name.

Play video starting at :8:40 and follow transcript8:40

So, loop over all left endpoints, then, within that, loop over all possible right 

endpoints. I guess that loop can start at the current left endpoint. 

And so, what do I want to do inside that for loop? 

So, within that for loop, 

I want to figure out what's the height of the rectangle with those particular sides. 

So, what's the height of this rectangle? 

Maybe I'll leave that unspecified just for the moment. 

I'll write a function later on that tells me the height that's the minimum height of 

a bar between L and R.

Play video starting at :9:12 and follow transcript9:12

And then I need to figure out what's the width of that rectangle. 

That's just the difference between R and L. And, I think I need to add 1 to that. 

And now that I have the height and 

the width, I can find the area. That's just the product of height times width. 

I'm writing this code in a very, you know, I could have written all of this in like 

one line of code, basically, but I'm trying to write it out very cleanly so 

that the intent of what I'm doing is very clear. Right?

Play video starting at :9:39 and follow transcript9:39

The code that you write should express the intentions of yourself as 

the programmer. And, it should be easy for someone to come in after you and 

look at your code and understand what you're doing. 

So, I've looped over every candidate rectangle; 

I've computed its area. 

I need to just remember the best one. 

So, let's maybe just do a running max where we remember the best possible area that we 

have seen over this entire process. 

So, just keep track of the maximum area as we loop over all of these choices and 

then return that largest possible area. 

So, now all I need to do is write the get height function.

Play video starting at :10:14 and follow transcript10:14

I can just go ahead and do that, and then we'll have a working, 

hopefully, implementation of our first algorithmic idea. 

So, I want to find the height between L and R. 

That's just going to be the minimum bar height in that range. 

So again, I'm going to have a for loop that just keeps a running minimum. 

So, the minimum height in this range. 

Maybe I'll start that out at the height at the left endpoint 

and then I can loop over all choices from L plus one up to R. 

So i = L + 1; i less than or equal to R; i++.

Play video starting at :10:46 and follow transcript10:46

And then, my minimum height is just going to be the min of min_height and 

the height of the i’th bar. And then, return that at the end. Okay. 

All right, so we have our first candidate for an implementation. 

Let's go ahead and try compiling this and see if it actually runs properly. 

I guess, no guarantees in these videos that everything 

will just work properly from the get go. 

We may need to do some debugging. And, there's some value to being able to 

talk about how to do effective debugging, as well.

Play video starting at :11:19 and follow transcript11:19

I've created, just to simplify things, 

an input file called input10.text that we can run on. 

So, this is just an input of size ten. 

There are ten bars in the histogram. And you'll notice that these 

middle four bars are conspicuously taller than all of the others. 

And so, it should, hopefully, end up being the case 

that the optimal rectangle will be the one determined by those four bars. 

And maybe we can actually figure out what the answer will be 

in that case. 

The minimum height of those four bars is 1569.

Play video starting at :11:52 and follow transcript11:52

And so, if I load up a calculator and 

I just take 4 times 1569, that gives me 6276. 

Hopefully, that's the answer that we're going to get when we run our code. 

So, I can go ahead and compile. What are they called? hist.cpp And okay, nice. 

We compiled properly. 

And g++, or compiler generates a default executable called a.out.

Play video starting at :12:14 and follow transcript12:14

I'll then just run that and I'll feed it in as input, input10.txt, so that 

redirects this file so it gets redirected in the standard input. And it prints out. 

All right, we're on a good track. 

We have an answer 

that is what we expected to get. 

So, so far we're in good shape. 

Maybe it makes sense to think about the running time of our algorithm. 

So, let me go back to our code and see if we can analyze the running time.

Play video starting at :12:41 and follow transcript12:41

That's actually pretty straightforward because we can just use simple loop counting. 

We've got a nested for loop here, and then inside that we call the get height 

function, which has in it another for loop. 

So, we basically have three nested for loops, each of which can be looping up to, 

say, order N times. 

And so, the running time here is going to be nothing to write home about. 

It's going to be N cubed, which is not exactly super fast. 

Maybe, I'll kind of express my displeasure here in code. 

So N cubed 

So, we have a working algorithm, but it's not particularly fast. And, 

that's still a good starting point.

Play video starting at :13:17 and follow transcript13:17

I would argue, if you're in a job interview, definitely write something 

correct but slow rather than something incorrect and super fast. 

It's better to have a working algorithm as a good starting point. 

So, how do we make this faster? 

Let's go back and look at our setup here. 

Actually, there's one idea that comes to mind pretty quickly about how we can avoid 

one of those loops. 

We're spending an awfully long time looping over the contents of the bars 

between L and R over and over again to determine the height. 

And we actually don't need to do that.

Play video starting at :13:49 and follow transcript13:49

We can actually just keep a running minimum height as we're looping 

our right endpoint forward. 

So, we don't actually need that very inner for loop that computes the height. 

We can just kind of compute the height as we are looping over all choices of R. 

And that should reduce our runtime considerably if we do that. 

So, let's see about implementing that. 

I may actually keep around the old versions of my code so 

that I can compare the output that they produce to the output of newer versions. 

That will also help with debugging and give me some reassurance that maybe 

the newer versions are doing the right thing if they match the older versions.

Play video starting at :14:26 and follow transcript14:26

So, the older versions are more likely to be correct because the algorithm 

here is relatively simple. 

So, I'll keep around solve1, and now I will write a new function called solve2, 

which will be very similar to solve1. 

So, I can probably just copy and paste a couple of things here, 

so I'll have my solve2 function. 

We'll figure out the running time of that in just a second. 

But, to get solve2, I think I can just copy solve1 and 

do a little bit of surgery and, well, let's see what we can get. 

So I'll create this solve2 function. 

So it has the same high level structure as solve1.

Play video starting at :15:7 and follow transcript15:07

I'm looping over all left and right endpoints. 

It's just, now, the height is not going to be determined by calling my 

get height function. 

Instead, I'm just going to kind of keep a running minimum for my height. 

So, height is going to be, you know, the minimum of what it used to be and the, 

I guess, the height at the current right endpoint. 

So, I'm just keeping the running minimum of heights, and 

I guess I probably need to initialize that. 

So, the height's gonna start out at maybe the height of the left endpoint, I guess. 

So, that is essentially all the change I need to make.

Play video starting at :15:41 and follow transcript15:41

That was a relatively small amount of change. And, 

you'll notice that now I only have two nested for loops instead of three. 

And so, hopefully that will cut the running time down from N cubed down to order of 

N squared, which is maybe still nothing to write home about, but 

it's certainly better than N cubed. 

So, maybe I'm only slightly less annoyed 

at that running time. 

So, if I go ahead and, now again, try and compile, 

let me clear my screen just to keep things tidy. 

So, I'll compile hist.cpp, and again, I will run it on my input file. 

This is good to see.

Play video starting at :16:15 and follow transcript16:15

So, I ran both algorithms and they both gave me the same answer. 

So, we're off to a good start. 

And so now, the main question is, can we make our algorithm even faster? 

That's going to be our challenge now, moving forward. 

If we go back and look at the structure of the solution we've built so far, 

I think we're probably going to have to now step away from the approach that loops 

over every possible L and R, because there can be a quadratic number of choices for 

all possible left and right sides of all of our candidate rectangles. 

Any approach that loops over all of them is really doomed to take quadratic time. 

And if we want to do better than order N squared, 

we have to loop over fewer things; fewer candidate rectangles.

Play video starting at :17:1 and follow transcript17:01

So maybe, I guess, instead of looping over all possible left and right sides, 

what if we loop over the top of all possible candidate rectangles? 

Because the top of a candidate rectangle, it is defined by the height of some bar. 

So maybe what I can do is loop over every bar, bar i. And, for bar i, 

assume that it's the one that defines the height of a candidate rectangle. 

Then, just figure out what the width of that rectangle is going to be, 

and that gives me the area. 

And again, take the best one. 

So, if we kind of look at this, we actually can easily figure 

out what the width of that candidate rectangle is going to be from bar i.

Play video starting at :17:39 and follow transcript17:39

I'm just going to scan outwards to the left until I see a bar less than me in 

height, and then I scan to the right until I find a bar less than me in height. 

Let's maybe give those kind of flanking bars names. 

Maybe call them my left and my right neighbors: L of i and R of i. 

So, those two bars kind of define the width of the candidate 

rectangle whose height is defined by bar i. 

Then I can find the area and do the same sort of approach. To make sure that these 

scans, going left and right, don't run off the end of my array, 

just for simplicity, I'm going to add a dummy zero height bar to the beginning and 

to the end of my instance. 

That's just going to clean up the code a little bit.

Play video starting at :18:22 and follow transcript18:22

And I'll have fewer if statements that I'll have to include 

that worry about the possibility of running off the end. 

These loops that go left and right to find L(i) and R(i) are guaranteed to stop 

somewhere. They're going to at least stop at those dummies. 

So, maybe I should go ahead and start writing code for this approach. 

I do worry a little bit that it still kind of feels like we're in the N squared 

territory here. 

Because we're going to be looping over every possible bar i and then for 

every bar i, we're also going to be looping to the left and 

to the right to compute the L(i)'s and the R(i)'s. 

But it turns out, I think there's going to be some insight that will help speed up 

that part of the calculation in a moment.

Play video starting at :19:4 and follow transcript19:04

So, let's go ahead and write code for this new structure and 

get that working first. And then, we'll see if we can speed it up even further. 

So, going back to my code here, 

I guess now we're on to solve3. 

Okay, solve3. I suspect is probably still going to be quadratic in time, 

but we'll verify that after we've written our code. 

I guess, we also wanted to include those dummy zero height bars at the beginning 

and at the end of our input. 

So, I'm going to say h.push_back(0) at the beginning of the input and 

also at the end of the input.

Play video starting at :19:43 and follow transcript19:43

So now, I have added in those flanking zero height bars to my instance. 

I should probably also make sure that doing that isn't going to break my 

existing solve1 and solve2 solutions. And, I think it's not. 

Those two solutions should still operate fine even if I add those dummy 0 height 

bars at the beginning and at the end of the histogram. 

So, at least hopefully, I haven't broken anything. 

So now, let's get started writing solve3. 

I guess solve3 is going to have a slightly different looping structure.

Play video starting at :20:16 and follow transcript20:16

So, I'm looping here fundamentally over all possible bars i. 

And, I guess, I don't have to start at 0 

because the 0th bar is now the dummy 0 height bar. So, I can start at bar 1. 

And I guess, instead of looping up to less than N, 

I can loop up to less than N-1, because I don't want to 

worry about including the dummy bar at the far side of the histogram. 

So loop over all the bars. 

I guess I need to also define N is H.size. 

And then, within my loop over all of the bars, 

I'm going to calculate the area of the candidate rectangle defined by bar i.

Play video starting at :20:53 and follow transcript20:53

So, the height, in this case, is going to be just defined by the height of bar i. 

And the width of the rectangle, that's defined by the difference of those, 

you know, neighboring indices, the R(i) minus L(i). 

And, I think, since those are flanking but outside the rectangle, 

I need to subtract one, I think, to get the proper width. 

And then again, I can calculate the area, which is the height times the width. 

I can find the best area so far, which is just a running max of all of the areas 

that I've seen. And, I'm going to return the best. 

I guess should probably initialize best to 0 at the beginning.

Play video starting at :21:30 and follow transcript21:30

Okay, so this is now my new high level structure for the algorithm. 

It only has one for loop instead of two. 

The only thing I haven't computed yet are the R(i)'s and the L(i)'s. 

In fact, I haven't even allocated a structure for storing the R(i)'s and the L(i)'s. 

Let me maybe just create a vector of ints L of size N and R of size N. 

Those are just going to be the vectors that store those L(i) and R(i) values. 

So, if we just go back and look at the picture, for every rectangle i, 

I need to compute L(i) and R(i).

Play video starting at :22:8 and follow transcript22:08

So, I have to scan to the left until I find someone shorter than me, 

and I need to scan to the right until I find someone shorter than me. 

And those are my left and right neighbor values, my L(i) and R(i). 

So, let's maybe just code that up. 

It's possibly not going to be the most efficient approach yet, but, 

hopefully, it'll at least give us something that works. 

So again, I guess, if I want to compute all of the L(i)'s, how do I do that? 

So, I'm going to loop over all the i's, and, for each one, 

I'm going to compute its left neighbor. 

So, maybe I'll start the left neighbor out at i minus 1 at the bar 

immediately to the left and I'll just keep stepping it to the left.

Play video starting at :22:50 and follow transcript22:50

As long as the height of L(i) is taller than or equal to my height, 

I guess, I keep stepping L(i) backwards. 

So, this is going to basically just keep stepping L(i) backwards 

until I reach a bar whose height is less than my height. 

And then, I can do the same thing to compute all of the R(i)'s. 

I'll just, again, loop over all of the i's. 

I guess I probably could have done a lot of this in one big for loop, but 

maybe it's simpler to kind of see the two being calculated separately. 

So, for every bar, I'm going to start R(i) out at i+1, 

which is the bar immediately to my right. 

And then as long as the height of that bar is taller than me, 

I'm going to step R(i) forward.

Play video starting at :23:43 and follow transcript23:43

Okay, so scan left and scan right until I reach the next bar over 

on both sides that's shorter than me. 

That should compute the L's and the R's, and the rest of the code should now do 

the right thing, because it just assumes that I've computed the L's and the R's. 

So, let's go ahead and compile and run. 

So, ok, this is nice. 

It looks like we're getting the same output 

for input ten. I've also created these other inputs: input 100, input 1000. 

I've created a couple of other inputs of different sizes of N.

Play video starting at :24:17 and follow transcript24:17

Actually, for 

the input 1000, you can see the N cubed starting to strain a little bit here. 

So, this is nice. 

We're getting what looks like the right answer from all 

of our different approaches. 

However, I don't think we are where we need to be in terms of running time yet. 

Because if you look at the calculation for computing the L(i)'s, 

we have two nested loops here. 

Effectively, we're looping over N things here. 

And then, for each of those, 

the while loop inside of this could also be stepping back a fair distance.

Play video starting at :24:47 and follow transcript24:47

So, I think that this, unfortunately, is still an order N squared algorithm. 

So, we're going to need some sort of additional insight in order to be able 

to improve the running time further. 

So, let's take a closer look at maybe the calculation of the Ls and the Rs, 

because that seems to be the slow part of this algorithm. 

The rest,the part that loops over all the i's and 

finds the best rectangle once we've computed the Rs and the Ls, that's fast. 

This for loop right here is just running in linear time because it loops 

over N things and does a constant amount of work in each iteration of the loop. 

So, we need some sort of an insight that lets us compute the L's and 

the R's more efficiently. 

So, let's maybe look at one of those problems.

Play video starting at :25:34 and follow transcript25:34

Let's look at the calculation of just the L's, for example, and 

see if we can speed that up. 

So, along the way to doing that, 

one interesting observation is that the problem that we just talked about 

the one of scanning left until we find someone shorter than us and 

scanning right until we find someone shorter than us, that's almost identical 

to another problem that we have previously talked about in this module. 

So, maybe that will help us with insight that we need. 

We've talked about this so called domination radius problem, 

where you're given as input the heights of N individuals standing in a row and, 

for each individual, you scan to the left until you find someone, 

in this case now, taller than you, that's your left domination radius. 

And you scan to the right until you find someone taller than you. 

That's your right domination radius. 

And your overall domination radius was the smaller of those two numbers.

Play video starting at :26:28 and follow transcript26:28

And I think, previously, we had looked at the question of calculating the domination 

radius of every individual. And, we looked at some nice algorithms for doing that. 

Here, it seems like we need to individually calculate the left and 

the right domination radii, which actually is a little bit different than 

the problem we had considered earlier. 

I think previously, we had built an N log N algorithm that computed the domination 

radius of every element. 

But that approach, unfortunately, 

won't work here because it kind of scans outwards in both directions and 

stops when it hits one of the taller flanking elements. 

So here, we need to actually scan out and find both the left and 

right neighbors of each element. 

So we'll need a slightly different approach, but we actually will be 

able to come up with a neat bit of insight that not only solves this problem and 

the histogram problem, but solves them both in only linear total time.

Play video starting at :27:23 and follow transcript27:23

So, this will give us another approach we could have applied to the domination 

radius problem in our previous discussion. 

So, here's the idea. 

I mean, I guess, really, to illustrate that domination radius and 

the histogram problems are really the same problem, I could have maybe 

drawn the domination radius problem upside down on top of the histogram problem 

to really illustrate that, from every element, I really am doing the same scan. 

I scan to the left until I find someone shorter with the histogram problem, 

which is the same as someone taller with the domination problem, and vice versa, 

scanning to the right. 

So these really are essentially the same problem. 

It's just whether you're looking for someone shorter or 

someone taller on either side of you. 

So, let's look at that process.

Play video starting at :28:9 and follow transcript28:09

We're trying to calculate the L(i)'s or all of the i's. 

Remember, the structure of our algorithm? 

We're looping over all the i's and we're trying to compute for each one, 

what's the L(i). The left neighbor that you get by scanning to the left until 

you find someone either shorter than you, for the histogram problem, or 

someone taller than you, for the domination radius problem. 

And this is in a loop over i. 

So, we're going to be computing this for, you know, i equals 11, i equals 12, 

i equals 13, i equals 14... 

So, that's kind of the structure of the overall loop that we're doing.

Play video starting at :28:43 and follow transcript28:43

I've kind of, at the bottom here, 

I want to think about all of the possible indices in my array that are possible 

candidates for L(i). 

So, if I'm computing L of 11, then all of the indices to my left, 

1 through 10, are possible candidates. 

When I move forward and now try and compute L of 12, 

now 11 is added to that candidate set. 

So, the set of possible candidates is expanding. 

Every single time I step i forwards, 

a new element gets added to the end of my list of possible candidates 

that could be L(i). 

I'm actually working my way towards understanding what's a good data 

structure for storing this set of candidates? 

So, as I loop i forwards, I'm adding elements into that set 

of possible candidates from which I'll be selecting L(i).

Play video starting at :29:30 and follow transcript29:30

Okay, one more insight that I need. If I go back to maybe the snapshot in 

the middle of my algorithm where I'm calculating L of 11, in this case, 

choosing the best choice from among my contenders for L(i). 

So, to do this, remember, we scan backwards until we find 

the first bar that has a height less than us or bigger than us. 

We scan past a number of possible bars along the way. 

And I think the crucial insight here is that the bars that we scan past, 

they're not only not the answer for this value of i, but 

they will actually never be the answer for any future value of i. 

We can kind of permanently disqualify them from consideration forever for 

the rest of our calculation. 

So next, we're moving on to calculating L(12) and L(13) and L(14).

Play video starting at :30:27 and follow transcript30:27

As I continue stepping forward, these red elements are never going to be the answer 

for any of those future values of i because, I guess maybe that's most apparent 

from the domination version of the problem, because those red elements are now 

blocked by this green element right here. 

So, anybody on the right that we consider in the future will not be able to see any 

of these red elements because, well, 

you're going to bump into the green element first. 

So, this is interesting. 

If you look at our list of contenders, now we're able to actually remove elements 

from the end of this list because they will never, ever be valid choices for 

us or for anybody else for any value of i that we consider in the future. 

And so, this might actually suggest a data structure that we should be using for 

our list of contenders. 

Because, remember, what we're doing to that list of contenders is, 

as i is scanning forward, we're adding new elements to the top of that list. 

But we also seem to need the ability to remove elements from the top 

of that list when they are disqualified from consideration.

Play video starting at :31:31 and follow transcript31:31

And so, it actually makes sense to think about storing this list of contenders as 

a stack because we're basically adding and removing things at the top of that list. 

And this also suggests kind of the overall algorithm. 

So, I'm trying to compute L(11), L(i) for i=11. 

I'm scanning backwards. 

In terms of the list of contenders, 

that means I'm basically popping elements off of that stack as long 

as they correspond to elements that I'm scanning past that have higher heights 

than bar i. 

And then I finally end up sitting on an element that has a lower 

height than bar i. 

That's going to be L(i).

Play video starting at :32:9 and follow transcript32:09

And so, in terms of the operation phrased as our stack here, 

this is actually relatively straightforward. 

For every value of i that I consider, I'm just going to pop off of the stack all of 

the elements that now become disqualified because they're sitting at the top 

of the stack and they have heights that are taller than me. 

And I'll keep doing that until eventually the top element on the stack has 

a height shorter than me. And that is going to be my L(i) value. 

So it's very easy to find L(i) because I just remove all the non contenders from 

the stack and the one now sitting at the top of the stack is going to be L(i). 

And so, I just do that and then I have to finally, again, push i as a new contender 

onto that stack. And then I can step forward and consider future values of i.

Play video starting at :32:55 and follow transcript32:55

So, I have a very simple approach that's based on a couple of straightforward 

stack operations for each of the i's that I consider. 

And, if I were to have kind of done this properly and 

really taken a snapshot up to this point, what would have happened is I would have 

been disqualifying elements as I'm going. The set of elements that remain, 

the ones that have not been disqualified, kind of the remaining contenders still 

on the stack, they're actually going to have a really nice structure to them. 

So, if you look at the bars that are still in contention, they're going to be 

kind of an increasing series of heights for the histogram problem and 

a decreasing series of heights for the domination problem. 

And so, kind of the operation here, 

let's maybe think in terms of the domination problem, 

every time we add a new bar, every time we process a new element i, 

that's basically going to look to the left 

and it's going to pop off of the stack 

all of the elements that are shorter than that guy. 

And then, we add him to the top of the stack, 

leaving the stack in monotonic order. 

So there is some really nice structure to the set of contenders in our stack.

Play video starting at :34:8 and follow transcript34:08

If we've disqualified all of these red elements 

those are the ones that we're never going to be able to see again 

the remaining elements form this monotonic sequence of elements that we could still 

conceivably see from someone here on the right hand side looking to the left. 

So, all we have to do is change our code around to implement things in 

terms of this stack here, 

so every iteration for each i, instead of just scanning to the left, we're now 

going to be popping elements off the stack as long as they're taller than us. 

We set L(i) to the top element on the stack and then we push i. 

Everyone remember those three steps. 

That's what we're going to have to implement next in code. 

So, if I go back to my loop here where I compute all of the L(i)'s, I guess I'm 

going to have to have a stack that's going to hold my list of contenders. 

Maybe initially, the first contender is going to be just the dummy zero height 

element on the very left hand side of the histogram.

Play video starting at :35:3 and follow transcript35:03

And I think that's never going to get popped off of the stack 

because that's a fail safe. 

That's going to be a backstop that prevents me from scanning too far to 

the left. 

So, I guess, I can remove this bit of code right here. 

So, what were the three steps? 

I had to pop elements off the stack. 

So, as long as the element at the top of the stack, 

that's S.top, I think, is the element at the top of the stack. 

As long as the height of that element is at least as tall as me, 

as H(i), then I'm going to pop something off the stack.

Play video starting at :35:39 and follow transcript35:39

So, this is going to be a loop that disqualifies everybody that I'm scanning 

past. They're too tall, so they're never going to be in consideration ever again. 

And then, I think I set my left of i value to the value that's now sitting on the top 

of the stack. 

So that's just S.top. 

And then finally I push. I do S.push(i). 

So I just add i to the list of contenders.

Play video starting at :36:2 and follow transcript36:02

So, those are the three steps that I'm doing on my stack. 

So actually, in code, that wasn't too crazy. 

I guess I actually should now do the same thing for computing the R(i)'s. 

To do that, I guess I would have to scan the other direction, 

so instead of scanning from left to right, I'm essentially doing the same algorithm 

but scanning from right to left. 

So, I'm going to start at N minus 2 and 

scan downwards until I reach i equals 1, decrementing i at each step. 

And then, inside that loop, I'm essentially going to do the same thing. 

Because I'm still using the same stack, 

I disqualify everyone at the top of the stack who's taller than me.

Play video starting at :36:41 and follow transcript36:41

I'm going to set, I guess, R(i) now is going to be the one sitting at the top 

of the stack. 

And then I push i. 

So, actually almost the same algorithm works for computing the R(i)'s. 

I guess I should probably clear the stack between these two calculations. 

So, as long as there's something in the stack, 

as long as the stack isn't empty, I will keep popping things out of it. 

So that will just clear out the contents of the stack. 

And then I probably need to, just as I had pushed 0 here as a backstop, 

I'll probably have to push the rightmost dummy element, 

N-1, into the stack as a starting point.

Play video starting at :37:19 and follow transcript37:19

That's my zero height element on the far right of the stack. 

This is my new approach based on a stack. 

Let's see if this actually compiles and runs. 

So I'll go in and g++ hist.cpp. Aha! Our first compiler error! 

I knew we'd been too lucky so 

far. It looks like we have failed to include the header file for stack.

Play video starting at :37:43 and follow transcript37:43

So, if I go back in my code here, I'm now using a stack, so I have to include stack. 

Aright. I would argue that's not really a bug, 

so we'll just kind of pretend that didn't happen. 

I'll clear the screen, and nobody's the wiser. 

Okay, so now if I run this program on one of my input files, then this is nice. 

We actually do seem to get agreement with all three versions of our code. 

And again, you'll notice that if I run it on the size 1000 input, 

the N cubed algorithm is struggling a bit.

Play video starting at :38:19 and follow transcript38:19

So, I've also created a size 1 million input. 

So, if I run all three of these on my size 1 million input, then, this is nice. 

The algorithm that we just wrote that gave me back an answer in a split second. 

The N squared algorithm, solve2, seems to be taking its time, and 

I don't even want to think about the N cubed algorithm. 

But, so what's the solve2 algorithm, the one taking quadratic time, 

what are we expecting to happen there? 

We've taken our input and we've increased it from size 1000 to size 1 million. 

We've actually upscaled the input size N by 1000.

Play video starting at :38:57 and follow transcript38:57

What happens to an N squared algorithm when you upscale N by 1000? 

N squared actually increases by 1000 squared, or a million. 

So actually the N squared algorithm that we're waiting on right now, 

we would expect that to take 1 million times longer essentially than it ran 

before with the input of size 1000. 

So, I'm probably safe in breaking that calculation. 

Let's go in and look at the the running time of the code that we just wrote. 

It seems to be running quite fast. 

So I would actually claim that the running time, 

we've actually improved it from quadratic down to, I claim, linear.

Play video starting at :39:33 and follow transcript39:33

So let's see if we can convince ourselves of that. 

The loop at the end here is still clearly linear, 

because we're looping over N possible rectangles and 

just doing a constant amount of work for every iteration of that loop. 

The two loops that worry us are calculating the L(i)'s and the R(i)'s. 

And, they're basically doing the same thing, 

so if I analyze one of them, I've basically analyzed both of them. 

So I'd like to show that this loop right here, in total, takes just order of N time [O(N)]. 

And, the thing that worries me in that calculation is this inner while loop here. 

Because, yes, the outer loop is looping over N things 

but might it be possible for 

that inner loop to also be looping over multiple things for 

each iteration of the outer loop? In which case, this would not be linear.

Play video starting at :40:19 and follow transcript40:19

However, I think we're in okay shape, because this inner while loop, 

every time it executes, it pops something out of the stack. 

And, if I now think about things on maybe like a per element basis, 

which we have advocated doing during this module, every element gets pushed 

into the stack exactly once and gets popped out of the stack at most once. 

Once an element is popped out of the stack, 

it never again goes back into the stack. 

And so, in total, over all possible iterations of this while loop, 

this is going to only contribute at most O(N) total time 

because every element is, at worst, going to get popped out of the stack once. 

So, we're actually okay. 

This outer for loop contributes a total of O(N) time. 

The while loop contributes a total of O(N) over all the iterations of that outer for loop.

Play video starting at :41:9 and follow transcript41:09

And, we're done. 

I guess computing the R(i)'s is the same argument, basically. 

So, this does indeed run in just linear time. 

So, we have a nice fast algorithm here. 

So, it's pretty cool how we can actually take even the fundamental ideas we've 

talked about in this module and put these ideas together in, arguably, 

a somewhat sophisticated way, and solve a problem here much, much faster. 

So, before I end, I wanted to add maybe one other interesting observation of how 

we can take this solution and 

even build on top of it to solve an even more interesting problem, perhaps. 

So, if I look at the following problem, this is another one that I 

think I've seen it first as a competitive programming problem somewhere.

Play video starting at :41:56 and follow transcript41:56

But, it's somewhat of a standard problem. 

The problem is, given a binary matrix, find the largest rectangle I can 

fit in the binary matrix that only covers 0s. It doesn't cover any 1s. 

So, maybe I have a plot of land that I'm trying to build the biggest possible house 

on, but I can't build a house that covers any trees in the plot of land. 

So this problem may look somewhat similar, because you're still trying to find 

a maximum area rectangle, but it also may look kind of complicated 

because now it seems like all four sides of the rectangle are in play. 

So how on earth are we going to solve this problem efficiently? 

And I won't code up a solution to this problem.

Play video starting at :42:35 and follow transcript42:35

I just want to point out that we can now actually solve this problem easily by 

running multiple invocations of the preceding algorithm. 

So given what we have just accomplished, we can now build on top of that to easily 

solve this even more sophisticated problem. 

So, let me just draw a picture of that. 

I've drawn a picture of the matrix only showing the 1s. 

I haven't drawn the 0s, just for simplicity. 

Imagine, for a second, that we commit to this red line being the bottom 

of the candidate rectangles that we're considering. 

I'm only considering rectangles that have a base on this red line.

Play video starting at :43:12 and follow transcript43:12

In that case, I would argue that our problem boils back down to 

exactly the largest area rectangle in a histogram problem. 

Because, from this red line I can extend a histogram bar upwards until I hit a one, 

and then all I want to do is find the largest rectangle that I can fit 

into that histogram. 

That's the biggest possible rectangle that has a base on this red line. 

And so, all I'm going to do is run that calculation, 

that linear time calculation from our preceding algorithm N times, one for 

each possible setting of this red line that defines the bottom of our rectangle. 

So, every step, I'm going to take the red line and move it down one notch. 

What happens when you move it down one notch? 

What happens to our histogram?

Play video starting at :43:56 and follow transcript43:56

Well, every bar in the histogram just gets one unit taller. I guess, 

except if you cross over a 1. 

That basically sets the height of a bar in the histogram back down to 0. 

So it's very easy. 

If you move the red line down by one step, 

you can update the histogram in just linear time. 

And then, also in linear time, you can find the biggest area rectangle in that 

histogram. And then just do that 

as you're scanning downwards that red line, 

you know, you're just N steps times O(N) time.

Play video starting at :44:24 and follow transcript44:24

And the total running time is going to end up being quadratic. 

So, I think this is just a nice illustration of how 

we can take one algorithm and then build something else on top of that and 

kind of continue to develop even more sophisticated solutions, 

but we try and simplify our thought process along the way by kind of only 

thinking at one level of abstraction as we go. 

So, I'll leave this with you. 

Hopefully, we'll have some more fun implementation as the course continues in 

future modules. 

[MUSIC]![[Screenshots/Screenshot 2025-08-27 at 1.36.56 pm.png]]![[Screenshots/Screenshot 2025-08-27 at 1.37.42 pm.png]]![[Screenshots/Screenshot 2025-08-27 at 1.39.11 pm.png]]
All Written in C++
![[Screenshots/Screenshot 2025-08-27 at 1.41.06 pm.png]]![[Screenshots/Screenshot 2025-08-27 at 1.42.32 pm.png]]![[Screenshots/Screenshot 2025-08-27 at 1.42.40 pm.png]]![[2InWpReDTQuByV6ocOXNng_11482f1f98ad46978de82b40867974f1_Coding-Discussion.pdf]]