![[Divide and Conquer.pdf]]
![[Screenshot 2025-09-10 at 12.05.57 pm.png]]

![[Screenshot 2025-09-10 at 12.06.17 pm.png]]

[MUSIC] 

This video serves as 

a grand finale in our exploration of divide and conquer, 

in which I will discuss what I personally consider to be 

the most elegant examples of the technique in action. 

Maybe a good starting point for 

our discussion is to just remind ourselves of how 

we typically analyze divide and conquer 

algorithms by taking a recurrence and 

expanding it out in a tree format 

that allows us to add up the amount of work 

we spend per level of recursion 

in recursive divide and conquer algorithm, 

that always ended up as 

a geometric series for 

the types of recurrences that we're considering here. 

The series was either an unchanging series, 

a decreasing series or an increasing series, 

and it was easy to add up in any of those cases. 

I want to add one very brief additional extension to 

this idea because it will be 

useful for analyzing some of the algorithms that follow. 

Here, I'd like to consider 

recurrences that have an extra log term in them. 

Something like this, T(N) is 2T(N/2) plus 

instead of just like Theta(N), Theta(N log N). 

It turns out that we don't have to do 

too much extra work to solve 

these types of recurrences if there's 

an extra log factor or 

log squared factor or something in them.

Play video starting at :1:22 and follow transcript1:22

What you basically do is just pretend the log 

isn't there and solve 

the recurrence the way you normally would. 

Then based on whether you got an increasing, 

decreasing or unchanging series, 

we reintroduce the log in an appropriate way. 

What happens is if you have a decreasing series, 

remember that the answer there was just basically 

the contribution of the root of 

the tree, that's the same. 

The root of the tree now just has 

that log factor built into it. 

Nothing really is different if it's a decreasing series. 

The answer is still Theta of whatever was at the root. 

It's just this final term in your recurrence.

Play video starting at :1:57 and follow transcript1:57

If it's an increasing series, 

also, things don't change. 

The answer is the contribution of the leaves, 

that's still our familiar end to the log base b of a. 

The maybe interesting case is if 

it's an unchanging series, 

you have the same amount of work per level basically. 

In that case, previously, 

we just added a log factor. 

Here, we basically increase 

the exponent on our log factor. 

If we had a log factor 

to begin with, it turns into a log^2. 

If we had a log^2 to begin with, 

it becomes a log^3 and so on.

Play video starting at :2:29 and follow transcript2:29

Relatively easy to solve recurrences, 

even if they have this extra log term in them, 

we'll be seeing quite a few of 

those in the discussion that follows. 

Let's quickly work through a couple of 

practice problems just to make sure that we're 

comfortable with this extension 

of our recurrence solving technique. 

If we take a look at the first example, 

that's the one from the previous slide. 

If you temporarily pretend a log n isn't there, 

that's the regular old merge sort recurrence, 

and that involves an unchanging series, 

and the rule with an unchanging series 

is you just add an extra log factor. 

The solution here becomes 

n log^2 of n because you already had a log term. 

In fact, all of the first three recurrences here 

involve unchanging series when 

you pretend that the log term isn't there. 

You use the same rule for all of these, 

you just add an extra log factor.

Play video starting at :3:20 and follow transcript3:20

The third recurrence, I've just put 

some lower order terms here in 

the non recursive part just to scare you. 

But remember, you can safely just ignore those terms. 

The third recurrence is 

effectively the same thing as the second recurrence. 

All three of these recurrences, 

you would classify as an unchanging geometric series, 

if you look at the pre expansion. 

If we look at the next example, 

T(n) is 3T(n/2)+Theta(n log^10 of n). 

I'm not sure what algorithm that would come from. 

But if we wanted to solve this, again, 

we'd pretend that the log^10 

of n isn't there temporarily, 

expand things out in a tree, 

and then mentally, I guess we would realize this is 

going to be an increasing series, 

and so the rule here is that 

the contribution due to the leaves is the same.

Play video starting at :4:5 and follow transcript4:05

It doesn't even matter that there's this log part, 

the answer is n^log base b of a, 

n^log base 2 of 3. 

Nothing really different in this case. 

Next case is the case of a decreasing geometric series. 

Again, pretend that the log base 10 of n is not there. 

You get a decreasing geometric series 

when you expand things out in a tree, 

and the rule there is that the answer is 

just Theta of whatever 

the contribution of the root is, which in this case, 

is the n log^10 of 

n. Relatively straightforward to solve these, 

let's take a look at this final recurrence. 

This is one that would probably trip up 

students on a quiz, for example, 

if the log wasn't there, 

this would just turn into a constant, 

and this would be the recurrence that 

basically describes binary search.

Play video starting at :4:51 and follow transcript4:51

What does that look like when 

you expand it out in a tree? 

You actually get a constant contribution at the root, 

and then you get one sub problem of size 

N/2 that expands again to a constant contribution. 

You actually end up with a constant contribution on 

each level for a logarithmic number of levels. 

That makes sense because binary search, 

the solution is on the order of log 

n. This is actually an unchanging series. 

The rule there is you just add 

an extra log factor 

on top of the log that you already have, 

so you're actually going to get log^2 of n in this case. 

Just a bit of practice using 

this extended approach for solving 

recurrences with extra log terms.

Play video starting at :5:30 and follow transcript5:30

To motivate the next set 

of algorithms we're going to discuss, 

let's go back and look at some of 

the common sorting algorithms that we've already talked 

about and I guess one that we haven't talked about 

heap sort that we'll talk about in the next module. 

For each algorithm, I've written whether it 

is a stable algorithm and whether it runs in place. 

We've talked about in place before. 

That means you're not using 

a substantial amount of additional memory. 

Advantage of Quicksort is that it runs in place. 

Merge sort doesn't because the merging process 

is inherently hard to implement in an in place fashion. 

What does stable mean?

Play video starting at :6:7 and follow transcript6:07

This is a concept we haven't yet talked about in sorting, 

but it is pretty important. 

What it means is that equal elements 

stay in the same order during the sorting process. 

All the sevens stay in the same order as 

they originally were when you sort the array. 

You might say, well, who cares? They’re sevens? 

It doesn't matter if I rearrange them or not, 

but there are actually some very 

important applications of stability. 

If you're sorting, for example, 

multifield records, it can be extremely important.

Play video starting at :6:36 and follow transcript6:36

For example, if you sort your inbox 

based on the “date received,” 

and then you do a stable sort on from address, 

then elements with the same from address will 

stay sorted by date received, which is convenient. 

Stability is also a key underlying property that is 

exploited by a sorting algorithm 

for sorting integers quickly called radix sort, 

which we'll actually talk about in just a second. 

We'll have to round out 

our discussion of sorting with 

even more, sorting algorithms. 

Stability can be an important feature 

of sorting algorithms. 

But interestingly, it seems that it's hard to achieve 

both stability and in-place operation at the same time, 

at least with a fast algorithm. 

If you look at our slower algorithms, 

the quadratic time algorithms 

like bubble sort and insertion sort, 

they can easily be implemented in 

a stable fashion and so that they're in place. 

But all of our faster n log n sorting algorithms, 

it seems like you have to compromise.

Play video starting at :7:32 and follow transcript7:32

You have to pick either stability or in place operation. 

You can actually, in some cases, 

you can sacrifice in 

place operation to achieve stability. 

If you really care about stability, 

then what you can do is you can augment every element in 

your array with 

basically its sequence number in the array, 

and then when you sort, you can use 

those sequence numbers to break ties, 

and that will make your algorithm stable, 

but at the expense of in place operation because 

you're using extra memory to 

augment all of your elements. 

You can always achieve stability 

by sacrificing in place operation. 

But it seems it's one or the other here. 

We don't yet have a sorting algorithm 

in hand that is fast, 

stable, and in place. 

It turns out that this actually is possible.

Play video starting at :8:21 and follow transcript8:21

In the late 70s, 

a paper was published that showed 

an n log n sorting 

algorithm that was stable and in place, 

but it is incredibly complicated. 

I don't think I've ever seen it implemented. 

What I wanted to build towards here was a set of very 

elegant n log^2 n 

approaches that are both stable and in place. 

We'll see a variant of merge sort 

and a variant of Quicksort with 

n log^2 n as 

the running time where they're both stable and in place. 

These are the very 

beautiful and elegant approaches of divide and conquer. 

They even used divide conquer 

inside of a divide and conquered algorithm. 

Let's go back and build towards, 

I've mentioned Radix sort.

Play video starting at :9:3 and follow transcript9:03

Let's briefly talk about how 

Radix sort works because it's a useful algorithm to know. 

Radix sort is typically built on top of counting sort, 

which we have already talked about. 

Counting sort sorts n integers, 

each of size at most C in a very simple fashion. 

It basically scans your array, 

it builds a histogram of counts of all 

of the distinct values in your array. 

Then it unpacks that array of counts 

and rebuilds your array in sorted order. 

If you're careful, you can actually 

do this in a stable fashion. 

If you want this to be stable, 

you want all of the threes in your original array to 

end up in the same order in the final array, 

and so the way you do that 

is you take your histogram of counts, 

and from that, you build essentially a prefix sum array.

Play video starting at :9:54 and follow transcript9:54

Like P(3), for example, 

since we're focusing on elements of value 3, 

P(3) is going to be four because that's 

the sum of the counts 

of all the elements less than three. 

That also gives you the position at which you're 

going to want to put threes in the final array. 

If you're scanning through your array at this point, 

trying to rebuild it in 

sorted order, then scan through the array. 

The first element is a three. 

Where do I put the three in my final sorted array? 

I guess I put it in position 4. 

That matches what P(3) is here.

Play video starting at :10:28 and follow transcript10:28

It's position 4. 

The reason it's position 4 is because 

there are four elements less than three. 

That's basically what you get by doing 

a prefix sum calculation on your histogram. 

The value of P(3) is 

the number of elements of value less than three. 

That's equivalent to the index at which you'd 

want to put this three in the sorted array. 

After you put the three there, 

you can increment this value. 

The next three you see would be 

put it position 5, for example.

Play video starting at :10:56 and follow transcript10:56

You can basically scan through your array 

and use this array of prefix sums, 

if you want to call them that to tell you 

the indices at which you 

deposit each of the elements as you go. 

That will actually drop elements in 

sorted order and also in a stable fashion. 

This is counting sort. 

It runs in order(n+C)time. 

If C itself is on the order of n, 

then this is a linear time algorithm. 

Now we can move from counting sort to radix sort. 

Radix sort just basically does several passes of 

counting sort effectively to sort 

even larger integers in linear time.

Play video starting at :11:35 and follow transcript11:35

A lot of times we think of 

radix sort as a digit by digit sort. 

Imagine that you take the numbers you're 

sorting and you write them in some base. 

Here, I've written my numbers in base 10. 

You could write them in base 2 in binary. 

It turns out that typically for radix sort, 

we write them in base n because then the digits 

themselves are in the range from zero up to n-1. 

They're just the right size to use for counting sort. 

But in this example, I've written things in base 10, 

just because that's a little bit more familiar.

Play video starting at :12:4 and follow transcript12:04

What you typically then do is you sort digit by digit. 

You look at the least significant digit, 

and you sort on that, 

and then once you've sorted on that, 

you then sort on the second 

most least significant digit on the tens place, 

and then on the hundreds place, and so on. 

The key thing is that those sorts have to be stable 

because elements that have 

the same number in the hundreds place, 

they have to stay sorted on the tens and 

the ones place from the previous sorts. 

Basically, you just sort digit by digit. 

At the end, all of the numbers end up sorted. 

Sorting, starting from the least significant digit. 

The running time here, if you 

write your numbers in base n, 

that allows every single digit by digit sort 

to use counting sort and to run in linear time.

Play video starting at :12:48 and follow transcript12:48

The main question is just how many digits do you have? 

Writing things in base n, 

the number of digits is log to the base n of C, which, 

as long as you're sorting 

numbers of size n to a constant, 

that's going to be a constant number of digits. 

Typically, we describe the running time of 

radix sort as linear as long as you're 

sorting integers whose magnitudes 

are at most n to some constant. 

Another interesting fact about 

radix sort it's actually an old algorithm. 

It dates back to the era of punched cards and such, 

because if you want to sort a bunch of 

binary numbers that are represented by punched cards, 

hole punches for ones and non hole punches for zeros, 

you can build a mechanical sorting device 

that basically scans 

through all your cards and separates the ones 

that are punched versus the ones that aren't punched. 

With one pass of this mechanical sorting algorithm, 

you can separate the ones 

from the zeros in one of the digit positions, 

and then you can shift over the cards and sort on 

another digit position and separate 

the ones from the zeros mechanically. 

This is actually a very old algorithm 

dates back quite a ways.

Play video starting at :13:57 and follow transcript13:57

You can actually take radix sort and 

implement it in a forward direction, if you want. 

The traditional way is to go, 

least significant digit upwards using stable sorts, 

but you could also use more of 

a forward version of radix sort, 

where the first thing you do is you look at 

the leading digit and 

you partition on that leading digit. 

You now have all the numbers that start with one, 

followed by all the numbers that start with 

two and all the numbers that start with three, 

they're all grouped together. 

This is basically like what Quicksort does. 

It's a multi way partition operation on that first digit. 

That breaks up your array into 

blocks that you can then recursively 

sort on the remaining digits. 

This gives you a Quicksort-esque feeling, 

but it's another way that you could 

have done essentially a radix sort.

Play video starting at :14:45 and follow transcript14:45

The running time ends up being 

the same because you only have 

a constant number of levels of 

depth in your recursive process. 

You can actually phrase radix sort in a way that 

actually is more of a divide and conquer algorithm. 

We finished our aside on stability and on radix sort. 

Let's go back to the question of can we build algorithms 

for sorting that are both stable and in place and fast? 

A building block for this 

is a fundamental problem that's fun. 

Basically, if I have an array 

that's divided up into two blocks, 

A, followed by B. 

They don't have to be the same size.

Play video starting at :15:24 and follow transcript15:24

Can I rearrange the contents of 

this array so that now it's B followed by A? 

I'd like to do this in linear time, and crucially, 

I'd like to do this in place because this will 

be a building block for 

the algorithms that are developed in a second. 

Really easy, of course, if A and B have 

the same size because you can just scan through A 

and B and successively swap 

elements to interchange their positions. 

But how do I do this if A and B have different sizes? 

There are actually a couple ways you can do it. 

My favorite way actually is to simply reverse the array. 

If you reverse the array, 

we started with an array that had A followed with B.

Play video starting at :16:3 and follow transcript16:03

If you reverse that array, what happens? 

You end up with, I guess, B, 

but in reverse, followed by A, but in reverse. 

Reversing is something that you can do very 

easy in linear time and in place fashion, 

you just start at the end of the array and 

work your way in and swap elements. 

It's easy to reverse in place. 

How do we fix things now that we have 

B and A in the right place, but the reversed. 

We just apply a reverse operation to B 

and A separately and that gives you the contents of B, 

followed by the contents of A. 

That's one easy way that you can basically do in 

place block swap of two blocks within a larger array.

Play video starting at :16:46 and follow transcript16:46

How can we actually now use 

this to build more sophisticated algorithms? 

Well, what we're going to do is let's take a look at, 

for example, merge sort. 

With Merge sort, 

the difficulty is it's not in place. 

The merging algorithm that we use with merge sort is 

inherently not an in place algorithm. 

We have to allocate a new buffer 

and merge into that buffer. 

You can merge in a stable fashion, 

though, if you're careful. 

What we're going to do with merge sort is we're going to 

develop a merging algorithm 

that is both stable and in place, 

and it will run slightly slower in n log n time.

Play video starting at :17:21 and follow transcript17:21

That will give you a version 

of merge sort where the recurrence 

is T(n) is 2T(n/2)+Theta(n log n). 

There's an extra log n term here now. 

This is why we introduced the extensions 

for solving recurrences with extra log term. 

If you have a merge sort with this recurrence, 

the total running time is going to end up being 

n log^2 of n. The nice thing is, 

if all of the merges in 

merge sort are stable and in place, 

that means the entire merge sort algorithm will 

end up being stable and in place. 

All we really need to do is fix merge, 

and so in the slide that follows, 

I will tell you how to do a merge in 

n log n time in a stable, in-place fashion. 

That algorithm itself is going to 

be inherently based on divide and conquer.

Play video starting at :18:6 and follow transcript18:06

This is an overall divide 

and conquer algorithm merge sort that now 

uses divide and conquer for 

a small piece of its operation for the merge operation. 

How do we do merging in a stable in 

place fashion in n log n time? 

Consider having one big array that basically 

is broken up into two blocks L 

and R that are themselves sorted. 

I would like to merge everything together into one, 

so that the entire array becomes sorted. 

Normally, when you do merging, 

you have an iterative process where you 

walk through the two arrays and lock step, 

always taking the smaller of the two elements 

and putting it next in the merged array. 

I want to simulate that process. 

Go through the motions of merging the two arrays, 

but I'm not actually going to construct the merge array.

Play video starting at :18:53 and follow transcript18:53

I'm just going to walk through the two arrays, 

keeping those two pointers that I 

advance as if I was merging, 

and I stop when I've scanned through 

exactly half the elements in the array. 

At that point, the snapshot 

looks like this middle row here. 

I've scanned in the first array up to 

a certain point and in the second 

array up to a certain point. 

The total number of elements that I've scanned is 

exactly half of all the elements in my array. 

The elements I've scanned so 

far are actually all less than the median, 

and the elements I haven't scanned, 

they're all bigger than the median of my array. 

This breaks up my picture into four blocks, essentially. 

I've partitioned L into 

two blocks, things less than the median, 

things bigger than the median and the same for 

R. Now all I do is I 

run my in place 

block swap algorithm on the two middle blocks.

Play video starting at :19:43 and follow transcript19:43

What that does is it puts 

all the elements less than the median on the left. 

There's half of those elements less than the median, 

and all the elements bigger than the median on the right. 

In linear time, I have essentially partitioned 

my original merging problem into two merging problems. 

One involving all the elements less than the median, 

one involving all the elements greater than the median. 

These elements are in 

the right place in 

the left and the right hand side blocks, 

and so I can further complete the merge by just 

recursively applying my algorithm to 

the left side and to the right side. 

Everything here is happening in place because it's 

basically just fundamentally based 

on my block swap algorithm, 

which is itself in place. 

If you look at it carefully, 

it's also a stable algorithm.

Play video starting at :20:29 and follow transcript20:29

You can implement this so that 

it runs in a stable fashion. 

The total running time here is n log n because 

it satisfies the familiar merge sort recurrence. 

You're doing two recursive sub problems of size N/2, 

and then a linear amount of work 

outside of those sub problems. 

This is the stable in place 

merge that we plug into merge sort. 

What about Quicksort? 

It turns out that you can build a 

stable and in place version of, say, 

randomized Quicksort by making 

the partition operation stable. 

With Quicksort, normally, it runs in 

place because partitioning is an in place operation, 

but it's very hard to partition 

in a way that's both in place and stable.

Play video starting at :21:11 and follow transcript21:11

What we're going to do here is design an in place 

and stable partitioning algorithm 

that is slightly slower. 

It's going to be n log n in 

its running time instead of n. That's going to 

lead you to a running time of n log^2 

of n or randomized Quicksort, 

say with high probability. 

You can actually analyze this using 

the same tools that we 

had used in the previous module 

for analyzing randomized Quicksort. 

Just every element instead 

of undergoing a constant amount of 

work per partition involves 

a logarithmic amount of work per partition. 

You just get an extra log factor in the running time. 

How do we do partitioning in a stable in place fashion?

Play video starting at :21:50 and follow transcript21:50

If we can do that, that makes all of 

Quicksort run in a stable in place 

fashion because Quicksort is basically just 

doing partitions to do all of its work. 

That picture is almost of 

the mirror image of what we did with merge sort. 

To do a stable in place partition of an array of size n, 

I'm going to first recursively do a stable in 

place partition of the first 

and second halves of that array. 

There's 2T(n/2) in my running time. 

Divide the first half into 

elements less than the pivot 

and elements bigger than the pivot, 

and the same for the elements in the second half. 

This is all happened by 

induction in a stable in place fashion. 

All I need to do now to finish 

off the partition operation is again, 

run my in place block swapping 

algorithm to swap these two inner blocks, 

and that rearranges my array 

so that I have elements less than the pivot, 

followed by elements bigger than the pivot.

Play video starting at :22:45 and follow transcript22:45

Everything has happened in place, 

and if you look at it carefully, 

also in a stable fashion. 

We can make both merge sort and Quicksort run stabely 

and in place with 

only a mild degradation in their running time. 

For my final example, I wanted to revisit a problem 

that we talked about quite 

prominently in the first module, 

that is transposing a matrix in place. 

In that module, we talked about 

a pretty elegant n log n 

algorithm for solving the problem, 

where n is the total number of elements in the matrix. 

Here, we're going to see that we can also apply divide 

and conquer successfully to solve this problem. 

The running time will be a touch slower, 

it'll be n log^2 of n, 

but it's nice to see how 

so many different techniques can be 

applied to these common problems. 

As a starting point, let's look at 

a special case where 

my matrix only has two columns in it.

Play video starting at :23:38 and follow transcript23:38

This actually by itself is 

an interesting problem in its own right. 

If you look at the structure of what's going on here, 

let's say the two columns are A and B. 

In row major order, 

that means I have A1, 

B1, A2, B2, and so on. 

A and B are interleaved with each other. 

In column major order, 

I just have all of A followed by all of B. I would like 

to transform between these two representations 

if I'm transposing the matrix. 

This transformation actually has a nice name.

Play video starting at :24:7 and follow transcript24:07

It's called a “Perfect Shuffle.” 

It's familiar to anyone who has shuffled a deck of cards. 

Cut your deck of cards exactly in half. 

Those are the A and B arrays, 

and then you just riffle shuffle them together, 

and if you do that perfectly, 

you interleave one element from A, 

followed by one element from B and so on. 

I guess going from column major to row major order, 

that's a perfect shuffle, going 

from row major to column major, 

that's an “Inverse Perfect Shuffle.” 

Our starting point is, 

can we do either of these two 

in place in an efficient fashion? 

It turns out that there's a really nice way 

to do that with divide and conquer.

Play video starting at :24:47 and follow transcript24:47

It looks very similar to what we just talked about 

with merge sort and Quicksort 

running stably and in place. 

If you want to do an in place inverse, 

perfect shuffle, then what we're 

going to do is divide our array in half. 

Do an inverse perfect shuffle of the first half and 

an inverse perfect shuffle of the second half. 

By induction, I assume that's happening in place. 

What that's going to do is it's going to an interleave 

the first half and it's going to 

interleave the second half. 

That I end up with I 

guess the first half of A 

followed by the first half of B, 

and then the second half of A 

followed by the second half of B. 

To finish things off, I just need to swap 

these two inter blocks with my 

in place block swap algorithm, 

giving me all of A followed by all of B.

Play video starting at :25:32 and follow transcript25:32

The running time here, it's obviously m 

log m because I have the same recurrence that I have 

for regular merge sort in a 2T(m/2) plus 

order of m. I can 

actually run this algorithm either direction. 

If I want to do an inverse perfect shuffle in place, 

I run it in the forward direction that I've indicated. 

If I want to do an in place 

perfect shuffle, I run it backwards. 

I do the block swap first, 

and then I finish by doing two in place 

perfect shuffles to finish interleaving the elements. 

In m log m time, 

I can do either a perfect shuffle 

or an inverse perfect shuffle in place. 

Now using the in place 

inverse perfect shuffle algorithm that 

we just built up as a building block.

Play video starting at :26:16 and follow transcript26:16

Let's see if we can now do an in 

place transpose of a general matrix. 

We can do this by pretending that our matrix has 

only two columns and by running 

the preceding inverse perfect shuffle algorithm. 

I say, row 1 of our matrix, 

let's just pretend that it only has two elements. 

Those are actually going to be now blocks of 

elements of size n/2, 

that treat those blocks as single elements. 

If you do that, then effectively, 

the matrix now just has two columns, 

and we can run our inverse perfect shuffle algorithm 

to un-interleave those columns from each other. 

Whereas initially in row major order, 

we had R1 followed by R1', 

then R2 followed by R2' in memory. 

After the inverse perfect shuffle, 

now in memory, we're going to have R1, R2, 

R3 and so on, 

and then R1', 

R2', R3', and so on.

Play video starting at :27:10 and follow transcript27:10

The left hand side and the right hand side, 

they're actually in the right place in memory. 

If we're trying to as a goal, 

convert our matrix into 

column major format because we have 

the first half of the columns 

followed by the second half of the columns. 

The trouble is these two big blocks 

are still not in column major format. 

They are themselves still in row major format. 

To finish off the algorithm, 

all we need to do is recursively 

apply it to the left block and to 

the right block to convert them 

respectively from row major to column major format. 

Then the entire matrix will be 

represented in memory properly 

in column major format. That's the algorithm.

Play video starting at :27:49 and follow transcript27:49

All it's doing is running my in place 

inverse perfect shuffle algorithm many 

different times in a recursive hierarchical fashion, 

and so the entire algorithm 

is actually going to be in place. 

It's running time is pretty easy to analyze as well. 

I have two recursive calls to sub problems of size N/2, 

where capital N is the size of the entire matrix. 

Then the non recursive part, 

the in place inverse perfect shuffle, 

that usually runs an m log m time, 

but that slows down by a factor of 

n because I'm running it on blocks. 

What used to be a swap of two elements 

is now a swap of two blocks of elements. 

That now takes order N log N. If I solve this recurrence, 

I get N log^2 of 

N as the total time of my algorithm slightly 

slower than the n log n that we came up with in 

Module 1 with a very different algorithmic approach.

Play video starting at :28:42 and follow transcript28:42

But I think it's neat that again, 

you can approach the same problem from 

many different lines of 

attack from an algorithmic point of view. 

I like this algorithm also because it's 

divide and conquer within a divide and conquer, 

like we saw with the stable in 

place versions of Merge sort and Quicksort. 

[MUSIC]