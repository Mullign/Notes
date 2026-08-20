[Music] ![[Assignment 2 Overview.pdf]]

Dean: If you're watching this video, 

that hopefully means you have successfully 

survived programming Assignment number 1, 

and that you're eager to get going on 

the second programming assignment in this class. 

This video describes the details of that assignment. 

It's based on what I think is 

a very fun problem from 

a very interesting area of application, 

that being the overlap between 

algorithms and game theory. 

Algorithmic game theory is actually 

a surprisingly hot area of study at the moment. 

We'll spend an enrichment lecture 

on it later on in the course when 

we talk about so called stable 

matching or stable marriage problems. 

But there are lots of problems that 

fit into this framework well that are best 

described using game theoretic terminology 

and a game theory mindset. 

This would be problems like maybe auctions 

or matchings and assignments, 

or even automobile transportation network optimization.

Play video starting at ::57 and follow transcript0:57

Lots of exciting stuff in this area. 

Any problem in general that 

involves trying to optimize something, 

where instead of thinking about having 

one unique global optimum solution, 

you look at things from the vantage point 

of the N participants in your system, 

and try and figure out what's 

the best way to optimize for their benefit? 

Because they're all optimizing according to 

their unique individual objective functions, 

and those objective functions 

may not quite agree with each other. 

The problem we're going to study here is 

a very fundamental problem called Fair Division. 

How do you take some resource 

and allocate it fairly among 

N players who may have 

different ideas about what parts of 

the resource they value the most? 

We're going to look at a very simplistic example of 

this problem where the resource is 

the one dimensional number line, 

and we would like to allocate that number line, 

say between 0 and 1, 

between a number of participants. 

Each participant is going to 

have a value density function, 

if you will, that describes how that 

participant values different parts of this unit interval.

Play video starting at :2:1 and follow transcript2:01

Here, the blue Player 0 

really likes the early part of the interval, 

has a high amount of value 

assigned to the early part of the interval. 

Player 2 likes the latter part of the interval, 

and Player 1, 

the red player, really 

likes the latter parts of the interval. 

Player 1 would rather be assigned parts of 

the interval that are later on and Player 0, 

the blue player, would rather be 

assigned early parts of the interval. 

If you look at these value functions, 

they integrate to 1. 

There's one total unit of value for every player, 

it's just spread out differently 

across the interval for every single player. 

Our goal is to subdivide the interval in a way that 

makes every player feel like they're 

getting their fair share, which in this case, 

would mean every player should be 

getting according to their own value function, 

at least 1/3 of the interval. 

You can see that in this case, 

that is indeed what's happening.

Play video starting at :2:55 and follow transcript2:55

If you give this first segment to the blue player, 

they're getting what they consider to be 56.6% of 

their total value if you 

integrate their value function over that range. 

That's a lot of value from the perspective of Player 0. 

But the other two players are also getting 

at least 1/3 of the value that they 

could have hoped to get 

according to their own valuation functions. 

This homework problem, I like to joke, 

it really is a piece of cake, 

because the recreational mathematical version 

of Fair Division is 

sometimes called the cake-cutting problem. 

You may have actually seen this problem. 

How do you fairly cut up a cake amongst N participants, 

so each participant feels like they're 

getting their own fair share of the cake? 

To make it interesting, of course, 

every participant should have 

a non uniform valuation function 

over different parts of the cake.

Play video starting at :3:44 and follow transcript3:44

I like the strawberries, you like the frosting, 

someone else likes the 

middle part of the cake, for example, 

and that makes it a little bit less 

trivial on how you should slice up the cake so that 

everyone feels like they're getting at least 1/N worth of 

their value in the cake handed to them 

as part of the Fair Division algorithm. 

Sometimes you actually look 

at just the special case of dividing between two people. 

This leads to a simple heuristic 

you may have heard called, 

“I cut, you choose”. 

Player 1 basically makes a cut, 

and then Player 2 chooses 

which side of the cut they want to choose. 

That incentivizes the first player 

to cut the cake in a way 

that basically evenly divides 

the cake from that person's perspective, 

so that they would be happy with either side because they 

don't know which side the second 

player is going to choose. 

That's actually one way to ensure 

a Fair Division between two people, 

so each one gets what they 

perceive to be at least half the value. 

Another way you can do that is you can have 

one player slowly move the knife across the cake, 

and the second player will say stop at some point, 

presumably when you have 

moved the knife enough so that now you 

have carved out a piece that is worth 

at least half of the value to that second player.

Play video starting at :4:56 and follow transcript4:56

There are a couple of ways that you can do 

this Fair Division algorithm with only two players. 

Our goal here is going to be to generalize 

this to N players. 

One of my favorite lectures I've given in class, 

we actually talked about this problem 

once and I actually baked a cake. 

On top of the cake, I put all weird toppings. 

I had, sprinkles, 

and cheddar goldfish, 

and gummy worms and all sort of weird toppings, 

just to implement this algorithm for Fair Division, 

and it was a lot of fun. 

How do we generalize 

this fair division algorithm to N people? 

Well, let's think about maybe how we can 

generalize the idea of moving 

the knife slowly until someone says stop.

Play video starting at :5:38 and follow transcript5:38

What we're going to do is imagine that we have 

these value density functions 

provided to us for all the players. 

That's going to be our interface with the grading system 

is we'll be able to probe these value density functions. 

We will be able to say a cutoff like 1/N, 

and the grading system will return to 

us exactly the cutoff points in each of 

the value density functions that 

represents 1/N worth of value to each player. 

If I ask for the 1/3 point 

in every value density function, 

then I'll send 1/3 to the grader, 

and I'll get back a vector of these cutoff points. 

For Player 0, the blue player, 

his or her 1/3 point will be, 

it looks like about at 0.25. 

The green player would be about 0.48 maybe, 

and the red player would be about 0.55 perhaps. 

What those cutoff points represent are the points at 

which that player has exactly 

1/3 of their value on the left.

Play video starting at :6:35 and follow transcript6:35

The blue player has exactly 1/3 of 

their value to the left of this 0.25 cutoff, 

and 2/3 of their value in the remaining part of the cake. 

What we basically want to do 

is take the one 1/N cutoff points, 

where N is the number of players for all the players, 

and we take the smallest one, 

the most conservative one. 

The person whose value is the most 

concentrated on the left hand side of the cake, 

that's the blue player, Player 0 here, 

and we assign that piece. 

We basically take the minimum of 

these cutoff points for the 1/N cutoff points. 

We assign that piece to 

the player that has that minimum cutoff point. 

That piece leaves the picture, 

and now you subdivide the rest of the cake the same way. 

Over the remaining interval, 

you take the one 1/(N-1) cutoff points.

Play video starting at :7:21 and follow transcript7:21

For the remaining (N-1) players, 

you take the minimum one and assign that piece. 

That's basically what you would get if you were 

slowly moving the knife across the cake, 

waiting for someone to say “stop”. 

Because you have finally put the knife at a place that 

represents 1/N of the value of the cake to them. 

They'd be happy with that piece. 

In this case, the blue player is happy 

with the piece that the blue player gets. 

What about the other players? 

Well, the other players, 

if you look to the right of the line for the blue player, 

the other players still have 

1-(1/N) of their value in play.

Play video starting at :7:54 and follow transcript7:54

They haven't even reached their 1/N value cutoff points. 

If you look at the cake that's left over, 

every other player still has 1-(1/N) 

worth of their value remaining, which is N-(1/N). 

If you divide that amongst 

the (N-1) players fairly, by induction, 

each one of them is going to get 

a 1/N share of the entire cake at least. 

This algorithm will give you a fair division. 

The only downside is it's not particularly fast. 

Because to assign one piece of cake, 

you'd have to actually do a linear amount of work. 

You have to look at N cutoff points, 

one for every player, and pick the minimum.

Play video starting at :8:31 and follow transcript8:31

This would actually be order N time to just 

assign one piece of cake or 

quadratic time over the entire algorithm. 

Unfortunately, in our case, 

N is going to be quite a bit 

bigger than N^2 will be able to deal with, 

I think a quarter million or something. 

So we need a faster algorithm. 

It's no surprise that 

that fast algorithm is going 

to be using Divide and Conquer, 

because this problem appears 

in the module on Divide and Conquer. 

There is actually a very clever way that we 

can almost run that same algorithm. 

But using Divide and Conquer, 

we can make a substantial amount of 

faster progress and get 

a running time of just N log N as a result. 

Imagine for a second that the number of players is even.

Play video starting at :9:13 and follow transcript9:13

What I'm going to do is, if N is even, 

I'm going to ask every player for their 1/2 cutoff point. 

These are these dotted lines. 

Here I have 10 players in this diagram. 

I ask every player for their 1/2 cutoff point. 

That's the point that for that player 

would have exactly half of 

their value on the left and exactly half 

of their value on the right. 

I take all of those 1/2 cutoff points, 

and I take the median of those. 

Actually, since N is even, 

there are actually two entries in 

the middle that could rightly be called the median.

Play video starting at :9:44 and follow transcript9:44

Those are those bold dotted lines 

that I've pictured here. 

Those are going to be my dividing points. 

I'm going to take 

those two middle cutoff lines 

and use those to divide my problem in half. 

I have a first half that consists 

of the first half of the cutoff points, 

and the second half that's all the players who have 

cutoff points in that second half of the cutoff points. 

I have half the players in the first half, 

half the players in the second half. 

More importantly, the half 

of the players in the first half, 

they haven't even gotten to 

their halfway cutoff points yet. 

To them, at least half of the cake's worth of value is 

in that first half that they're 

now vying for contention over.

Play video starting at :10:26 and follow transcript10:26

In the second half, I have N/2 players, 

and from their perspective, 

at least half of the total cake's value 

is still available in that second half, 

because their halfway points are inside that range. 

More than half of the value to them is 

locally within that second half of the cake. 

I'm on track to being able to give 

everybody 1/N of the total value. 

I've assigned N/2 people 

to a segment of the cake that they 

collectively value it at more than half of 

their total value and on the other side as well. 

I just keep proceeding to sub-divide in this fashion. 

Because I can find the median values here in 

just linear time with 

Quickselect or linear expected time 

with randomized Quickselect. 

Then if I plug that into a Divide and Conquer framework, 

I have two sub problems of size N/2, 

plus a linear amount of time 

to find the place to sub-divide.

Play video starting at :11:18 and follow transcript11:18

That's going to be essentially the 

same recurrence as Merge Sort, 

and it's going to solve to 

N log N. That's my running time. 

This algorithm, there's a couple of interesting notes. 

One is that because we're 

actually use these two median values to 

define the end and 

the start of the cutoffs between the sub problems, 

we actually left a little bit of value on 

the table between those two cutoffs. 

You can actually make this algorithm work, 

even if you don't assign 

this little sliver between those two medians. 

You can actually just leave that out, 

and everyone will still end up 

getting at least 1/N of their total value. 

Of course, if you want more value 

to make everyone even happier, 

you could have just used one of 

these two medians and use that as the single cutoff, 

and not just left out any little sliver in the middle.

Play video starting at :12:1 and follow transcript12:01

Either way will work. I guess 

the participants will thank you if you only 

use one cutoff and you don't have 

that little sliver available in the middle. 

This approach though only works if N is even. 

If N is odd, 

then you have to be very careful because one 

of these sub problems would end up with N/2 rounded up, 

and only half the value in that case, 

which isn't quite enough value to be able to 

split fairly among N/2 rounded up players. 

We have to be a little bit careful about how we 

treat the N even versus N odd cases. 

One way we could do that is if N is odd, 

we can run one iteration of the preceding algorithm, 

the one that assigned one piece, 

based on the person who had the minimum value 

of the 1/N cutoff point. 

We could assign just one piece 

and then we're back to the even case, 

and then that case makes a lot more progress 

because it can divide in half.

Play video starting at :12:52 and follow transcript12:52

That would be one alternative. 

We could also just use the central division algorithm, 

but just being a little bit more careful. 

We can't use 1/2 as the dividing point, 

because if N is odd, 

we know that we're going to be dividing into “N/2 

rounded down” and “N/2 rounded up” players. 

We have to actually use a cutoff point 

that takes that into account basically. 

It's not (N/2)/N, which would be 1/2, 

but it's N/2 rounded down divided 

by N. It's just slightly less than 1/2. 

That's the region that you assign 

these rounded down N/2 players to.

Play video starting at :13:32 and follow transcript13:32

You can also make this work. 

You just have to make sure that the number of players you 

assigned to that region is commensurate with 

the cutoff value that you used to define that region, 

so that you're on track 

to being able to divide everything up, 

so that everyone at the end of the day 

will finally reach a value of 1/N. 

We can make this work in 

the odd case in several different ways. 

You should feel welcome to do it this way where you, 

in the odd case, peel one slice off, 

and that reduces it back down to the even case, 

or you can just make both cases into 

one case and just be 

careful with how you choose the cutoff point. 

Just don't use 1/2 in odd case, 

but use N/2 rounded down divided by N, 

which will be ever so slightly less than 1/2. 

The left side will be what you assign 

the “N/2 rounded down players” to, 

and the right side will be what you 

assign “N/2 rounded up worth of players” to. 

That's the Divide and Conquer algorithm 

that we're hoping to be able to implement.

Play video starting at :14:31 and follow transcript14:31

Actually, it's interesting that we've talked about 

this original algorithm that peels off 

one slice as a special case. 

But that really is the same algorithm 

as the Divide and Conquer algorithm. 

It's just, we're 

choosing a very different dividing point. 

Instead of 1/2, we're choosing 1/N, 

and assigning one player on 

one side and (N-1) players on the other side. 

The case of one slice that we talked about initially, 

that actually is the same algorithm 

that we used in the 1/2 cutoff case. 

Instead of the 1/2 cutoff, 

we used the 1/N cutoff instead. Pretty cool algorithm.

Play video starting at :15:9 and follow transcript15:09

Our goal with the problem is going to be implementing 

that algorithm so that we 

can run on instances of size up to N, 

at most a quarter million. That’s big enough 

that N^2 will time out. 

It will not be effective to 

just peel off one slice at a time. 

We really do need to run 

the Divide and Conquer algorithm. 

Just like with the previous assignment, 

you'll be given a small template file 

that you'll be able to modify and turn in. 

You should just turn in that one file, 

and that one file will 

have a program called “Compare” in it. 

You won't actually be able 

to access these cutoff points directly, 

but you'll be able to compare cutoff points.

Play video starting at :15:49 and follow transcript15:49

If you're interested in these cutoff points 

at a value of 1/3, 

then what you can do is say, well, 

I would like to compare Player 2 with Player 0 

at this 1/3 cutoff point. 

That's going to go in and say, 

the grader will evaluate 

those value densities at the cutoff point of 1/3. 

It'll say, two, 

that was at about 0.48, 

and zero, that was about at 0.25. 

I'm going to get the value plus one 

because two was greater than zero. 

This cutoff point for Player 2 

was to the right of the cutoff point for Player 0. 

You'll basically be given a 

comparison function that tells you if 

one cutoff point is less or 

greater than another cutoff point. 

But you'll never actually get the actual 

exact values of the cutoff points, 

only the ability to compare them, 

which is fine because all the algorithms that 

we're going to be using here are comparison-based.

Play video starting at :16:40 and follow transcript16:40

They should just make use of comparisons. 

What we print out at the end of the day is going to be 

an allocation of this unit interval 

into segments that we assign to each player. 

We're going to just list out 

the players in the order 

that their segments are assigned. 

Here 0, 2, and 1 because 

the first segment is assigned to Player 0. 

The next assignment goes to Player 2, 

and then the final assignment goes to Player 1. 

That would be the optimal order for 

this particular instance that 

would make the players the happiest. 

How happy does it make those players?

Play video starting at :17:12 and follow transcript17:12

The grader is actually going to take your output, 

this list 0, 2, 1, 

and it's going to figure out how 

much it could have allocated in 

the best possible circumstances to 

those players with that particular ordering. 

It's going to say, well, could I have actually allocated 

a 1/N fraction of value to 

all those players? If so, great. 

It'll even see if I can allocate more than 1/N, 

which in many cases you will be able to do. 

But you definitely should be able to allocate 

at least a 1/N fraction of the value to each player. 

The grader will determine, for this ordering, 

what's the best possible amount 

of value that I could have uniformly allocated 

to each of the players in that order of assignment? 

Your score will be based on that amount of value.

Play video starting at :17:56 and follow transcript17:56

If they each get at least 1/N, then that's good. 

That's what your target is. 

If they don't get 1/N, 

then you would only get partial 

credit for this assignment. 

I think I've gone over the information here. 

The grader will basically give 

you partial credit based on how much of 

an allocation everybody gets when 

assigned in the order that you specify. 

Now, to implement your algorithm. 

It should be a nice example of Divide and Conquer.

Play video starting at :18:23 and follow transcript18:23

It's actually a Divide and 

Conquer within a Divide and Conquer. 

This really is testing your Divide and Conquer skills. 

What we're first going to have to do 

is find the division point. 

Remember, that was a median finding application 

among those cutoff points. 

That's going to require implementing Quickselect. 

Step 1 is implement 

the Quickselect algorithm to find 

the median of the cutoff points at 1/2, 

or 1/N or whatever. 

I guess, 1/2 in the case that N 

was even. That's the first step.

Play video starting at :18:53 and follow transcript18:53

Then using that cutoff point, 

you can implement the overall Divide 

and Conquer algorithm that apportions 

the unit interval into 

segments for each of the participants. 

What you might want to do actually 

for ease of implementation, 

is you may want to actually forego 

the Quickselect part, at least initially, 

because one easy quick and dirty way to find 

the median is to just sort the cutoff points. 

You could use a built-in sort function in 

your language to sort 

the cutoff points and find the median. 

That will let you implement 

the overall Fair Division algorithm much more easily, 

and then you can swap out the median finding part 

by implementing Quickselect. 

That shouldn't really change your answer. 

It should just make it run a lot faster 

and use a lot less comparison. 

The interesting thing here about the grader is that 

it's going to keep an eye on 

the comparisons that you're making, 

because you're talking to the grader, 

asking it to make a variety of comparisons.

Play video starting at :19:46 and follow transcript19:46

The grader is actually going to figure out if 

the comparisons that you are making are 

indicative of implementing Quickselect. 

If you actually don't use 

quick select to find the median, 

but use something like sorting instead, 

then the grader will know, 

because the greater will look at the pattern of 

comparisons you're making and it'll say, 

it looks like you're actually sorting 

instead of running Quickselect, 

and so it will actually give you a penalty in that case, 

because the goal here is to actually practice 

our Divide and Conquer skills and actually get 

an N log N algorithm which requires implementing 

Quickselect and not just running 

an internal sort function in our library. 

If we implemented this algorithm 

with just sorting instead of Quickselect, 

here's what you might want to try first. 

Instead of Quickselect, we 

just use sorting to find the median. 

That's actually going to give you 

a slightly slower running time also, 

because every single time we pick the median, 

that involved a sort which took N log N time presumably. 

We get the recurrence of 2T(N/2)+(N log N). 

That solves to N log^2 N 

instead of N log N. If you do this, 

you'll get a slightly slower running time, 

and the grader will penalize you because 

it thinks that you're sorting and 

not running Quickselect.

Play video starting at :20:59 and follow transcript20:59

That is the structure of 

the program that we're going to be writing. 

You're also going to be given 

a facility for testing locally, 

just like with the first assignment. 

There will be a compare local function 

that you can call if you'd like to 

test locally and not call 

the compare function on the actual grader. 

The compare local function is simply 

going to give you an instance that looks like this. 

Everyone is going to have a 

triangular value density function 

with the peaks spaced out like this in reversed order. 

The optimal solution you should hopefully arrive at is 

to order the individuals 

in decreasing order of their indices. 

Player (N-1), then player (N-2), 

all the way down to Player 0, 

should end up being the optimal solution 

with this particular set of density functions, 

which is what the compare local function 

is going to simulate, 

basically, if you call it.

Play video starting at :21:51 and follow transcript21:51

You know what the right answer is 

that you should expect in that situation. 

Hopefully, this is just a piece of cake to implement. 

I wish you the best of luck with 

your Divide and Conquer implementations, 

and hopefully, you'll be able to 

divide the unit interval 

[Music]