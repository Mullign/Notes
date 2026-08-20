To reinforce our understanding of 

performance analysis using O notation, 

let's look at a couple of examples. 

This also will give us an excuse to introduce 

an incredibly important topic in the world 

of algorithms, which is sorting. 

Along the way, we'll also see 

some high-level techniques for just 

designing algorithms in general. 

Performance analysis, there are many ways to do it. 

Maybe one of the simplest is what you 

could just call simply loop counting. 

For example, if I have an outer loop that 

executes N times and then inside of that 

an inner loop that executes 

N times for each iteration of the outer loop, 

then obviously that takes a total of Theta N^2 time. 

If you like to visualize that, 

you're maybe looping over all of 

the elements in an N by N matrix, 

and that would be one way to think 

about things graphically.

Play video starting at ::52 and follow transcript0:52

Another example maybe slightly more sophisticated. 

I have an outer loop that runs N times, 

a middle loop that runs N times for 

each iteration of the outer loop and then a loop 

inside that that runs another log 

N times for each iteration of the middle loop. 

This would add up to a total 

of N^2 log N. Remember, again, 

that if you start at N and 

keep dividing by 2 in each iteration, 

going from N to N/2 to N/4, 

that takes a logarithmic number of steps. 

Simple loop counting is 

a very useful way to do performance analysis, 

and it's actually all you need for 

a very wide range of algorithms. 

Let's now look at a couple 

of examples from the world of sorting, 

just to illustrate how we analyze algorithmic running time. 

Sorting is really good for this because there 

are a large number of sorting algorithms out there.

Play video starting at :1:42 and follow transcript1:42

It gives us a nice sandbox to play in that illustrates 

many different types of algorithm design techniques 

and many different types of analysis techniques. 

Sorting is an incredibly important problem 

to study in algorithms. 

It's a very widespread problem. 

Lots of computational cycles 

are spent on sorting every day. 

Sorting is also a key building block of many algorithms. 

Many algorithms start by sorting as 

a pre processing step and then doing something. 

I like to jokingly tell my students, sort first, 

ask questions later because 

lots of times problems get much 

easier if you first sort 

the input as a pre processing step.

Play video starting at :2:21 and follow transcript2:21

Let's go ahead and look at 

a couple of sorting algorithms. 

This is one that's very trivial. 

It's called selection sort, 

and you can say that it adheres to 

the overall design principle of incremental construction. 

Here we're just simply building up a solution, 

one element at a time. 

That's what incremental construction is all about. 

With selection sort, you scan the array, 

find the smallest element, put it 

first. That's where it's supposed to go.

Play video starting at :2:47 and follow transcript2:47

Then you scan the remaining elements, find again, 

the smallest element, put it second, and so on. 

You're just building up a sorted array, 

one element at a time. 

If you pause the process 

after i iterations of that main loop, 

then your array will basically look like this. 

It'll have the first i elements 

in their proper sorted locations, 

followed by the rest of the elements 

that you still have to sort out. 

Running time wise, this is actually 

quite straightforward to analyze with loop counting. 

The outer loop here just executes N times because 

you're overall just scanning through 

the array and fixing all the elements one by one. 

The inner loop here doesn't always run for N iterations.

Play video starting at :3:26 and follow transcript3:26

It actually gets faster and 

faster as the algorithm progresses. 

It runs in N-1 iterations initially, 

then N-2, then N-3, and so on. 

If you think about it in terms of 

that picture of looping over a matrix from before, 

you're actually looping over a 

triangular shaped portion of the matrix, 

but that's still on the order of N^2. 

It's half of N^2. 

This is still a Theta of N^2 running time. 

Another nice example of 

incremental construction is given by insertion sort. 

This again, follows 

the general principle of incremental construction.

Play video starting at :4:1 and follow transcript4:01

You're adding elements one at a time into 

your instance and keeping 

your solution up to date as you do that, 

incrementally constructing your solution. 

If you take a snapshot of 

insertion sort at any given point, 

after i iterations, you will have 

built up a sorted prefix of size i. 

You will have sorted effectively the first i elements and 

every iteration of insertion sort 

involves taking the next element, 

the i plus first element, 

and inserting it into the sorted prefix you've built 

up so far to make a sorted prefix of size i+1. 

How do you do that? How do you take 

each subsequent element and 

insert it into its proper location? 

Usually, the way you do that is just by swapping it 

backwards until it reaches 

the correct final resting place. 

If you want to think about running time here again, 

we can use loop counting.

Play video starting at :4:56 and follow transcript4:56

The outer loop runs N times because 

we're inserting N elements. 

To insert each element, 

this "while" loop just swaps it backwards until it reaches 

its correct location and that takes 

up to order N time in the worst case. 

Order N^2 again is our running time, 

Theta N^2 in the worst case. 

These are worst case guarantees. 

In the best case, if you already have a sorted array, 

this only takes linear time. 

It can run much faster if your array is nearly sorted, 

but in the worst case, the guarantee is not so great. 

It's quadratic, just like selection sort, 

and just like bubble sort, 

which is another very common, 

very prevalent sorting algorithm that 

also runs in N^2 time in the worst case.

Play video starting at :5:39 and follow transcript5:39

A bubble sort is a good example of 

an algorithm design principle 

that you could call iterative refinement. 

Very prominent in areas like optimization, 

for example. Where here, 

you start with a solution that's 

not correct or not optimal, 

and you just keep improving 

it over a series of iterations. 

In the case of bubble sort, 

we're going to just make our array a little more 

sorted after every pass over the array. 

Bubble sort will scan the array. 

If it finds a consecutive pair 

of elements that are out of order, 

a big element followed by a small element, 

it'll swap them and that 

improves the sortedness of the array as a whole. 

Bubble sort just keeps making passes and keeps doing this 

until it notices that 

the entire array is sorted, and then we're done.

Play video starting at :6:25 and follow transcript6:25

What would be the running time of bubble sort? 

Well, every pass takes linear time. 

The main question is, how many passes. 

That's actually easy to analyze as well. 

If you think about it carefully, 

the first iteration of 

bubble sort that scans through the array is going to 

effectively drag 

the biggest element all the way to the end, 

where it will then reside and stay forever. 

Then the second pass of bubble sort 

will certainly take the next to largest 

element and move it all the way to the second to 

last position of the array, and so on. 

After k iterations of bubble sort, 

the final k elements are in their correct locations.

Play video starting at :7:4 and follow transcript7:04

It's almost the exact opposite picture 

from selection sort. 

This shows us that after n iterations, 

bubble sort will terminate, 

so n^2 is the worst case running time. 

We've seen a couple of algorithms, 

and we've thought about them all 

from an iterative perspective, 

nested loops and such. 

But there are other ways to think about 

to articulate, to analyze algorithms. 

Another prominent approach is using recursion. 

We're not going to say a huge 

amount about that right now, 

but I just wanted to motivate 

the importance of maybe thinking 

about things from 

a different viewpoint, a recursive viewpoint. 

We're actually going to spend an 

entire module coming up soon, 

learning how to think recursively and to 

analyze algorithms that are designed recursively.

Play video starting at :7:52 and follow transcript7:52

That can involve some interesting challenge. 

But just think about how we could re-articulate some of 

our existing sorting algorithms through 

the lens of recursion for selection sort. 

All you have to do is get the right first element; 

put the minimum element first, 

that's the right first element. 

Then how do you finish up 

up the rest of the sorting process? 

Let recursion deal with it. 

Put the minimum element first and 

then follow that by what you get when you 

recursively sort the rest of the remaining elements. 

The nice thing about recursion 

is that you can trust it to give 

the right answer just based on 

the principle of mathematical induction.

Play video starting at :8:29 and follow transcript8:29

Any smaller problem than your original, 

you can just assume by induction, 

recursion will properly solve, which is kind of nice. 

Insertion sort, how would 

you articulate that recursively? 

Well, you could say, I'm 

going to take the first element and just 

insert it into what you get when 

you recursively sort everything else. 

I guess in keeping with the last slide 

where we talked about insertion sort, 

maybe insert the last element into what 

you get when you sort the rest of the array. 

Very simple, very clean ways 

to describe these algorithms recursively. 

A couple of interesting notes. 

One is that the running time isn't any 

different if you implement these algorithms recursively, 

as stated here versus iteratively.

Play video starting at :9:12 and follow transcript9:12

It's effectively doing the same work. 

It looks a little bit different 

in terms of the way we've described the algorithm, 

and that might make it a little harder from 

a thought process perspective 

to analyze the running time. 

Articulating things recursively can have advantages, 

maybe from an implementation or a design perspective, 

but it can also have challenges. 

It can make things a little trickier to think 

about maybe from an analysis perspective. 

Although in a few modules, 

we'll see that there are some good tools available 

for analyzing recursive algorithms. 

An approach like this might also be good for say, 

sorting a linked list because 

a linked list is a very recursively oriented structure. 

It is a first element, 

and then a pointer to another linked list, 

which is everything else.

Play video starting at :9:55 and follow transcript9:55

These sorts of approaches might be more 

straightforward to implement if you're trying to 

sort a linked list versus an array. 

That's about all I want to say about 

the iteration versus recursion 

just as different viewpoints. 

There is actually a very prominent 

algorithm design technique 

out there based on recursion, 

which is called divide and conquer. 

We're going to study that in 

much more detail in the module on recursion. 

But just to highlight a prominent sorting algorithm 

based on this recursive principle of divide and conquer. 

Merge sort basically operates by merging sorted lists. 

What you do with merge sort is you first 

recursively sort the first half of your array, 

you recursively sort the second half of your array.

Play video starting at :10:38 and follow transcript10:38

In code, that's extremely straightforward. 

Here's just some high level pseudocode 

effectively that illustrates how 

easy it is to implement merge sort. 

You just spend one line of 

code calling merge sort recursively on the first half, 

one line of code calling 

merge sort recursively on the second half. 

By induction, we can just trust 

that those two recursive calls will do 

what they're supposed to do and sort 

the first and second halves of our array. 

That's another principle that I often just 

tell my students is trust recursion. 

Any time you recursively 

solve a smaller part of your problem, 

just trust that recursion 

is going to do what it's supposed to do. 

We get these two sub arrays that are both sorted, 

and then all you have to do to finish off 

the entire sorting process is merge them together.

Play video starting at :11:22 and follow transcript11:22

Merging together two sorted arrays 

is a very straightforward process 

that just takes linear time. 

If you have two combined arrays of size N, 

the process of merging them 

together into one big sorted array, 

takes just linear total time. 

There's a few ways that you could 

articulate that process. 

In fact, we could articulate 

that recursively or iteratively. 

Recursively would just consist 

of get the first element right. 

Look at the two leading elements of 

your two sorted input arrays. 

Take the minimum of the two, 

that's the element that clearly has to go first.

Play video starting at :11:55 and follow transcript11:55

Then how do you finish off the merge process? 

Well, that's recursions problem. 

Just finish off the merge process 

by recursing on everything leftover. 

You could merge that way, 

or you could merge in more of a loop based fashion. 

This is also a common way it's done iteratively. 

Here's a snapshot in the middle of that process, 

where we've already merged the yellow pieces of 

the two input arrays to 

create the yellow part of the output array. 

The next step involves 

looking at where these two pointers are.

Play video starting at :12:26 and follow transcript12:26

You have these two pointers that are 

advancing in lock step through the two input arrays. 

You look at the elements 

pointed at by those two pointers, 

and you take the smaller of the two elements, 

and that's the next element to go into the merged array. 

Again, you're constructing 

the merged array one element at a time. 

At each step, you're taking the smaller of 

the two leading input elements and putting that 

next into the output array 

and advancing its corresponding pointer. 

The process of merging 

two sorted arrays of combined length N, 

that's easy to implement and easy to analyze, 

that takes linear time. 

But the overall merge sort 

algorithm is a little bit more interesting 

because merge sort is doing a whole bunch of 

these merges of all sorts of different sizes. 

How do we get a handle on the running time of 

merge sort in its entirety?

Play video starting at :13:19 and follow transcript13:19

There are a couple of ways to do that, 

but I wanted to highlight one nice way that I would 

recommend as an approach to keep in mind for algorithm 

running time analysis in general and that's to think 

about running time from 

the perspective of individual elements, 

add up the total running time you 

spend per element over all the elements. 

I like to, again, 

joke with my students that as algorithm designers, 

we boss around these elements of data all the time. 

Think about how they feel for once. 

Think about life from 

the perspective of an element of data. 

Whether or not it's advisable to personify our data, 

if we think about merge sort from this perspective, 

let's first just think about a single merge process. 

You merge together two sorted arrays of combined length N, 

that takes order N time. 

On a per element basis, 

that's like constant time 

for each of the participating elements.

Play video starting at :14:15 and follow transcript14:15

Every time you do a merge, 

every single element involved in 

that merge undergoes one unit of work. 

Now if I'm an element of data, 

how much work is done to me 

during the entire merge sort algorithm? 

Well, every time I'm part of a merge, 

that's one unit of work done to me. 

All I need to do is figure out how many merges I'm 

a part of during the entire merge sort algorithm, 

and that's actually pretty easy to figure 

out because every time I take part in a merge, 

the sorted array that I'm part 

of effectively doubles in size. 

How many times can that happen? 

Well, a logarithmic number of times. 

If you start with one element and keep 

doubling and you stop when you reach N elements, 

that's just the opposite of 

the process that we talked about before where you start 

with N elements and keep 

halving until you get down to one element.

Play video starting at :15:4 and follow transcript15:04

That also just takes a logarithmic number of steps. 

Each element undergoes a logarithmic amount of 

work because it participates 

in a logarithmic number of merges. 

Therefore, since there are N elements, 

the total running time is N log N. 

Thinking about running time from 

the perspective of an element of 

data can be a very powerful idea. 

We'll see this used quite a few 

times over the course of the semester.![[Screenshots/Screenshot 2025-08-25 at 1.41.49 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 1.42.19 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 1.43.32 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 1.44.44 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 1.45.49 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 1.46.43 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 1.49.28 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 1.57.13 pm.png]]