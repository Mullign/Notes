[MUSIC] ![[Z7i7e8SIRs6vn_AI6lW3eQ_ef4f0aac50c54f90a41b58d2c3355ef1_Randomized-Quicksort.pdf]]

In the previous module, we briefly reviewed a number 

of common sorting algorithms, but one was conspicuously absent. 

That was Quicksort, one of the most popular sorting algorithms out there. 

The reason for that is that Quicksort is often implemented using randomization, 

and now we actually have the tools to be able to analyze it properly. 

So, let's spend a few minutes talking about Quicksort. 

Quicksort is a very simple algorithm. 

It's a wonderful example of the so-called divide and conquer 

algorithm design paradigm. 

To sort an array with Quicksort, all you do is you pick some element in your array. 

—it's called a pivot element— 

and then you spend a linear amount of time kind of partitioning the array about that 

pivot element into two blocks: 

a block of elements less than the pivot element 

and a block of elements bigger than the pivot element.

Play video starting at ::57 and follow transcript0:57

At a high level, 

those two blocks are roughly in the right places, 

and all you need to do to complete the sorting process is to independently sort 

those two blocks with recursion. 

So, you apply Quicksort to the first block, 

and you apply Quicksort recursively to the second block, and you're done. 

That is Quicksort. 

That is the entire algorithm. 

I should probably say a few more details about some of the pieces here, 

in particular, the partitioning process. 

So, in linear time, we can do this partitioning process where we take 

the array and split it up into these two blocks. 

There are a couple ways that this is commonly done.

Play video starting at :1:34 and follow transcript1:34

Maybe the most common is shown in this left diagram here, 

where you have kind of two pointers that scan inwards from the sides of your array. 

So, you have a pointer i that scans forward through the array. 

As long as you see elements less than the pivot, you scan i forwards. 

And then, this pointer j that scans backward through the array 

from the back of the array, 

and you keep scanning as long as you see elements greater than the pivot. 

We're happy with those elements because they're in the right place. 

So, you keep scanning until both pointers get stuck— 

i is going to get stuck on an element bigger than the pivot, 

and j is going to get stuck on an element less than the pivot. 

And then, you can unstick things by just swapping those two elements and 

then continuing the scan inwards until the two pointers meet.

Play video starting at :2:19 and follow transcript2:19

So, in linear time, that will partition. 

There's another approach that you might also see that's fairly common, 

where you build up these two blocks— again, one block having elements 

less than the pivot; the next block having elements bigger than the pivot. 

And, every step, you try and move j forwards, 

and you can do that as long as the next element is bigger than the pivot. 

If the next element is less than the pivot, you would actually 

need to swap it with the element right ahead of i and advance i instead. 

So, in either case, either i or j moves forward by one, 

and this is going to also take just linear time to partition the entire array. 

Another nice feature of both of these approaches is that they partition in 

place, so they don't require substantial additional memory. 

They just rearrange the array within the memory buffer that it comes in 

to begin with.

Play video starting at :3:10 and follow transcript3:10

And, that's quite advantageous. 

If we can partition in place, 

that actually means the entire Quicksort algorithm also runs in place. 

And, that's often touted as a feature, a benefit of Quicksort as compared to other 

fast sorting algorithms, like say, Mergesort. 

Quicksort runs in place, 

it does not require a substantial amount of extra memory. 

That's a real benefit of using this algorithm. 

Now, there's one little caveat to what I just said. 

Quicksort is a recursive algorithm, and as such, 

it will actually use extra space on the stack whenever it makes recursive calls; 

however, probably not a huge amount of additional space as long as 

the recursion depth is not too great.

Play video starting at :3:53 and follow transcript3:53

So, that's the actual Quicksort algorithm. 

Let's think about performance of Quicksort. 

It turns out performance really boils down to the quality of our partitions. 

So, you can have so-called bad partitions, which are very unbalanced 

—maybe one element on one side versus n minus 1 on the other side— 

or you could have good partitions which are balanced partitions 

—ideally, half and half, 

but any partition where you have maybe a constant fraction reduction in 

problem size on both sides. That would probably do the trick. 

That would be good. 

And so, if you have— Let's look at both of these two cases.

Play video starting at :4:33 and follow transcript4:33

If you always have a bad partition, what happens there? 

Maybe that would happen if you were unlucky enough to pick the min or 

the max in your array as the pivot, 

because then you'll have just that one element on one side of the partition and 

all other n minus one elements still unordered on the other side of the partition. 

So, you've spent linear time effectively just putting one element in its proper 

place with that first partition operation, 

and you still have n minus 1 elements to go. 

So, if you keep doing this—if you're unlucky with every single partition, 

you will end up with a quadratic worst case running time 

—n squared is the worst case that can happen with Quicksort. 

On the other hand, if you have always good partitions where each side of 

the partition represents —a constant factor reduction from 

the original size of your array—then you end up with the running time of n log n. 

One way to see this is very similar to what we did earlier with merge sort. 

We can kind of look at things on a per element basis.

Play video starting at :5:32 and follow transcript5:32

So, if I'm an element of data, how many partitions do I take part in? 

So, I'm an element of data. 

I start out in an array of size n, and then I take part in a partition. 

And now, I'm part of a smaller block. And then, I take part in another partition; 

I'm part of an even smaller block. 

As long as the blocks are reducing by a constant fraction in each of those steps, 

that means the number of partitions that I take part in will be logarithmic. 

So, that's good.

Play video starting at :5:59 and follow transcript5:59

How much time is spent on each element in each of those partitions? 

Well, each partition takes linear time, 

so, if you spread that out across the elements in the partition, that's only a constant 

amount of work per element in each partition it takes part in. 

So, to figure out how much work or time you spend per element, 

it basically suffices to ask, how many partitions does an element take part in? 

And, the answer being log n, gives you a total running time of n log n. 

So, relatively straightforward to see that the running time is efficient if you 

always have good splits, 

and you can actually guarantee this. 

There is actually a variant of Quicksort where 

you partition on the median in each step. 

The median is the dead center element that has half the elements on both sides, 

and that gives you a perfectly balanced split in every single partition operation.

Play video starting at :6:51 and follow transcript6:51

That gives you the best possible asymptotic bound 

for Quicksort—you get a worst case running time of n log n. 

However, this typically isn't used in practice that often because the algorithm 

that we actually use to find the median —as part of the partitioning process— 

it's rather complicated and it actually has a relatively high hidden constant in it. 

And so, Quicksort, with this exact split on the median, 

it would be a very complicated algorithm to implement, and 

it would have a relatively high hidden constant inside of its running time. 

So, it's typically not used in practice that often. 

What variants of Quicksort are often considered in practice? 

We just talked about the version that runs in n log n, worst case time, and 

pivots on the median element of the array. 

Another very common, very simple heuristic that tries to kind of— as much as 

possible tries to guarantee good splits with the partitions 

is to just look at, say, three elements: 

the element that happens to be first, the one that happens to be last, and 

the one that happens to be sitting in the middle of the array.

Play video starting at :7:55 and follow transcript7:55

And, you pick the median of those three elements, crossing your fingers and hoping that that 

is a decent choice for a pivot that gives you a relatively balanced split. 

And, in most cases, that does a decent enough job that your running time is 

actually relatively efficient. 

So, in practice, this does get used. 

It's sometimes called a median of three Quicksort. 

Although, if you have a malicious adversary, they could certainly craft 

an input that would still make this run in quadratic worst case time. 

So, this is just kind of a heuristic that often works well in practice. 

Now, since this is a module on randomized algorithms, 

we are excited about the next variant —maybe even the simplest one possible— 

where you just pick the pivot to be a random element in your array.

Play video starting at :8:38 and follow transcript8:38

And, that also leads you to a running time of n log n, both in expectation and 

also "with high probability"—which is something we haven't quite defined yet. 

We're going to see that notion in a future video in this module. 

So right now, let's focus on the expected running time. 

And, we can analyze that in much the same way that we just analyzed the running 

time on a per element basis. 

So, the same thing holds. 

Every single element still undergoes a constant amount of work for 

every partition operation that it takes part in. 

So, if we're thinking per element, 

all we need to do is figure out how many partitions each element is a part of.

Play video starting at :9:18 and follow transcript9:18

And, it turns out, at a very high level, —We'll kind of show you a picture 

in a second—that the number of partitions that you take part in is order log n 

in expectation, because the sizes of the subproblems that you belong to 

shrink, according to a randomized reduction process. 

So, you basically spend log n expected work per element and then times n elements. 

You can apply linearity of expectation to add that up over all your elements, and 

you get a total expected running time of n log n. 

So that's the high level analysis of randomized Quicksort. 

But, I think it's good to look at the details a little bit more carefully 

in the dynamics of the subproblems to get a better 

and more intuitive sense of what's happening. 

So, here's a picture of the recursion tree 

of the entire randomized Quicksort process. 

So, at the top level, I've just done a partition of the entire array, 

so every single element got compared to my random pivot, 12.

Play video starting at :10:15 and follow transcript10:15

And, things less than 12 got put on the left, 

and things bigger than 12 got put on the right. 

And, those two subproblems are then processed recursively. 

So, within those subproblems, again, I pick a random pivot element, 

compare everybody to those pivot elements, to that pivot element, 

and they go left or right, and so on. 

So, this is a tree that depicts, 

basically, all of the work done in randomized Quicksort. 

And, if I would like to think about that work on a per element basis, 

then I have to trace what happens to one element through that process. 

What does this process look like from the vantage point 

of one specific generic element? 

Here, I've highlighted a generic element—this yellow 7 element.

Play video starting at :10:56 and follow transcript10:56

What does randomized Quicksort look like from the vantage point of 7? 

Well, at a top level, 7 got compared to the pivot. 

That's kind of one unit of work done to 7. 

And then, 7 ends up, after that, in a smaller subproblem. 

Now, 7, again, gets compared to a random pivot—another one unit of work—and 

again, it ends up in a smaller subproblem. 

So, as we just said, the total work done to seven is just a constant amount 

of work per partition that it takes part in. 

And so, it really boils down to: Well, how many partitions or— 

What's the depth that the 7 ends up going down to in this diagram?

Play video starting at :11:32 and follow transcript11:32

So, if you look at the subproblem sizes, you start with a subproblem of size n. 

You end up in a smaller subproblem; you end up in a smaller subproblem. 

These subproblems actually follow a randomized reduction progression. 

And, maybe a nice way to see that,is— We can relate this, actually, to another 

algorithm that we've just recently studied as well, when we introduced 

randomized reduction. And, that was randomized binary search. 

It turns out that you actually do the exact same comparisons on this 7 in 

randomized Quicksort as you would if you were randomized— 

if you were doing a randomized binary search for 7 in a sorted array. 

In fact, you could even argue, I guess: If I'm the 7 element, 

then what does randomized Quicksort look like from my vantage point?

Play video starting at :12:18 and follow transcript12:18

It kind of looks like somebody's doing a randomized binary search for 

me, as the target element. 

Why is that? 

Well, look at all your elements in sorted order. 

What does randomized binary search look like, if you're searching for 7? 

Well, you pick a random pivot, you compare seven to that pivot and 

realize, 7 is less than the pivot. 

And so, I'm going to now restrict my search to everything less than the pivot. 

And, that took one comparison.

Play video starting at :12:43 and follow transcript12:43

Now, again, in this subproblem, I compare seven to a randomly chosen pivot. 

And here, I go to the right because seven is bigger than the pivot. 

So, seven is ending up in a progression of smaller and smaller subproblems. 

And that progression we already talked about in our previous lecture— 

That satisfies the conditions of our randomized reduction lemma. 

And so, we know that we spend the order of log n steps, we make— 

on the order of log n expected comparisons along the way with the seven to wrap up 

the randomized binary search process. 

And, if you look at the work done to seven, —the comparisons done to seven— 

they're exactly the same on both sides. 

You get compared to the pivot as you walk your way down the tree.

Play video starting at :13:24 and follow transcript13:24

And so, this is another way just to highlight some similarities between 

algorithms that we've talked about, and 

also give you a little more of a detailed sense of what's happening with 

the dynamics of analyzing a randomized Quicksort. 

So, we've basically finished analyzing randomized Quicksort, 

concluding that the running time is n log n in expectation. 

That's pretty cool. 

We've spent a while building up some tools in this module to be able to 

analyze substantial randomized algorithms, and we have just done that. 

We've analyzed a substantial randomized algorithm in fairly simple terms. 

[MUSIC]