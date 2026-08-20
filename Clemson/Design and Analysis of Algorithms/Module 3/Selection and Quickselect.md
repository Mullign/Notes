
![[Selection and Quickselect.pdf]][Music] 

Dean: In elementary school, we all learn the so-called 

three Rs: reading, writing, and arithmetic. 

In the study of algorithms, 

maybe the fundamental topics we learn are 

the three S’s: sorting, searching, and selection. 

The topic of the moment for this video is selection, 

something that actually dovetails quite nicely 

with our discussion of Divide and Conquer. 

The selection problem is 

very fundamental and very straightforward, 

given a set of n elements in no particular order, 

I would just like to find the kth largest element. 

I always get into arguments with students about whether I 

should call this the kth largest or the kth smallest. 

What I mean here is if k=1, 

I'm looking for the minimum element. 

If k=n, I'm looking for the maximum element.

Play video starting at ::51 and follow transcript0:51

K=n/2 is also special. 

That's the median element, 

so half the elements are smaller, 

half the elements are bigger. 

You could also call this 

the rank of the element that you're looking for. 

I'm looking for an element of rank k, 

that would be the element that is in position 

k after you sort the elements in your input. 

Very fundamental problems, it's really 

easy to solve certain special cases. 

If you're looking for the min or the max, 

you can just scan your elements and keep 

a running min or max and get the answer in linear time. 

You can, of course, calculate the element of rank k for 

any k after sorting because it's 

just in position k. In n log n time, 

you can perform selection.

Play video starting at :1:31 and follow transcript1:31

Our goal in this discussion is to 

see if we can perform selection in just linear time 

for any value of k. We can essentially do 

this using a very simple algorithm 

called “Quickselect”, sometimes. 

It's a very close relative of QuickSort, 

almost a one-sided version of QuickSort. 

All the algorithm does, 

if you're looking for an element of rank k, 

is it basically starts by 

partitioning the array just like QuickSort. 

You pick a pivot element, 

you rearrange the contents of your array in 

linear time so that you have 

elements less than the pivot, 

followed by the pivot, followed 

by elements bigger than the pivot. 

After you do this, you know the rank of the pivot, 

because the pivot is now in 

the proper location as if the array was sorted. 

You can use that as 

a guide post to figure out if the element of 

rank k belongs in 

the first set of elements 

or in the second set of elements.

Play video starting at :2:24 and follow transcript2:24

I won't say the first half or the second half 

because our choice of the pivot 

may not necessarily exactly split 

the elements into two half-sized sets. 

Once you have found the rank of the pivot, 

that's the location of the pivot 

within this array after you've done the partition, 

then you have three cases. 

Either the rank of the pivot r 

is the rank k that you're looking for, 

in which case, the answer is the pivot, 

and you were lucky and you can 

finish the algorithm then and there, 

or the element you're looking 

for has a rank less than the pivot, 

so it belongs to the left sub-problem, 

so we can just recurse on the left 

sub-problem and select for it there. 

Or if the rank of the element 

you're looking for is bigger than the rank of the pivot, 

then you can recurse on the right-hand side sub-problem. 

The only catch or thing to be 

careful about is that you have to adjust 

the rank that you're looking for if you recurse 

on the right-hand side because locally, 

within just the right-hand sub-problem, 

the element you're looking for is of rank, say, 

k minus r, the rank of the pivot. 

Because these elements that are now smaller, 

the ones less than the pivot have left 

the picture so your rank within 

just the right-hand sub-problem is different than 

your global rank within the entire array. 

That's a standard caveat that is 

a common bug when you're implementing selection.

Play video starting at :3:44 and follow transcript3:44

We basically recurse on one or the other side. 

It's almost exactly QuickSort. 

It's just we only recurse on one of the 

two sub-problems, not on both. 

How do we choose the pivot? 

We have the same concerns here as we 

did with QuickSort about good pivot selection. 

If we're lucky, we can choose a pivot that 

gives us a relatively balanced partition. 

If we're unlucky, we choose 

pivots that give us very unbalanced partitions.

Play video starting at :4:11 and follow transcript4:11

The worst case here is 

still n^2 just like it is with QuickSort. 

But if you choose the pivots randomly, 

you get a version of 

the algorithm we call randomized Quickselect, 

and that actually runs in just linear expected time. 

It's a little bit faster than 

QuickSort because you're only 

recursing on one side rather than on both sides. 

It's actually relatively easy to show 

that the expected running time here is linear. 

We can actually use some very 

familiar tools from the last module, 

geometric random variables, expected time 

until success, that sort of thing. 

Here's the picture that we want to look at. 

Imagine that you're running 

iterations of randomized Quickselect.

Play video starting at :4:53 and follow transcript4:53

The very first iteration does a partition of 

the entire array and splits it into 

two pieces and recurses on a smaller sub-problem. 

Then you do another partition, 

you do another partition. 

The series of iterations that I'm looking at here, 

those are all of the partitions done by 

Quickselect as it continues 

to reduce the size of your sub-problem. 

Some partitions are lucky and that 

they lead to a good reduction in sub-problem size, 

some are not lucky. 

I think if you look at 

the mechanics of this randomized reduction process, 

we've seen this many times when we analyze 

randomized binary search and randomized QuickSort, 

you can argue that you have 

at least a one-third probability 

in any given partition 

of reducing your problem size to at 

most two-thirds of what it used to be when you go from 

one problem to the next problem 

after recursing on one or the other two sides. 

At every step, there's 

a one-third probability at least of 

success in reducing your problem size 

by a decent amount to two-thirds of what it used to be. 

Since your probability of success is at least one-third, 

you expect at most three iterations, 

three successive partitions before 

you hit one that is successful, 

that actually leads to a reduction in 

problem size to two-thirds of what it used to be.

Play video starting at :6:10 and follow transcript6:10

You can think of the algorithm as running in phases. 

The first phase is running partitions up 

until the first successful partition 

that reduces your problem size. 

Then the next phase again consists of iterations up until 

the second successful partition that again reduces 

your problem size to at 

most two-thirds of what it used to be. 

In each phase, we expect at most three iterations. 

In the first phase, just as accrued upper bound, 

every single iteration takes 

at most n units of time because it's 

partitioning an array of size at 

most n. But in the second phase, 

we've already gone through a successful iteration. 

The problem size has definitely shrunk to 

at most two-thirds of n in this case.

Play video starting at :6:51 and follow transcript6:51

So every iteration in 

the second phase takes at most two-thirds of n time. 

Again, you expect three iterations in the second phase. 

In the third phase, again, 

you expect at most three iterations, 

each of which takes at most two-thirds squared of n time. 

If you add that up, you get 

a geometric series that sums up to something that's on 

the order of n. That's 

the expected time of randomized Quickselect. 

We can select now for 

the rank k element in linear expected time. 

An interesting question might be, though, 

can you solve the same problem in 

just linear worst-case time?

Play video starting at :7:26 and follow transcript7:26

It turns out the answer is yes, 

but it's not at all obvious 

from the get-go how to do this. 

It actually took a group of 

relatively famous computer scientists 

a long time to resolve this problem back in the day. 

Let's maybe go through the motions or 

the thought process that they may have gone 

through trying to solve this problem, 

especially because it involves 

a really interesting journey through Divide and Conquer. 

If you wanted to say find the median of your array, 

we'll focus on the median for now, 

the element of rank n/2. 

Then maybe if I apply Divide and Conquer, 

according to the usual pattern that 

I see divide and conquer being applied, 

I'll just divide my array in half and 

I will recursively find the median of 

the first half and the median of the second half. 

Then I'll wonder, is this actually 

going to help me at all because is 

the median of the entire array even related in 

a useful way to the median of 

the first half and the median of the second half? 

It turns out the answer is yes, 

the median of the entire array actually 

lives between those two sub-medians.

Play video starting at :8:30 and follow transcript8:30

That's really actually easy to show. 

Suppose I take the contents of the first half and 

I just arrange those elements in sorted order. 

m_1, the median of those would be in the middle. 

If I then take the contents of the second half, 

the right-hand side sub-problem, 

and I arrange that in sorted order, 

m_2 would be the middle element in that ordering as well. 

Let's just assume m_1 is the smaller of 

those two medians without loss of generality. 

Now, how many elements 

overall are bigger than m_1 in this picture? 

At least half the elements on 

the left side are bigger than m_1. 

By transitivity, at least half the elements on 

the right side are also bigger 

than m_1 because m_2 is bigger than m_1, 

and then you have half the elements 

being bigger than m_2.

Play video starting at :9:15 and follow transcript9:15

More than half the elements in my array 

are m_1 or bigger than m_1. 

That means the median can't be 

less than m_1 because there's 

just too many elements bigger than 

you if you are an element less than m_1. 

A characteristic of the median is that you can only have 

half the elements less than 

you and half the elements smaller than you. 

If more than half the elements in 

the array are bigger or smaller than you, 

you cannot be the median. 

This argument disqualifies anyone smaller than 

m_1 from being the median 

because there are too many elements bigger than you. 

Similarly, by asymmetric argument, 

the median couldn't have been bigger than 

m_2 because there'd be too many elements less than you. 

The median of the overall array has to 

live between m_1 and m_2.

Play video starting at :10:3 and follow transcript10:03

What we basically are going to do then 

to finish up our Divide and Conquer approach is, 

in the block that had the smaller median, 

we're going to discard the elements 

that were smaller than that median, 

and in the block that had the bigger median, 

we're going to discard the elements 

that were bigger than that median. 

Remember, those are the ones we 

just disqualified from consideration. 

They can't have been the median of the overall array. 

The nice thing is, since we've actually thrown 

out the same number of elements on either side, 

less than the overall median 

and greater than the overall median, 

the median of the array remains unchanged. 

You cut the array back by 

getting rid of half of its elements, 

a quarter on both sides, 

but that preserves the median of the entire array. 

Now I have an array of half the size of 

my original where the median 

is still what the median of the original array was. 

I can just recursively 

select for the median on that array.

Play video starting at :10:56 and follow transcript10:56

That gives me an interesting Divide and 

Conquer algorithm where I take a problem of size n, 

and I've effectively divided it up 

into three sub-problems of n/2, 

the two original problems, 

and then this new problem that I get after I throw 

out half the elements and I'm left with 

a recursive problem size n/2. 

Of course, it took me a linear time to throw out 

these elements that were bigger and smaller 

than the block medians. I get this recurrence. 

Now I solve this recurrence because 

I'm an expert in solving recurrences. 

It's an increasing geometric series because, 

if I look at the work per level 

of recursion, it's increasing. 

I get n to the log base two of three, 

which is about n^1.58. 

Now I'm profoundly disappointed because I could 

have found the median just by sorting 

my elements in n log n time very easily.

Play video starting at :11:47 and follow transcript11:47

This is much worse than that. 

This is almost like n times the square root of n. 

It's a substantially worse 

running time than just sorting. 

I feel let down here because a lot of times, 

if Divide and Conquer is going 

to work at solving a problem, 

then the natural approach, 

like what we just did here, 

seems like it should work if nature is being kind to us. 

I guess, nature is just 

deciding not to be kind to us here. 

The obvious natural algorithm 

does not lead to a reasonably efficient running time. 

We need to look for 

alternative approaches or modifications of this technique.

Play video starting at :12:26 and follow transcript12:26

In desperation, maybe we try 

dividing into three pieces instead of two pieces. 

If you try and figure out an approach based on this, 

it sadly doesn't work either. 

But interestingly, what does work is 

if you do an extreme version of Divide and Conquer here, 

you go down to the level of dividing your array up 

into tiny little blocks of size 5. 

There are other numbers than 5 that would work, 

but 5 is the right number to start with here. 

I'm going to divide the array up into 

n/5 blocks each of size 5. 

The nice thing about a problem of size 5 

is that that's only a constant-sized sub-problem, 

and I can find the median of each of those 

sub-problems in just constant time 

per sub-problem because it's only 5 elements. 

I can sort 5 elements in 

constant time and find the median.

Play video starting at :13:18 and follow transcript13:18

What used to take me a recursive sub call 

to find the medians of these little blocks, 

now I can just do that in only linear total time. 

I can find the median of each of these blocks of size 5. 

In just linear time, I know the block medians. 

There's a lot of them. There's n/5 of them. 

What I'm going to do now is 

I'm going to take the medians of the blocks. 

There's n/5 of them, 

and I'm going to find their median, 

and I'm going to do that recursively.

Play video starting at :13:49 and follow transcript13:49

I have n/5 block medians. 

I recursively run my median finding algorithm on those. 

That's going to take me T(n/5) time, 

I guess, because it's a set of n/5 things. 

Now I know the median of the medians of the blocks. 

It turns out that that element, 

let's call that M, 

that's a reasonably good choice 

for the pivot of Quickselect. 

I basically have used this approach here to 

get a decent estimate for a good pivot for Quickselect. 

It'll give me a balanced enough partition 

that using Quickselect with 

this choice of pivot will run in 

linear time. Why is that?

Play video starting at :14:31 and follow transcript14:31

Well, it turns out that if 

you use this particular choice of pivot, 

again, this value M, 

the median of those block medians, 

then you can show that 

at least three-tenths of the elements 

in your array have to be bigger than that element, 

the pivot, and at least three-tenths have to be smaller. 

That choice of pivot is relatively central. 

It's going to give you a balanced enough partition. 

I guess, if three-tenths of the elements 

are less than the median, 

that means at most seven-tenths are bigger, 

and at most seven-tenths are smaller. 

After you partition and recurse on one of the two sides, 

your sub-problem in the next iteration is going to be at 

most seven-tenths of what it 

was in the current iteration. 

You end up with an 

interesting recurrence for this algorithm. 

The first time we've seen a two term recurrence 

with very different sub-problem sizes.

Play video starting at :15:23 and follow transcript15:23

To solve for the median of n elements, 

we first used recursion 

to find the median of the block medians, 

that took T(n/5) time, 

and then we used that as a pivot for Quickselect. 

Quickselect does a linear time partition on that pivot, 

and it recurses on one or the other sides, 

but those two sides, 

each r of size at most seven-tenths of 

n. The next recursive 

sub-problem is only of size at most seven-tenths of n, 

this is the recurrence you get. 

If you actually expand this out in a tree, 

you will also get a geometric series. 

If you have a multi term recurrence like this, 

you also get a geometric series 

when you expand it out in a tree, 

and conveniently, it's a decreasing geometric series. 

The answer is just the contribution 

of what's sitting at the root, 

which is order of n. That's 

what gives you the overall running time of 

order of n because this recurrence 

solves to order n time.

Play video starting at :16:21 and follow transcript16:21

I guess, the only thing left to argue now is 

this claim that if I use 

the median of these block medians, 

that that's relatively central within my array. 

At least three-tenths of the elements have to be 

bigger than that choice and 

at least three tenths smaller. 

I can draw a similar picture to 

what I had drawn before to argue that pretty easily. 

Imagine that I had taken all of my blocks, 

and for each block, I arrange 

the five elements and the block in sorted order. 

Each column here represents one of my blocks with 

its five elements in sorted order 

from smallest up to largest. 

The medians of the blocks here 

are in that middle row, the third row. 

Those are all of the block medians.

Play video starting at :17:3 and follow transcript17:03

This is just for the sake of my proof. 

My elements aren't actually arranged this way. 

This is just a hypothetical saying, 

what if I did arrange all of my elements this way? 

If I were to take all the blocks 

and arrange them in sorted order, 

and then I'm going to arrange the blocks 

themselves in sorted order by their medians. 

That would put M, the median of 

the medians dead center in this picture. 

All of the block medians to the left are 

smaller than M. All of the block medians to 

the right are bigger than M. Now 

this lets us figure out easily, by transitivity, 

how many elements are bigger than M. Well, 

half of the block medians are bigger than M, 

and within those blocks, 

the elements bigger than the block medians, 

there's three-fifths of the elements in 

those blocks that are bigger than M by transitivity.

Play video starting at :17:53 and follow transcript17:53

I guess, half of the blocks, 

three fifths of the elements in those blocks are 

bigger than M. They're half times three-fifths, 

that's where we get the three-tenths from. 

A relatively straightforward argument 

to show that at least three-tenths of 

all the elements in your array are bigger and 

a symmetric argument also shows smaller, I guess, 

in this quadrant here than M. 

That wraps up the analysis of what was 

a very difficult algorithm for 

some very famous computer scientists to come 

up with in many decades ago. 

But the nice thing is, now that we have this algorithm, 

we can use it as a black box, 

we can select for the median of 

an array in just linear time, worst case. 

Why is that useful? Well, it's 

useful for a large number of reasons.

Play video starting at :18:40 and follow transcript18:40

I guess, if we think about Divide and Conquer, 

what's a natural place to divide a problem? 

Well, the median is a very natural place to divide 

the problem because half the elements 

are smaller and half the elements are bigger. 

If you divide a problem on the median element, 

you're dividing it in half. 

That really is the ideal choice for Divide and Conquer. 

The median finding application and Divide and Conquer, 

things kind of go both ways. 

We've used Divide and Conquer to 

build a successful algorithm for median finding, 

but median finding itself is 

also a useful part of many Divide and 

Conquer algorithms because it gives you 

the ability to ensure that you're 

dividing exactly in half. 

For example, we focused on 

selecting the median element in an array.

Play video starting at :19:26 and follow transcript19:26

But now that you can find the median in linear time, 

you can actually use that as 

the pivot for Quickselect and build 

a deterministic version of Quickselect that can 

now find any rank k element. 

The running time here just boils down to the recurrence, 

T(n) is T(n/2) plus 

linear because linear time to partition, 

and since you're partitioning on the median, 

then both of your two sides are exactly n/2 in size. 

If you solve this recurrence, 

you get order n. You can actually now 

use Quickselect to find the element of 

any rank given that we can now find 

the median in linear time if you partition on the median. 

Partitioning on the median and finding the median, 

that goes into that order of 

n term here in the recurrence. 

We can also now de-randomize randomized QuickSort. 

We initially focused on QuickSort, 

the fact that you can actually build 

an n log n in worst case version of QuickSort, 

and that's using this algorithm.

Play video starting at :20:25 and follow transcript20:25

We first find the median, 

and then we partition on that median. 

If we do that with QuickSort, 

we actually get an n log n, 

deterministic version of QuickSort. 

It's maybe not super practical, though, 

because the hidden constant is a bit high. 

There are lots of applications in the world of Divide and 

Conquer involving use of the median. 

[Music]