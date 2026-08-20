![[Divide and Conquer Examples.pdf]]
[MUSIC] 

Brian: Let's have a look at some prominent examples of Divide and Conquer algorithms. 

This will not only help us understand better the types of problems to which 

we can successfully apply Divide and Conquer. 

But it will also help us get some extra practice with analyzing performance 

of Divide and Conquer algorithms in solving recurrences. 

So maybe a good starting point here is our old friend Merge Sort, 

the prototypical example of a Divide and Conquer algorithm. 

So to sort an array of size n, you do two recursive sorts of size n over 2, 

and then a linear time merge. 

Giving us what is perhaps the most common recurrence we will ever see, 

T(n) = 2T(n/2) + theta(n), solving to n log n. 

Many of the examples that we're about to look at will share this 

exact same recurrence and this exact same final running time.

Play video starting at ::55 and follow transcript0:55

Perhaps that's not surprising, 

because dividing in half is such a common thing to do with Divide and Conquer. 

Okay, first example. 

Suppose I have a sorted array and someone has come along and 

shifted that array over by k units. 

And whatever got shifted off one side kind of wrapped back around to the beginning of 

the array. 

And so now the array looks kind of like this picture right here. 

I have the k elements that used to be at the end of the array that are now at 

the beginning of the array. 

And I would like to figure out what k was by what amount someone shifted 

the array over.

Play video starting at :1:29 and follow transcript1:29

I, essentially, would like to find this, the index of this kind of precipitous 

drop, this point of discontinuity, that, basically, will tell me what k is. 

So this is actually a relatively straightforward problem. 

I can almost solve it with what I would call, essentially, 

a variation on binary search. 

If you look in the middle and 

compare the value of the array in the middle to the values at the endpoints, 

then on the right-hand side, you notice that in the middle, you have a high value. 

On the right-hand side, you have a low value. 

The only way for that to have happened is for the right-hand side to contain 

the precipitous drop, for there to have been a decrease on the right side. 

So you know that you need to recurse to the right, 

the answer is on the right-hand side.

Play video starting at :2:12 and follow transcript2:12

And in general, you can look at the first, the middle, and the last value, 

and figure out which direction you need to recurse. 

This, essentially, 

then gives you the performance characteristics of binary search. 

It's going to run in log n time because every iteration is going to be halving 

your problem size. 

If we write that as a recurrence, then to solve a problem of size n, 

we spend constant time deciding which of the two directions to recurse, 

and then we're left with a subproblem of size n over 2. 

So if we solve this recurrence using standard techniques, 

we will end up with log n as the running time of our algorithm. 

This reminds us that binary search is also an example of Divide and 

Conquer in action. 

Kind of a baby example, but 

it still probably fits into that class of techniques.

Play video starting at :2:59 and follow transcript2:59

Okay, this looks a little bit scary when you first see it, perhaps. 

I would like to calculate X raised to some ridiculously large power, 

and maybe X is even a matrix. 

So multiplication is expensive in that situation. 

So I really, really wouldn't want to just take X times X times X this many times, 

that certainly would not be a preferred solution in this case. 

So here, what we can do is something called repeated squaring. 

If you'd like to raise X to a very large power, you can square X repeatedly. 

So the first time, you get X squared, then you get X to the 4th, 

then X to the 8th, X to the 16th.

Play video starting at :3:37 and follow transcript3:37

You double the exponent every single time you square it. 

And so that leads us to a relatively simple Divide and Conquer based approach, 

where if you want to raise X to an even power, 

then all you have to do is raise X to the N over 2 power first. 

And then just square that with a single multiplication. 

And so that lets you make a lot of progress towards raising X to a very big 

power. 

If N is odd, if your exponent is odd, then you can reduce that back to the even 

case by just taking X times X to the N-1, which would be X to an even power. 

So kind of after two steps of applying this formula, you have, 

essentially, halved your exponent. 

So to compute X to the N, run this formula in two steps, and 

now you only have to compute X to the N over 2.

Play video starting at :4:23 and follow transcript4:23

And then that boils down to computing X to the N over 4, and so on. 

And so again, 

you're going to get this same sort of binary search type recurrence. 

To raise X to the Nth power, you do a constant amount of work, 

assuming multiplication takes a constant amount of time. 

And then you're left with a subproblem of size N over 2, 

raising X to the N over 2 power. 

So you only need a logarithmic number of multiplies to make this work. 

And so even raising x to a ridiculously large power like this would be perfectly 

tractable, not a problem at all. 

These types of problems show up a lot in number theory and in cryptography.

Play video starting at :5: and follow transcript5:00

So it is good that we have the ability to exponentiate things very quickly. 

Okay, here is a good old classic problem, 

let me turn off my face view here so you can see the entire problem. 

So this one, I think I first saw it on a competitive programming contest, but 

it's a very common problem called the "skyline" problem. 

You're given a set of rectangles, and 

you would just like to figure out the area that they cover. 

And for simplicity, they all live on a common base. 

So these are all buildings in a city skyline, and 

you'd just like to figure out how much total area is covered by all of them. 

So how can we approach this problem?

Play video starting at :5:39 and follow transcript5:39

This would be another example of, essentially, Merge Sort, I would say. 

So, basically, all you need is merge. 

We can kind of design an algorithm that really does kind of invoke 

the essence of Merge Sort. 

So I'm going to take half of the rectangles and color them red, and 

another half of the rectangles and color them blue. 

I just chose arbitrary n over 2 rectangles to be red and an n over 2 set to be blue. 

And then I'm going to recurse on those two sets of rectangles and 

recursively compute a skyline profile for each one. 

A skyline profile is just this kind of piecewise constant function that I've 

drawn below.

Play video starting at :6:16 and follow transcript6:16

So after spending 2T(n/2) time, I have these two profiles, 

kind of the red profile and the blue profile. 

And now all I need to do is merge those together into one common profile, 

after which I can easily compute the area covered by that profile by just scanning 

across and kind of integrating up the area inside the profile. 

So how do you merge these two things together? 

It's very similar, actually, to the merge from Merge Sort. 

I'm just going to kind of scan through those two profiles in lockstep and 

keep a running maximum as I trace out the tallest building as I go. 

And that only takes me linear time. 

So the total running time is going to end up being just n log n.

Play video starting at :6:55 and follow transcript6:55

The same exact mechanics and the same exact recurrence as Merge Sort. 

Okay, this picture should look familiar. 

We have in many of our prior modules talked about a problem called domination 

radius, which is very similar to this one. 

Here, I'm given the heights of n individuals standing in a row, and 

I would like to find what I call the longest line of sight. 

So, basically, find me the two individuals that can see each other over the tops of 

everybody in between. 

So those two individuals have to both be taller than everybody in between them. 

And I want to find the two such individuals that are farthest apart in my 

lineup.

Play video starting at :7:33 and follow transcript7:33

So that's the problem. 

I could, of course, solve this quite efficiently if I ran an algorithm for 

the domination radius problem that we had introduced in prior modules. 

But since our goal here is to practice using Divide and Conquer, 

let's see if we can actually approach this problem also with Divide and Conquer. 

And it turns out that leads us to an n log n solution, basically. 

So I like this problem because it really does give you kind of a prototypical 

application of Divide and Conquer. 

So the idea is I'm going to divide the problem in the most natural way, 

just divide it in half. 

So I have the first half and the second half, and 

I'm going to recursively run the algorithm on the first half and on the second half.

Play video starting at :8:14 and follow transcript8:14

What that will give me is the longest line of sight 

between a pair of individuals on the first half and 

the second recursive call will give me the optimal solution in the second half. 

The pair of individuals in the second half that have the longest line of sight 

between them. 

The only case that doesn't cover would be a pair of individuals that kind of one 

lives on the first half, one lives in the second half, and 

I want to find the best solution of that form. 

If I can do that, then I'm done, because I can just compare the three solutions I get 

completely in the first half, completely in the second half, and 

kind of straddling the dividing line, take the best solution, and that's the answer. 

And it turns out in just linear time, you can find the optimal solution for 

the best line of sight that crosses over from the first half to the second half. 

You do have to be a little bit careful when you do this. 

The obvious first attempt of just picking maybe the tallest person on the left half 

and the tallest person on the right half does not actually work.

Play video starting at :9:12 and follow transcript9:12

In fact, in this example, 

it doesn't work because the tallest person on the left half is kind of blocked by 

a similarly tall individual that prevents the tallest person on the left half 

from even being viewable from anybody on the right hand side. 

So instead, I think one approach you could use is you find the tallest person on 

the left, you find the tallest person on the right. 

I think you take the shorter of the two of those people and 

project across from that person, and that will give you the optimal line 

of sight that crosses over between the two halves. 

You can do that in linear time. 

So this again gives you the same recurrence as Merge Sort, 

and we get n log n as a resulting running time. 

Okay, here is another simple, classic problem. 

I give you an array, and within that array I would like to find 

the sub array whose sum of elements is as big as possible.

Play video starting at :10:5 and follow transcript10:05

So maximum sum over all possible sub arrays. 

Presumably there are some negative numbers in my array, otherwise this would 

be a very boring problem because the answer would be the entire array. 

This is a fairly well studied problem. 

There are lots of interesting ways you could approach it if you want to kind of 

look at maybe the naive or brute force approach as a starting point, 

then how many different subarrays are there? 

A sub array is just characterized by its starting and ending location. 

So if I loop over all possible choices for starting in any location, that's 

n sub 2 different possible subarrays on the order of n squared of them. 

And if I just check every subarray by looping over its contents and 

adding it up, that's another loop.

Play video starting at :10:47 and follow transcript10:47

So actually, my very naive approach would run in n cubed time for 

solving this problem. 

You can improve that pretty easily to n squared by checking 

every one of your on the order of n squared subarrays in only constant time. 

You can do that with a nice trick called computing prefix sums. 

So as a pre-processing step, what I'm going to do is scan through my array and 

just keep a running sum and write those down. 

So at every location in the array, I know the sum of the elements up to that point. 

And now given that array of prefix sums, 

I can easily now compute the sum of any subarray in just constant time. 

So to compute the sum from i up to j, I'll take the prefix sum that goes up to j.

Play video starting at :11:33 and follow transcript11:33

That's all the elements that go up to the jth element. 

And now I just subtract off the prefix sum up to the i minus first element, 

leaving the sum of all the elements between i and j. 

So in constant time, just using a difference of two prefix sums that I've 

pre-computed, I can evaluate any of my subarrays. 

So that gives me a quadratic total running time. 

I can actually improve on that, though, with Divide and Conquer. 

So Divide and Conquer will lead to an n log n running time, again, 

with the same recurrence as Merge Sort. 

So I will divide my array in half.

Play video starting at :12:8 and follow transcript12:08

I will recursively run the algorithm on the first and second halves that will give 

me the optimal solution that lies entirely within the first half. 

So the best possible sub array that lies entirely in the first half, 

and the best possible subarray that lies entirely in the second half. 

So the only type of solution I haven't covered yet 

would be the best possible subarray that straddles across the two halves. 

And that you can actually compute easily in linear time because I can 

kind of decompose that problem into, tell me the maximum sum of 

a prefix of the right hand side, and I glue that together with 

a maximum possible sum of a suffix in the left hand side. 

So I can really just consider those two problems independently and 

put the results together. 

So on the right hand side, I basically compute prefix sums. 

Again, I scan from the dividing line outwards, and I keep a running sum.

Play video starting at :13:3 and follow transcript13:03

And I just remember where that running sum was the biggest, 

and that's the prefix that I care about. 

And then on the left hand side, again, I scan backwards from the dividing point, 

keeping a running sum, and I just remember where that running sum was the biggest, 

and that's the suffix of the left hand side that I care about. 

I put those two things together, and that will indeed be the maximum 

sum subarray that crosses over between the two halves of my array. 

Take the best of the three solutions that I've computed, and 

that's the overall optimal solution. 

And so, if you look at the running time, 

this satisfies our familiar Merge Sort recurrence, and so we get n log n. 

The running time picture so far has been kind of boring, 

because everything has basically been Merge Sort in terms of its running time. 

But we will see one or 

two examples that are perhaps a little bit more interesting in a moment.

Play video starting at :13:56 and follow transcript13:56

Another interesting note, this problem can also very easily be solved in just linear 

time, and we'll see how to do that when we study dynamic programming a little bit 

later on in the course. 

So this is a nice example problem to look at from several different algorithmic 

vantage points. 

Okay, let's look at a fun problem in computational geometry. 

This is the bichromatic matching problem. 

The input here is a set of blue points and 

a set of red points in the two dimensional plane, the same number of both. 

And what I would like to do is draw a collection of line segments. 

Each one is going to connect a blue point to a red point, but 

I'm not allowed to have any of those segments cross.

Play video starting at :14:38 and follow transcript14:38

And so how can I do that? 

Is that even possible? 

And so the goal is to devise an algorithm that, if it's possible, 

computes the line segments that will connect those points together. 

It turns out this is not only always possible, 

but we can very quickly find a solution in, again, 

n log n time with the same recurrences as Merge Sort, although the answer 

here ends up essentially looking a little bit more like Quick Sort, perhaps. 

And it relies on a really, really cool theorem in computational geometry that 

this is really just an excuse for me to be able to tell you about this cool theorem. 

It's called the "ham sandwich" theorem. 

And what the theorem says, is that if I have a collection of points in the two 

dimensional plane, some of them are labeled ham and 

some of them are labeled cheese, this is a ham sandwich, I can always find 

some line in the plane that evenly subdivides both the ham and the cheese.

Play video starting at :15:36 and follow transcript15:36

So half the ham is on both sides and half the cheese is on both sides. 

The line might actually go through some of my points. 

That's perfectly fine. 

Moreover, I can actually find this magic line in only linear time. 

This is actually a little bit tricky, so I won't actually go into the details of how 

that's done, but you can do it in just linear time. 

And actually, the ham sandwich theorem generalizes to higher dimensions too. 

So in three dimensions, if I have ham points, cheese points, and 

lettuce points, I can always find a plane that simultaneously subdivides all 

three sets of points.

Play video starting at :16:12 and follow transcript16:12

So if I now just look at the applying kind of the ham sandwich theorem to this 

problem, then all I do is I will divide my points with a ham sandwich cut. 

So half the reds and half the blues are on both sides. 

And that basically decomposes my problem into two independent subproblems that can 

just be solved recursively from that point on. 

So I would think almost an analog of Quick Sort. 

I spend linear time kind of partitioning my problem, but in a way that basically 

creates two independent subproblems, because none of the line segments I draw 

on one side of the ham sandwich cut are going to interfere with the line segments 

that I draw on the other side of the ham sandwich cut. 

So I keep decomposing and decomposing until eventually I end up with just 

a single red and a single blue point in a subproblem, and 

then I just connect them with a line segment. 

So this also runs in just n log n time, 

because it takes me linear time to divide the problem in half.

Play video starting at :17:10 and follow transcript17:10

And then I solve recursively two half sized subproblems. 

So far, we still haven't seen any interesting running times 

that deviate from what Merge Sort had done. 

So actually here, we will see a different running time, 

even though the recurrence may look a bit similar. 

So this is an interesting example from the world of parallel algorithms. 

So here's the setup. 

I have a row of processors. 

They're all connected kind of in a line, and 

they're all connected to a global clock.

Play video starting at :17:41 and follow transcript17:41

So they're synchronized to a global clock. 

So every clock tick, the processors can all do a small amount of computation, 

some constant amount of computation. 

But these are extremely simple processors. 

Each one has only a constant number of bits of memory. 

That means that they really can't do too much and 

they really can't store much information. 

In particular, they can't even count as high as N, because to count up to N, 

the number of processors you would need log base, two of n bits of memory. 

And here we only have a constant number of bits of memory, like two or 

three bits of memory.

Play video starting at :18:16 and follow transcript18:16

So each processor can't even fathom a number as big as N. 

They can only count up to, like a constant, essentially. 

So what we would like to do is synchronize the processors. At some point in time, 

We're going to activate the leftmost processor, 

we send it a message saying ready, and then some distributed protocol is going to 

take place that eventually, hopefully in a short amount of time, will cause all 

of the processors to enter a common fire state all at once in the same clock tick. 

So how do we synchronize the processors if they can't even count as high as N? 

So, like, the usual approach would be that the leftmost processor starts sending 

a message down the line. 

It takes N-1 steps for a message to reach the other side.

Play video starting at :19:1 and follow transcript19:01

But by then, the leftmost processor has kind of forgotten about, you know, 

it can't really start counting up to N or 

anything like that to synchronize with when the message would hit the other side. 

So how do we make this work? 

How do we synchronize the processors? 

So this is actually a pretty non-trivial problem. 

I think I remember first seeing it in a graduate class on parallel algorithms back 

at MIT, where it was an interesting class. 

To get an A in the class, all you had to do was solve half the homework problems, 

and I think I barely got an A in the class. 

It was a pretty tough class, but this was one of those homework problems.

Play video starting at :19:37 and follow transcript19:37

It's actually related to a very cool and kind of well known problem 

that sometimes also has been used as a job interview problem. 

But since it's maybe getting to be pretty well known, 

I'd be surprised if you see it nowadays as a job interview problem. 

So in this problem, kind of as an aside, I give you a linked list. 

And the linked list normally ends by pointing to null at the end. 

But you could also imagine a linked list that has its final element pointing back 

into the linked list at some other earlier element creating a loop at the end. 

And suppose I would like to figure out which of these two cases is reality. 

So, does my linked list end with a pointer to null, or does it end with a loop?

Play video starting at :20:19 and follow transcript20:19

This is, of course, easy to do if you're allowed to use maybe some extra memory. 

So you can just mark the elements as you walk down the linked list. 

And if you hit null, you know which case you're in. 

If you hit a marked element, you know that you're in a loop. 

But maybe I'm in an environment where I don't have the luxury of being able to use 

extra memory. 

Maybe I'm in a parallel environment where lots of different processes 

are using the same linked list, and I don't want 

them to get confused by each trying to mark the elements in the linked list. 

So can I solve this problem with only a constant amount of additional memory.

Play video starting at :20:54 and follow transcript20:54

So that makes things a lot more interesting, 

because I can't kind of mark the elements that I've already seen. 

And it turns out that there is a really, really clever approach for solving this 

problem that is just interesting to know in and of its own right. 

It's sometimes called the "slow-pointer fast-pointer" approach, or the "tortoise and 

the hare" approach. 

So you basically send two pointers down the linked list, 

one of which moves faster than the other. 

So in each step, the tortoise pointer moves ahead by one element and 

the hare pointer moves ahead by two steps. 

So after one step of my algorithm, this is what things look like. 

So the bunny rabbit is racing ahead and leaving the turtle in its dust.

Play video starting at :21:38 and follow transcript21:38

So, of course, as this process continues, if any of these elements, 

these pointers, reach a null pointer. 

You know for a fact that your linked list ended with a null. 

The hard part is realizing that you end with a loop. 

But that's easy to do also here, because as the slow and 

the fast pointer move forward, then eventually the hare is moving so fast, 

it will actually, you know, start getting stuck in the loop, and it'll loop around. 

It'll actually lap the tortoise and catch up and meet the tortoise another time. 

So if these two elements meet, these two pointers align, 

say after t time steps, then we know that we're stuck in a loop because 

that's the only way that the hare could have caught back up to the tortoise. 

There's actually another interesting variant of this where if the two pointers 

meet, at that point you can actually introduce another tortoise pointer and 

start these moving forward.

Play video starting at :22:37 and follow transcript22:37

And it turns out that the place where those two meet actually is this 

interesting node to which the linked list wrapped back around and 

had a back pointer to that particular node. 

So you can actually identify this kind of base 

node that's the base of the cycle at the end of the linked list. 

That's actually pretty easy to see. 

If you continue letting this process go forward until 2T steps. 

You know, T steps is what it took for the first intersection of the slow and 

the fast pointer. 

After two t steps, the two tortoises are actually going to be in that same 

place because, well, one of them has only been moving for T steps. 

So it's in the same place that the original tortoise would have been 

after T steps.

Play video starting at :23:18 and follow transcript23:18

The other one has been moving for 2T steps. 

So it's where the hare would have been after T steps. 

And so, you know, after 2T steps, 

these two tortoise pointers are going to be at the same place and the same place 

that you had originally had the meetup between the tortoise and the hare. 

And that means that these two have been traveling together since they 

originally met at this kind of base node of the cycle. 

So really cool idea. 

Sometimes, this is called Pollard's rho heuristic, 

I guess because a linked list with a loop looks kind of like the Greek letter rho. 

And it actually is useful in a surprising number of situations.

Play video starting at :23:55 and follow transcript23:55

It can be used, for example, to develop a fast factoring algorithm, 

things you would not expect. 

>> From the structure of this algorithm as it's just been described. 

So it's kind of a neat trick to know. 

And it turns out this is actually useful for solving the firing squad problem. 

So imagine that I have two pointers that I'm basically sending down this list of 

processors, one of which moves faster than the other. 

So here the fast pointer is going to move one processor ahead at every clock tick. 

The slow pointer is going to move only one processor ahead every three clock tick.

Play video starting at :24:30 and follow transcript24:30

So it moves one third of the speed of the fast pointer. 

And if you can kind of imagine what happens with those speeds, the fast 

pointer is going to race all the way down to the end of the chain of processors, 

bounce off that end, and get back to the middle processor at exactly the same 

time as the slope pointer reaches the middle processor. 

And so this basically allows us in linear time to realize which processor is 

the middle processor. 

That's the processor on which these two pointers finally converge. 

And once you've identified the middle processor, you can now do divide and 

conquer, because you can essentially treat both of the two halves kind of as 

independent subproblems. 

You kind of treat the middle processor as an endpoint in both directions, and 

you send a ready message going to the right and to the left. 

So both of the two sides on the right and 

on the left will now repeat the same protocol in parallel.

Play video starting at :25:25 and follow transcript25:25

And so by induction, that's a smaller version of the same problem. 

You know that that will eventually result in synchronization of those processors. 

So a really cool technique using divide and conquer, along with the slow 

pointer fast pointer trick that has application in parallel algorithms. 

The recurrence here is actually kind of interesting as well, 

because if you look at the recurrence, it took you linear time in order for 

these pointers to converge in the middle. 

And then you had your two recursive subproblems, one on the left and 

one on the right. 

So you might think that the recurrence is the same recurrence from merge sort. 

However, in this case, since we're operating in parallel, 

the two subproblems are actually being solved simultaneously.

Play video starting at :26:10 and follow transcript26:10

So the total amount of time for both of them to be solved is still just one copy 

of t of n over two instead of two copies. 

That would be normally the case if you solve one problem and 

then the other in sequence. 

So this actually only ends up solving to linear total time, 

which is quite impressive. 

Okay, we have reached our final example. 

This is an important one because matrix multiplication is a very, 

very important problem. 

A large number of computational cycles are spent multiplying matrices in a wide 

range of applications in data analytics and AI, and lots of different subfields, 

modeling and simulation and whatnot. 

So if we have the ability to multiply matrices quickly, 

there are a lot of benefits.

Play video starting at :26:55 and follow transcript26:55

In fact, you can show that the very, very fundamental problem of solving a linear 

system involving n variables and n equations, that's actually basically 

equivalent in terms of running time to the time it takes to multiply two matrices. 

So if you can improve the time to multiply two matrices, 

you can also improve the worst case running time for 

coming up with the exact solution for a linear system. 

So very fundamental, very important problem. 

The naive approach, kind of the straightforward approach for 

multiplying two matrices runs in N cubed time. 

Because to compute every single element of the output matrix, say, 

the ij elements of the output matrix, 

requires basically taking a dot product of the ith row of X and the jth row of Y. 

So you sum up all of the pairwise products of the elements in those vectors and 

add them together, and that gives you Zij. 

That gives you one element of the output matrix in linear time.

Play video starting at :27:52 and follow transcript27:52

And so do that for all n squared elements of the output matrix, and 

you get n cubed as your total running time. 

Now, for a very long time, that was the best we knew for 

how to multiply two matrices together. 

I guess down here in the corner, I've shown an example of just multiplying two, 

very small, two by two matrices. 

And so you can kind of see what the output elements in this case end up being. 

It turns out, though, this picture is quite relevant, 

because you can actually multiply matrices with a divide and conquer based approach. 

You can actually multiply matrices blockwise. 

So if I take two large matrices of size N by N, 

I can actually divide them up into quadrants.

Play video starting at :28:35 and follow transcript28:35

Each quadrant is an N/2 by N/2 matrix. 

So in this picture here in the lower left, A is actually an entire submatrix of 

size N/2 by N/2, and the same for all of these other eight submatrices. 

And I can actually multiply my N by N matrices by basically doing two by two 

matrix multiplication on those blocks. 

And so what I end up with is, 

is the same formula that I would get with two by two matrix multiplication. 

But now, instead of individual elements being multiplied and added up, 

they're actually N/2 by N/2 matrices being multiplied and added together. 

And so this gives me kind of a recursive way to multiply 2N by N matrices. 

That involves, I guess, a number of multiplications of 

smaller matrices of size N/2 by N/2, how many?

Play video starting at :29:26 and follow transcript29:26

So if I look at the resulting matrix here, it looks like I have to do, I'm counting 

eight individual matrix multiplications on N/2 over by N/2 matrices. 

ABCDEFG and H, they're N/2 by N/2 matrices. 

So to calculate all of the terms in this output matrix, 

I have to do 8 recursive multiplications on half sized matrices. 

That's going to be 8T(N/2) in terms of the recurrence that I'm going to get. 

And then I have to do a few additions. 

I see 4 plus signs. 

So I'm going to be doing four additions on also n over two by n over two matrices.

Play video starting at :30:4 and follow transcript30:04

Adding two n over two by n over two matrices, 

that's just a quadratic amount of time. 

So theta N squared. 

So I end up with a recurrence that is 8T(N/2) + plus theta of N squared. 

And now if nature has been nice to me, this will hopefully represent 

an improvement over the naive N squared algorithm for matrix multiplication. 

Sadly, it does not. 

So if you solve this recurrence, you actually end up with n cubed. 

So all we have really done is come up with a messier, 

more complicated recursive way of getting an N cubed running time, 

rather than a simple method based on just three for-loops.

Play video starting at :30:40 and follow transcript30:40

However, all hope is not lost here. 

There is a famous result due to Volcker Strassen from the late 60s 

that shows how you can actually compute the output elements of this 

product matrix using not eight but only seven recursive multiplications. 

And this really kind of surprised people when it came out because no one really 

would have thought that you can just kind of do some algebraic rearrangement 

of things and only have to get by with seven multiplications. 

I guess the trade off is you're doing a lot more additions. 

If you look at all the different additions that you have to do to calculate the four 

blocks of the output matrix. 

I guess I counted 18 separate additions. 

However, every single addition takes quadratic time, and 

whether you're doing 18 or 18,000, 

that's still just a constant that disappears inside the big O notation here.

Play video starting at :31:36 and follow transcript31:36

All of the additions still take just, you know, on the order of N squared time. 

The, the key thing that improves here is instead of having 8 T of n over 

two, you now have 7 times t of n over two, because you only have to 

compute these kind of seven intermediate product matrices. 

You can actually check that each one of those involves a single recursive 

multiplication of two N/2 by N/2 matrices. 

And then you just do a lot of additions and 

subtractions to piece everything together to get the terms of the output. 

And so if you now look at the resulting recurrence, 

this actually does help the bottom line. 

It solves to n to the log base two of seven, instead of n to the log base two of 

eight, which would have been n cubed, and that's roughly n to the 2.81. 

So that is actually a substantial improvement over n cubed.

Play video starting at :32:27 and follow transcript32:27

This actually does make a difference in practice with very large matrices. 

So what is kind of actually the state of the art for matrix multiplication? 

It's an interesting story algorithmically. 

So of course you can't beat n squared because your matrices are of size n 

squared. 

So that's kind of a trivial lower bound, but in terms of upper bounds. 

So there's Strassen's algorithm n to about the 2.81. 

And that was improved in about a couple decades ago to n to the 2.376 by 

Coppersmith and Winograd, and that was the reigning best bound for a long time.

Play video starting at :33:3 and follow transcript33:03

This was not exactly a practical algorithm. 

It's kind of imagine that you took Strassen's algorithm and 

just made it much, much, much more complicated. 

So the running time bound here kind of requires really big matrices, and 

it's not super practical, but it is interesting at least, 

because this is a very important problem in algorithmic theory. 

So this was where things stood for a long time. 

And maybe about a decade ago, the race has started up again with some very 

minor improvements in the thousandths position after the decimal point. 

But usually what that means is that over time, with enough research, 

people will hopefully be able to make some more substantial improvements 

in the running time of this key problem, because I can't imagine that 

mother Nature would really intend for the actual answer for 

a fundamental problem like this to be end of the 2.3727 or something. 

So hopefully there is just a better algorithm out there waiting to be 

discovered for matrix multiplication and all of the other problems that 

are equivalent to it, like solving linear systems and such.

Play video starting at :34:9 and follow transcript34:09

So a couple of exciting examples of Divide and Conquer, 

there are many more out there, but it's nice to kind of just understand some 

standard types of problems that you can approach successfully with the technique. 

[MUSIC]