We often deploy randomization as something of a line of 

defense against worst case performance in algorithms. 

This is something that we saw in the last lecture— 

the final example of the last lecture where we 

built a histogram in an online fashion, 

one element at a time. 

And here, the worst case performance could be 

quadratic because every single element you process 

could end up being an expensive element 

that causes an expensive update to the entire histogram. 

But, we saw that if you add the elements in random order, 

then you don't get too many of those expensive updates, 

and therefore, the entire running time 

drops down to just linear in expectation. 

This is a pretty common phenomenon. 

It motivates a general algorithm design technique called 

randomized incremental construction that we will see 

many times throughout 

this module and throughout the course. 

The idea is we're doing incremental construction— 

We're building a solution by adding elements of 

our input, one by one, and keeping 

a solution up to date as we do that, 

but we're adding the elements, now, in random order in 

hopes that that mitigates 

the possibility of worst case performance.

Play video starting at :1:14 and follow transcript1:14

Sometimes that helps and sometimes it doesn't. 

One example of where it maybe doesn't help is if you go 

back to insertion sort from the previous module. 

If you run insertion sort, 

which is a prominent incremental 

construction sorting algorithm— 

If you run that on elements chosen in random order, 

you still get expected 

quadratic running time as a result. 

In some cases, randomized incremental construction 

doesn't necessarily help the bottom line, 

but in many cases, it does. 

In maybe two modules, 

we'll actually use randomized incremental construction as 

the basis for how we keep binary search trees balance. 

We're going to see it quite a bit over this course. 

Another vantage point from which you might see 

the same ideas is— maybe 

not necessarily developing a randomized algorithm, 

but thinking about average case analysis of 

a non random algorithm, where you're 

simply feeding it some sort of random input.

Play video starting at :2:6 and follow transcript2:06

A lot of the same underlying tools can be used 

to analyze both types of scenarios. 

For the rest of our discussion here, 

I thought it might be fun to focus on a few examples of 

randomized incremental construction, drawn 

from the world of computational geometry. 

—A fascinating area of algorithmic study. 

One that I really wish we had the room in this class 

to devote an entire module too, 

but sadly, we don't have the space for that. 

So, instead, I've tried to sprinkle 

some geometric ideas throughout 

the remaining modules so at least you can 

get a sense of some of the fundamental problems and 

some of the fundamental solution techniques in this area. 

One hallmark of computational geometry is that 

randomized incremental construction seems to be 

extremely prevalent as a viable solution technique. 

I can think of maybe a dozen problems, 

very fundamental problems in geometry, where 

randomized incremental construction gives you 

a very simple and very effective 

efficient solution approach. 

So, on this slide, I've highlighted 

just a smattering of 

common problems in computational geometry.

Play video starting at :3:10 and follow transcript3:10

I thought I'd maybe pick two of these and, in one case, 

go over things at a very high level and, 

in the other case, go over things in 

a little bit more detail and just give you a sense of 

how we go about designing and 

analyzing randomized incremental construction algorithms. 

The first problem I wanted to highlight 

was the so called convex hull problem. 

It's a very prominent problem in 

the space of computational geometry. 

In some sense, it's almost 

like a geometric analog of sorting. 

There's almost as many ways to compute 

convex hulls as there are ways to sort. 

But, if we want to think about how we might design 

a randomized incremental construction algorithm 

for convex hulls, 

then what would that entail? 

So, the convex hull problem is very simple.

Play video starting at :3:53 and follow transcript3:53

It's just: given end point, 

find the smallest polygon you can wrap 

around those points or, in higher dimensions, 

the smallest polyhedron that you 

could wrap around those points. 

If you want to solve that problem 

with randomized incremental construction, 

you would basically take all the points in your input, 

add them, one by one, into the instance and 

keep an up to date hull 

of the points you've added so far. 

Most of the points you add are 

going to be relatively inexpensive if they 

land inside the current hull because you 

don't have to change the current hull if that happens. 

The expensive case is if you drop a point in and it lives 

outside the current hole because then you 

have to update the structure of the hull. 

So, the hope is that 

those expensive cases don't happen too often, 

and that's where the randomization comes in. 

Because, if you add the points in random order, 

you can imagine that, as the hull gets bigger and bigger, 

it gets less and less likely 

over time that every new point that 

you add is going to live outside 

the hull and cause an expensive update. 

So, that's just the high level gist of 

how randomized incremental construction can 

lead you to an effective algorithm for convex hulls.

Play video starting at :4:59 and follow transcript4:59

If you implement this the right 

way and analyze it the right way, 

you end up with an order N log N expected running time 

both in two and three dimensions for convex hulls. 

Things get a little dicier in higher dimensions, 

which we'll talk about later on. 

The problem I wanted to talk about 

in a bit more detail is 

another fundamental problem in 

computational geometry called 

the smallest enclosing circle problem. 

It is what the name suggests. 

Basically, you're given n points and you'd like to find 

the smallest circle that contains those n points. 

Maybe, as a practical application, 

you're trying to find an optimal place to locate 

a facility that serves n customers or 

the optimal place to locate a transmitter that can 

broadcast to n people with minimum power. 

I chose this problem to talk about 

because it is very elegantly 

solved with a really cool and really 

beautiful randomized incremental construction approach 

that leads to a fairly epic improvement in running time.

Play video starting at :5:56 and follow transcript5:56

It's the perfect problem to 

illustrate the power 

of randomized incremental construction. 

Maybe as a starting point, 

let's look at the non-randomized approach that 

we might first come up with 

for solving a problem like this. 

If you think about looping 

over all of the candidate circles that 

you want to check and find the best one as 

part of a brute force approach to solving the problem, 

then the key observation here is that 

the optimal circle is determined by three points. 

Three points determine a circle. 

If your optimal circle 

wasn't tightly constrained by three points, 

you could generally decrease its size until it catches on 

eventually three points or maybe two points 

at the opposite ends of a diameter as a special case. 

If you enumerate through every set of 

three points and fit 

a circle to every possible set of three points, 

then one of those choices will be the optimal circle. 

That will lead you to an order of n^4 algorithm 

because there's order n^3 

possible circles you'd have to check 

and, for each circle, you'd 

have to check that all the points are indeed 

contained within it and then 

take the one that has the smallest size.

Play video starting at :7:4 and follow transcript7:04

Our starting point is not exactly 

a fast algorithm—order of n^4. 

But, using randomized incremental construction, 

we will actually be able to improve this 

dramatically down to just linear in expectation— 

which is, I think, pretty cool. 

In fact, this algorithm even 

generalizes to higher dimensions. 

We can find the smallest enclosing sphere 

in three dimensions or four dimensions or even higher. 

It even works in one dimension, 

I guess, but it's boring. 

The corresponding problem there, 

I guess, would be the smallest enclosing interval, 

which you can easily solve just by finding 

the min and the max of your values. 

Although, there is a useful point to be made here.

Play video starting at :7:42 and follow transcript7:42

In general, if you're trying to 

solve a geometric problem, 

I would recommend trying to 

reduce the dimensions down to the point where 

the problem finally is easy 

enough for you to understand how to solve effectively. 

Maybe, here, reducing down to 

one dimension makes it a bit too boring, 

but don't start with a 10 dimensional problem. 

Start with a problem in one or two dimensions, 

get some insight in how to solve it and then start 

looking at higher dimensional 

versions of the same problem. 

So, let's talk about how this algorithm works. 

It works in a couple of simple steps— 

And actually, we're going to 

develop a very simple algorithm and 

then bootstrap on top of that another algorithm, 

and then we're going to add on top of 

that another layer of the algorithm. 

The very first of those layers 

is going to be an algorithm that actually assumes 

—somehow, by magic—that we are already given 

two of the three points 

that characterize an optimal circle. 

So, imagine for a second that a little birdie tells 

you what two of 

the three points on an optimal circle are, 

so you just need to find that third point.

Play video starting at :8:46 and follow transcript8:46

So, much easier than searching in general for 

the three points that characterize an optimal circle. 

In this case, it's very easy to find the optimal circle. 

All you need to do is just start with 

a circle that is 

defined by the two points that you're told, 

A and B. They're going to be opposite 

end points of a diameter. 

Then we just process 

the remaining points, one by 

one, in whatever order we want. 

It doesn't have to even be random, in this case. 

And, we simply think about adding 

those points into our instance one at a time.

Play video starting at :9:14 and follow transcript9:14

And, we're going to keep our current tentative circle up 

to date so that it continues 

to enclose all of the points so far. 

So, every time we add a point and it 

lives inside the current circle, 

we don't need to do anything. 

If we add a point and it 

lives outside of the current circle, 

then we need to expand the current circle. 

And now, if you think about what has to happen, 

it has to expand to go through that new point, 

and it also has to go through A and B, 

because we have been assured by our magic that 

the optimal circle does indeed go through A and B. 

That's going to be our algorithm. We just 

basically add the points in arbitrary order 

and keep expanding the circle as 

needed until we reach the final circle. 

Now, oftentimes when I 

talk about this algorithm in class, 

I get a very common question from 

students asking about, "Well, 

when you expand the circle, 

can something bad happen that kind of looks like this?"

Play video starting at :10:8 and follow transcript10:08

When you expand the circle, 

you are actually leaving behind 

a little bit of the area of the old circle. 

So, what if there were some points in that area there, 

like this red point here? 

Now that you've expanded the circle, 

it seems like that red point has been left behind and the 

resulting circle is not going to 

contain all n of your points. 

It turns out that this actually can't happen as long 

as whatever magic source you are 

relying on that tells you that 

A and B are on the optimal circle— 

if that magic source is correct, 

then this case can't happen. Because, if 

the circle has to flex out 

far enough to include this new point, 

then there's no way that A and B could 

have both been on an optimal circle to begin with. 

So, as long as your magic is right, 

then this actually can't happen, 

this sort of worrisome case right here. 

This is our first step— 

our first level of algorithm.

Play video starting at :11:4 and follow transcript11:04

Given some magic oracle 

that tells you two points on an optimal circle, 

we can find the third in linear total time. 

Now, what if we have a little bit less magic? 

What if we're only given via 

some magic oracle one point on an optimal circle, 

and now we have to find the 

other two points on that circle? 

We can do something similar, in that case. 

We're going to start with a fairly 

degenerate zero size circle 

that's basically that one point that we're given, and 

again, we're going to now sprinkle 

in all of the remaining points in our instance, one 

by one, and keep our circle up to date as we do that. 

And that follows the same procedure— 

Anytime you add a point inside the current circle, 

nothing interesting has to happen. 

If you add a point outside the current circle, 

the circle has to expand, 

and it has to expand to go through that new point because 

the new point is certainly going to be 

on the boundary of the new circle.

Play video starting at :12:2 and follow transcript12:02

You also know that point A, 

the one that you were told by magic, 

has to be on the optimal circle, 

that's also going to be on the boundary. 

So, how do you now expand the circle? 

All you know is two points on the optimal circle, 

the point A that you were told 

by magic and the new point. 

But, conveniently, we just built an algorithm that, 

given two points on the boundary 

of an optimal circle, finds the third. 

Every time our circle expands here, 

we're going to pause and 

run the algorithm that we developed 

as our first step to find the right circle in that case. 

So, we're bootstrapping this second algorithm 

on top of the first algorithm. 

Things now get a bit more 

interesting from a running time perspective, 

because when we expand the circle, 

it no longer just takes constant time to expand, 

like it did with our first algorithm.

Play video starting at :12:50 and follow transcript12:50

But rather, it gets more and more expensive, 

the more points we have added to our instance. 

Every time we expand the circle— 

Suppose you've added j points to your instance so far, 

so P_j is the point that causes the expansion. 

Then running the preceding algorithm, 

that takes linear time and the number of 

points in your instance so far, which is j. 

If you expand the circle when adding point P_j, 

that's going to take you order of j time— 

more and more expensive as time goes on. 

You might worry that if you have a lot 

of these expensive expansions, 

you could be heading more towards 

a quadratic running time. 

But this is where randomization is going to save 

us. Because we're adding points in random order, 

that will actually make it less and less 

likely over time that we actually cause expansions, 

and so that'll help dampen out 

the influence of this order of j term as we move forward.

Play video starting at :13:41 and follow transcript13:41

The total running time of 

this entire algorithm, as we add all n points, 

will end up being just linear in expectation still. 

And, we can see that with a pretty easy application 

of linearity of expectation. 

If we look at the way that's set up, 

I'd like to calculate the expected total running time 

of this entire algorithm, 

and I can break that up into 

a sum of simpler random variables, 

T_j. Each of which tells me 

the amount of running time I 

spend just adding the jth point. 

As we have discussed, 

there are two cases here. 

There's the expensive case where you add the jth point 

and that causes an expansion that takes order j time, 

and there's the inexpensive 

case where you add the jth point 

and that's inside your circle 

and it doesn't cause an expansion. 

So, what is going to be 

the expected value of one of these T_j random variables?

Play video starting at :14:30 and follow transcript14:30

Remember, the definition of expected value is 

just a sum over all the 

possible values that you can take 

—so, one of them is order j; 

the other one is order one— weighted 

by the probabilities of taking those values. 

So, order j weighted by the probability that 

we cause an expansion when adding the jth point. 

Then order one times the probability that 

we don't cause an expansion when we add the jth point— 

the probability that we have a point inside. 

I guess I can probably, very easily— 

I can just upper bound this probability by 

one because all probabilities are at most one. 

This part right here is going to 

contribute just a constant to our total. 

And, conveniently, this probability 

—the probability of causing an expansion— 

that actually gets smaller and smaller as j increases. 

We'll show in just a second 

that that's actually just 2/j.

Play video starting at :15:22 and follow transcript15:22

And, that's going to cancel out, effectively, 

the order j and make this part 

of the expression also just a constant, 

and the expected total amount of work we spend 

per point that we introduce to our instance is constant. 

That means, if we add those all 

up using linearity of expectation, 

the expected running time of the entire algorithm is 

going to add up to just order n at the end of the day. 

The only thing left to talk about is this probability. 

Why is it the case that when you add the jth point, 

there's a probability of 

2/j that your circle will expand? 

There's actually a really cool way to argue 

this, using sometimes what's called backwards analysis. 

You actually think about your algorithm running 

backwards instead of running forwards, 

and the probabilities get a little bit 

clearer to think about in that case. 

Imagine for a second that we take this algorithm 

that's adding points in random order 

and the circles expanding, 

and, instead, you can hit the rewind button 

and look at that process backwards.

Play video starting at :16:24 and follow transcript16:24

What would it look like if we unran our algorithm 

—if you run it in reverse, essentially? 

If you think about it in reverse, 

you start with a full circle 

that encloses all of your points 

and, now, instead of adding points in random order, 

you're deleting points in random order. 

And, the circle, instead of expanding, is actually 

contracting whenever it has the opportunity to do so. 

In fact, anytime you delete 

a point on the boundary of the circle, 

that will allow it to contract a little bit. 

That's the reverse process. 

The circle is contracting over time. 

The probabilities are actually the same though.

Play video starting at :17: and follow transcript17:00

At the jth step, 

when there are j points in play, 

the probability of an 

expansion when you're moving forward, 

that's the exact same thing as 

the probability of a contraction moving 

backwards when you delete 

a point when there are j points in play. 

It's the same event, you're just looking at 

it going forward versus going backwards. 

So, let's look at it from the reverse perspective, here. 

I have j points in play, 

and I'm deleting a random point from those j points. 

What's the probability of a contraction? 

The circle will only contract if I 

delete one of the points on its boundary. 

Remember, there's three points that 

characterize the boundary of my circle at this point.

Play video starting at :17:42 and follow transcript17:42

One of them is this point A that 

my magic oracle told me at 

the beginning must be on the optimal circle. 

That point has stayed with me the entire time. 

That point never leaves the boundary, 

so there's really only two possible other points on 

the boundary whose deletion 

could have caused a contraction. 

That's where I get 2/j as my probability. 

Now that we've built this algorithm, 

this algorithm uses a little bit 

less magic than the first algorithm. 

The first algorithm required 

a substantial amount of magic. 

Remember, we had to know two points 

on the boundary of our optimal circle.

Play video starting at :18:19 and follow transcript18:19

The second algorithm only needed to know 

one point on the boundary of our optimal circle, 

and it still ran in linear expected time. 

Our third step is basically removing all of the magic. 

Now, suppose you don't know 

any points on the boundary of your optimal circle— 

which you certainly don't in the real world. 

Now, what should we do? 

Well, we're going to do the same thing. 

We're going to bootstrap off of 

the second algorithm, in this case. 

We're going to start with a very lonely zero size circle 

just floating in the ether, 

and we're going to take all of our points and 

add them in random order into our instance.

Play video starting at :18:54 and follow transcript18:54

And, anytime we add a point that causes the circle— 

I guess, the first point is going to cause 

the circle to become a trivial circle 

centered on that first point and then adding 

more points is going to cause the circle to expand again, 

just like we've been doing in the past. 

Imagine now that you add a point 

and that causes the circle to expand. 

When you expand the circle, you know it has to 

go through that new point, but that's all you know. 

You don't know any other points on 

the boundary of that newly expanded circle. 

How do you figure out what that newly 

expanded circle should be? 

Well, you only know one point on the boundary, 

so you can just use the algorithm that we just developed 

that knows one point on the boundary. And, 

that runs in linear expected time.

Play video starting at :19:36 and follow transcript19:36

We're basically doing the exact same thing layer by 

layer here and using less magic in each layer. 

Here, every time we expand the circle, 

we're, again, going to be spending 

order j time— I guess, order j expected time 

because that's the running time of 

the preceding algorithm when 

run on an instance that has j points. 

If the jth point causes an expansion, 

this still ends up taking linear time at that point. 

Now, all we have to do is figure out 

the analysis of this algorithm—our 

final algorithm that doesn't require any magic. 

And, it turns out that this algorithm also 

runs in just a linear amount of expected time. 

If we go back to our analysis, 

very little actually changes. 

We can go back to our linearity 

of expectation based analysis here.

Play video starting at :20:27 and follow transcript20:27

The only thing that will actually 

change is the probability of an expansion. 

It turns out that everything 

else remains essentially the same. 

I guess, technically, the order j thing here— 

the order j term is in 

expectation as opposed to 

just being order j in the worst case. 

That might look a little bit weird 

that you have an expected value 

that, inside of its definition, contains expected values 

but it's mathematically actually okay to 

flatten out those expectations into just one expectation. 

The only thing that really changes 

here, appreciably, is this probability. 

Instead of it being 2/j, 

it's going to become 3/j. 

But, this will still end up 

giving us a constant for the running time and 

expectation on one point and 

a linear overall expected running time.

Play video starting at :21:19 and follow transcript21:19

Why is it 3/j? Well, if 

we go back to our backwards analysis, 

we basically just don't have this point A anymore. 

The probability of contracting the circle— 

Now, there are three points on 

the boundary that could cause 

that contraction instead of two. 

We get 3/j. That's the only real difference. 

We have built what 

I think is a pretty cool algorithm here. 

It is this succession of layers.

Play video starting at :21:45 and follow transcript21:45

Each one getting a little bit 

more sophisticated than the previous one, 

but each one is built on calling the previous layer. 

One of the really cool things about this algorithm 

is that it extends rather 

effortlessly into higher dimensions. 

For example, if you want to compute 

the smallest enclosing sphere of 

n points in three dimensions, 

you just add one more layer to the algorithm, 

and it still ends up running in 

just linear expected time; 

although, with a pretty substantial caveat. 

The dependence on dimension is really really bad. 

It's of the form dimension factorial, 

so the overall running time is basically order of 

n times the factorial of dimension. 

You can actually see that pretty easily in the analysis. 

Remember, our very first algorithm had a term of 

2/j for this probability. And then we had 3/j.

Play video starting at :22:35 and follow transcript22:35

The next layer would have 4/j. 

Because things are all composed together, 

those constants are going to end up 

multiplying together for the final running time. 

You're going to get a two times, a three times, 

a four... all the way up to the final dimension. 

So, that's where you get the dimension factorial from. 

So, this algorithm, while it works really 

well in two or three dimensions, 

it certainly would not be appropriate in 100 dimensions. 

This is actually somewhat of 

a general phenomenon in computational geometry. 

We sometimes call it the curse of dimensionality.

Play video starting at :23:6 and follow transcript23:06

It sounds like a bad horror movie film title. 

It refers to the phenomenon that, for many problems, 

there's this inherent scalability 

with dimension that's just very poor. 

So, for smallest enclosing ball, 

every algorithm that we know for solving that problem 

scales at a super polynomial rate with dimension. 

With say the convex hull 

problem that we talked about earlier, 

we can solve it in low dimensional spaces 

in n log n time in two or three dimensions. 

But, once you're up to four or five dimensions, 

you're already taking, as a lower bound, n squared time, 

and that's inherent in the problem. 

I guess, in four or five dimensions, 

it actually takes you n squared space 

to even describe a convex hull. 

You can't do better than n squared.

Play video starting at :23:48 and follow transcript23:48

Once you're up to six or seven dimensions, 

this becomes n cubed. 

Scalability is not great. 

This happens with a wide range of 

problems in computational geometry. 

It's quite a challenge for algorithm designers, 

and it also might concern us in certain fields, 

say like machine learning, 

where you typically deal with 

geometric problems and extremely high dimensional spaces. 

You might have points in feature spaces that 

are easily hundreds or thousands of dimensions. 

So, you have to be very cautious and 

careful when you're designing algorithms 

for these problems because you have to consider 

scalability in terms of dimensions very very carefully.![[c03g6HFuS9-9treY3jU_XQ_4b96a862bbf84d05815eef14471b75f1_Randomized-Incremental-Construction.pdf]]![[screenshots/Screenshot 2025-09-05 at 1.42.38 pm.png]]![[screenshots/Screenshot 2025-09-05 at 1.47.33 pm.png]]