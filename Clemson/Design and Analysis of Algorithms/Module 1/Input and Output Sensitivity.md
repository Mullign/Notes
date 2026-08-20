It's, of course, common for 

the running time of an algorithm to 

depend on the number of elements, N, in your input, 

but it can also depend on other parameters that 

characterize the complexity of 

either the input or the output. 

I think it's useful to take 

a quick look at just a few examples that 

highlight how we can get 

this input or output dependency in our running times. 

To start with, this is a simple sorting algorithm 

called counting sort. 

It sorts n integers, 

each one of size at most C in running time, order of n+C. 

It's perfectly fine to have 

a running time that 

depends on multiple parameters like this. 

In fact, if C is on the order of n itself, 

this will just sort in linear time, very, 

very fast sorting algorithm 

if you're sorting small numbers. 

But we could call this an input 

sensitive running time because it depends, 

not only on how many numbers you're sorting, 

but on how large those numbers are.

Play video starting at :1:1 and follow transcript1:01

If you want to sort really large numbers, 

it's going to be a lot slower. 

This phenomenon happens with many algorithms. 

The running time depends, not only 

on how many things are in the input, 

but somehow also on the complexity of those things. 

Let me briefly tell you how counting sort works. 

It's a very simple algorithm. 

All you do is make one linear scan 

over your array, and in doing that, 

you build a histogram of counts, 

telling you how many times 

every distinct value occurs in the array. 

Then one scan over that histogram of counts, 

allows you to reconstruct the array in 

sorted order by putting 

the appropriate number of every value.

Play video starting at :1:38 and follow transcript1:38

Very, very simple algorithm, 

the running time is easy to see, 

but it does highlight very well 

this phenomenon of input sensitivity. 

If we now look at what we could call output sensitivity, 

consider the following simple problem. 

I have an array that's sorted, 

and I would like to print out all of the values 

that live in a certain range between A and B. 

Now, of course, in just order log and time, 

I can do two binary searches to figure out 

where in my array A and B would live, 

let's suppose that there are k elements in 

the range between where those two points are. 

The trouble is now I have to print out those k values, 

and so my running time is inevitably going to 

have some dependence on k on the size of my output. 

I get a running time of order k+log n. The log n is 

the fixed part independent of output size 

and the order k comes from the size of the output.

Play video starting at :2:29 and follow transcript2:29

This thing happens a lot, 

especially in data structure queries, 

where the running time has these two components, 

one of which is sensitive to 

the size of the output that we're printing out. 

These are just a few examples of other types of 

parameters that you might often 

see in your running times.![[Screenshots/Screenshot 2025-08-25 at 2.43.20 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 2.44.29 pm.png]]