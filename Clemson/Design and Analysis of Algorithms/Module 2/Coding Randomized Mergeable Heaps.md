![[Wm7n5t8JQXGVzT2MNk8Lsw_f9714148d1a24f46b4f881987e7a42f1_Coding-Randomized-Mergeable-Heaps (1).pdf]]
[MUSIC] 

For this module's coding discussion, I thought it would be appropriate to 

talk about an elegant randomized data structure, since we haven't yet 

spoken much about data structures in this module. 

So, be prepared to be introduced to the randomly mergeable binary heap— 

one of my favorite data structures, actually. 

It's an example of a priority queue. 

So, priority queues are a very broad class of data structures used in many different 

algorithmic applications. 

They're related to FIFO queues, which we introduced back in the first module. 

So, remember that a FIFO queue elements enter the queue and 

exit the queue in the same order, 

so these are kind of like maybe a group of people waiting in line at a busy ticket 

counter. 

In contrast, a priority queue would maybe be more like people waiting in a hospital 

emergency room.

Play video starting at ::51 and follow transcript0:51

So people enter, but they exit in order of priority. 

So the most important, 

the most pressing case is the next one to be extracted from the priority queue. 

So, every priority queue basically has to support two main operations: 

insert an element and remove the element with the highest priority. 

And, that can be defined either as the minimum or the maximum, 

depending on your convention. 

I think, more common, I've seen the minimum used as the highest priority element, 

so that's the convention I'm going to adopt here. 

But, we just as easily could have called the maximum the highest priority element. 

So, we have an insert operation and a remove minimum operation.

Play video starting at :1:29 and follow transcript1:29

Those are our two fundamental operations, 

but many priority queues also support some ancillary operations, 

like the ability to delete an arbitrary element or 

to adjust the priority of an element sitting in the structure. 

And, these are used— 

It depends on the application—what operations are necessary to be 

implemented. 

There are a lot of different applications of priority queues. 

Just to give a few examples, you can use them in scheduling applications. 

For example, you can maintain a set of tasks in a priority queue, so 

you can always reach in and pull out the most important task and work on that next. 

Priority queues and sorting go hand in hand, because if you have a priority 

queue, then you can sort. You just insert your elements into the priority queue and 

they will come out in sorted order.

Play video starting at :2:14 and follow transcript2:14

In fact, maybe that's the best example of what we can try coding up today. 

We'll build a priority queue and we'll use it to sort. 

That'll be a nice, straightforward application of priority queues. 

Finally, there are a lot of algorithms that really rely 

heavily on the performance of priority queues for the running time. 

So Dijkstra's shortest path algorithm is maybe a good example. 

If you look at the running time of Dijkstra's algorithm, it basically just 

boils down to the efficiency of the priority queue that it's using. 

So, implementing fast priority queues has a lot of 

important application in a wide range of different algorithms.

Play video starting at :2:51 and follow transcript2:51

So, if you do want to implement a priority queue, there are many, 

many ways to do this. 

You could start by thinking, well, I could implement a priority queue from something 

really simple, like just an array, or a linked list, or 

an array that I keep in sorted order, or a linked list that I keep in sorted order. 

And, you can certainly do that, 

but, if you do, then your priority queue is going to have a weak spot. 

One of these two fundamental operations is going to have a worst case running time of 

order n, which is not so great. 

And, in order to get the running times down to something more reasonable, 

you have to use a little bit more sophistication. 

So, the go to data structure that everyone knows about for 

priority queues is called a binary heap. 

It's a very simple, lightweight data structure.

Play video starting at :3:35 and follow transcript3:35

You learned about it in just about any undergraduate data structures class, and 

we'll talk about it ourselves, maybe about two modules from now. 

It implements both of these operations in just logarithmic time, so 

it kind of balances the cost of those two operations. 

That's about as fast as you can hope for for these two operations, 

because, if your data structure is comparison-based, 

then at least one of these operations has to run in log n time. 

Otherwise, you would violate the lower bound 

on sorting in the comparison-based model. 

Remember that it must take you at least n log n time to sort n elements in 

the comparison-based model. 

And you can sort with the priority queue with n inserts followed by n remove-mins. 

And so, whatever your running time is for insert and remove-min, 

the cost of doing n inserts and n remove-mins, that should be at least n log 

n. Otherwise, you would aggravate the lower bound on comparison-based sorting.

Play video starting at :4:29 and follow transcript4:29

So, in today's discussion, we're not going to talk about the binary heap. 

We're going to talk about a relative of the binary heap called the randomly 

mergeable binary heap or a randomized mergeable binary heap. 

It's also a very simple and elegant data structure, and it's appropriate for 

our discussion today because it uses randomization. 

It's going to achieve the same efficiency as the binary heap just in expectation— 

so log n in expectation running times for both insert and remove-min. 

Very simple data structure. 

It consists of nothing more than a heap ordered binary tree. 

So, it's a binary tree. It's a bunch of individually allocated nodes in memory, 

each of which has a pointer to its left child and a pointer to its right child.

Play video starting at :5:12 and follow transcript5:12

One or both of those could be null, if you don't have a left or a right child. 

And, the tree is going to satisfy the so-called heap property. 

It's going to be heap ordered. 

This is a vertical ordering property that you often see in data structures, 

particularly in data structures for priority queues. 

What the heap property means is that, if you look at any element, 

the parent is always less than or equal to that element. 

So, if you walk down the tree, the elements get bigger. 

If you walk up the tree, the elements get smaller.

Play video starting at :5:41 and follow transcript5:41

And, specifically, that puts the minimum element in the entire tree at the root of 

the tree in an obvious place. 

That's why this is such a common property in priority queues. Because, with 

the priority queue, it's very convenient to know where the minimum element is, and 

it's sitting right there at the root. 

So that's our structure. 

In terms of implementing operations on the structure, those are going to boil 

down to being able to implement kind of a meta operation called merge, 

which just takes two of these structures and merges them into one. 

It turns out that, if we can do merge efficiently, 

we'll be able to implement all of the major operations—insert, remove-min, and 

all of the others—also very efficiently. 

So, we'll get to that in just a second, 

but maybe it's a good time to pause and start actually writing a little bit of 

code just to implement some of what we've talked about so far.

Play video starting at :6:33 and follow transcript6:33

And then, we can talk about the merge operation and 

how we use merge to implement the rest of our operations. 

Okay, so if we fire up our usual text editor emacs, 

I'll make a file maybe called pq.cpp. 

And so, let's start writing some code. 

I know I'm going to be doing some stream input output, so I'll include <iostream>. 

I will adopt the standard namespace. 

And now, I need to read in my input. 

Just for simplicity, 

maybe I'll use the same input file from last module.

Play video starting at :7:10 and follow transcript7:10

So, input10.txt is just 10 integers. 

Let's see if we can sort that file. 

So, maybe I will just read in a bunch of integers. 

So, as long as I can read in an input from standard input, 

I will insert x into a priority queue—into a pq, 

and then, afterwards, I'm going to call remove-min n times to remove the elements 

from that priority queue and print them out in sorted order, effectively. 

So then, I'm going to remove elements and print them. 

So that's kind of the overall structure of main, 

and then, I guess, I can also start coding up the structure of my tree. 

My tree consists of a bunch of individual nodes, 

so I can go ahead and define the structure that those nodes are based on.

Play video starting at :8: and follow transcript8:00

It's going to have an integer key sitting in each node, and 

it's going to have a pointer to its left child and a pointer to its right child. 

And, maybe, I'll make those default to null, 

so, if I allocate a new node, then, just by default, its left and 

right children are going to be null. 

Okay. So, so far, I've kind of started building out the skeleton 

of what I'm going to ultimately add on to do merging and other operations, 

so let's talk about those other operations now. 

Okay, so all you need is merge, right? 

—the lesser known hit, Beatles song. 

It turns out that, if you can merge things quickly, you can do anything. 

So, suppose we have the ability to do a merge in log n time.

Play video starting at :8:47 and follow transcript8:47

That means we can implement every other major operation on this priority queue in 

log n time. 

So, to insert a new element, for example, 

all you do is you merge with a new one element tree containing that new element. 

Pretty easy. 

What about removing the minimum? 

Well, if you take out the minimum, which is sitting at the root, then now you have 

kind of— Your tree kind of falls apart into your left subtree and your right 

subtree, but those are themselves valid heap ordered binary trees. 

And so, if we merge those two together, that puts them back together into one 

valid tree absent the root element, which you have now removed. 

So, we've implemented insert and remove-min.

Play video starting at :9:22 and follow transcript9:22

To delete an element, we do something similar. 

We just replace it with what you get when you merge its two child subtrees together, 

and then, if you want to update the value of an element, 

you can just delete it and reinsert it with a new key. 

So, very easy to implement all of our major operations, assuming we 

have a merge operation. 

So now, I can go back to my code and keep making some progress here. 

I can assume I have a merge operation and 

write all of the other operations in terms of that merge operation. 

So, what is the merge operation going to look like? 

It'll return a pointer to the root of the merged tree, 

and I guess it'll take two pointers to the roots of my two trees— Or, 

sometimes, we call those trees heaps, if they're heap ordered.

Play video starting at :10:8 and follow transcript10:08

So, h1 is going to be a pointer to the root of my first heap, and 

h2 is going to be a pointer to the root of my second heap. 

And so, here I'll have to do some logic and 

return the pointer that represents the root of the merged tree. 

But, assuming we have written that function, now I just need to write 

a function that inserts and a function that does remove-min. 

So, what is insert going to do? 

I guess insert— I can pass in a pointer to the root of my heap and 

the value that I'd like to insert. 

And I'm going to return a pointer to the root of the heap, post insert. 

So, I'm going to do the insert and return a pointer to the 

root of the resulting heap.

Play video starting at :10:46 and follow transcript10:46

And so, the way I could use this in my input reading routine is I can 

create a heap that initially is just null—so it's an empty heap. 

And then, for every value that I read in, 

I can just say h is equal to what I get when I insert into h the value x. 

Okay, so that's going to insert x into h, 

return a pointer that is now the new root of my heap, 

because the root could possibly change as a result of inserting something new. 

Okay, how do I insert? 

Well, I guess I merge with a new one element heap, 

so I need to create a one element heap. 

So, I'll create a new node. 

So, n is going to be a pointer to a newly allocated node, and 

n's key is going to be x— the value that I'm inserting.

Play video starting at :11:32 and follow transcript11:32

So, n is now a pointer to my new one element heap. 

Its left and right children are null. Its key is x. 

And, all I need to do is return what I get when I merge that with h. 

So, return merge of h and n. And, that's insert. 

Okay, what about remove-min?

Play video starting at :11:49 and follow transcript11:49

How do I implement that? 

So, that'll have a similar structure. 

Remove the minimum. 

I'm going to pass in a pointer to the root of one of these heaps, and 

this will give me back a pointer to the root of the resulting heap post remove-min. 

So, the minimum will now be gone, and I'll get back a pointer to 

the resulting root of the heap, after I've thrown out the root. 

So, what can I do here? 

So, the results that I'm going to return is going to be the result 

of just merging together h's left and h's right subtree.

Play video starting at :12:25 and follow transcript12:25

So, I'll just call merge to put those two things together, 

and that's the result that I'm gonna return, at the end. 

So return result. 

But, before I do that, I'm going to delete the root node of h, 

and I have to do things kind of in this order. 

I couldn't have deleted the root node and then merged its left and 

right children together because this would be accessing memory 

that I've technically just deleted and handed back to the operating system. 

So, the order of operations here is a little bit important, I guess. 

So, I merge my left and right subtrees together. 

That's the final result I'm going to return.

Play video starting at :13: and follow transcript13:00

I delete the root and then just return that result. 

—So, very, very simple implementations. All I need to do is write merge. 

So, let's finally talk about the merge operation. 

Okay, so there are actually a couple ways we can think about merging, but maybe 

the simplest is just using a kind of a recursive viewpoint on how merging works. 

So, if I have two heaps that I'd like to merge together, heap h1 and 

heap h2. Let's assume h1 has the smaller root, perhaps. 

And, if I want to merge these together, then h1's root, being the smaller one, 

has to become the root of the merged together tree.

Play video starting at :13:40 and follow transcript13:40

So the root of the merged tree is decided. That's h1. 

And then, to finish things off, I'm just going to kind of think 

about recursively merging h2 with either my left or right subtree. 

And that's it. 

And then, just let recursion kind of sort out— 

That's going to call merge; that's going to call merge. And, it's just slowly 

going to fold those two trees together until they're merged. 

Eventually, I'll hit a base case where I'm merging something with nothing, and 

the answer is going to be the something, I guess.

Play video starting at :14:6 and follow transcript14:06

So, that's actually a very simple viewpoint on merging. 

I guess, in this process, though, I have a choice to make. 

At every step of the merge, 

I'll have a choice between merging h2 with my left child or h2 with my right child. 

And, how do I choose between those two things? 

That might actually have performance implications? 

These trees don't have to be very balanced at all, 

like h1 could be one long stringy path. 

And, if I'm unlucky and I always choose to merge in the direction that keeps me 

walking down that path, the merge can take a very long time. And so, 

I'd like to avoid that sort of potential worst case behavior.

Play video starting at :14:45 and follow transcript14:45

And so, here's where the randomization comes in. 

I'm going to merge in the simplest possible way, according to 

the result of a coin flip. 

I flip a coin and, if I see heads, I merge left; if I see tails, I merge right. 

And then, I get to the next step of the merge, 

and, again, I flip another coin. And, heads, I go left; tails, I go right. 

And so, each step of the merge process— The direction that I go, 

is dictated by a bunch of coin flips. 

—Very, very straightforward. 

And, it turns out there's a very simple argument for 

why this merge operation should run in logarithmic time in expectation.

Play video starting at :15:17 and follow transcript15:17

It's based on our familiar randomized reduction lemma. 

So, actually, we can talk about that right now. 

If you do one step of the merge— 

So, I merge h2 with either your left or your right child, and 

I do that according to a coin flip. Then, with probability one half, 

I'm lucky enough to pick the smaller side. 

So, I merge with the smaller of my two children. 

—Well, so maybe that's my left child. 

That would have size, at most, half of the original size of h1. 

So, if you merge with your smaller subtree, the smaller subtree has, at most, 

half of the size— half the mass of the original tree.

Play video starting at :15:54 and follow transcript15:54

And so, that means that, if you look at the merge process, 

one of the two arguments of that merge process is effectively being reduced 

to, at most, half of its current size, with probability of at least one half. 

And, that's enough to satisfy the conditions of the randomized 

reduction lemma, 

so, therefore, the merging process runs in logarithmic time, 

with expectation. And, later on in 

the module, we'll also see that it also can hold with high probability. Which is nice. 

Let's go ahead and code this up, and then maybe just— 

We have a few more comments, about the merging process itself, but 

let's see if we can finish up our code, at least. 

So far, the coding part of this discussion doesn't look like it's been too bad. 

And, hopefully, the merge operation will similarly be relatively straightforward.

Play video starting at :16:37 and follow transcript16:37

So, like any good recursive function, 

we probably want to start out with a few base cases here. 

So for example, if h1 is null; I'm merging h2 with nothing, 

I should probably just return h2 in that case. 

And similarly, if h2 is null; I'm merging h1 with nothing, and 

I probably just return h1. 

So, those are probably my base cases of merging something with nothing. 

If I make it past both of those two base cases, then now, I have two somethings. 

H1 and h2 both have something sitting at their roots, and so 

I can look at those roots.— 

I guess, I was assuming, actually, that h1 had the smaller root. 

So, assume h1 has the smaller root.

Play video starting at :17:18 and follow transcript17:18

If that's not the case, let's make it the case. 

So, if the key sitting at the root of h1 is bigger than the key 

sitting at the root of h2, then I'll just swap them. 

So, swap h1's key— Or swap h1 and h2. 

So, now, h1 is the heap with the smaller root, and so 

now I just have to flip a coin. 

So, maybe, I'll make a boolean variable heads 

that's just— What's a good way to flip a coin? 

I can take a random integer. Maybe mod two?

Play video starting at :17:49 and follow transcript17:49

That will give me a result that's either zero or 

one, kind of with 50 50 odds on each one. 

And, if I store that in a boolean, 

then heads is going to be true with 50% probability. 

So, if I had flipped heads, then I want to merge to the left. 

So, that means that h1's new left subtree is going to be the result 

of what you get when you merge that left subtree with h2. 

And otherwise, if you flip tails, then I guess h1's right subtree is going to be 

replaced by the result that you get when you merge it—h1's right subtree—with h2. 

Okay, so that's the recursion. 

At the end,I probably need to return something.

Play video starting at :18:33 and follow transcript18:33

I'm going to return, I guess, 

just h1 because that's the overall root of the merged tree. 

That's the root that had the smaller key in it. 

So, that's merge. 

Oh. I guess I need to remove the elements and print them here. 

I haven't done that yet, so 

I'll just do another while loop here. As long as h is not null 

—so as long as there are elements in my heap— 

I'm just going to print out the element at the root. That's the minimum.

Play video starting at :19:5 and follow transcript19:05

So, C out the contents of the root's key. 

So, print out the root. And then, I'm going to remove the root. 

So I'm going to say h is equal to remove_min(h). 

If I call the remove_min function, 

that'll get rid of the root and merge the two children sub trees back together and 

keep doing that. 

So, as long as there's still contents in the heap: 

print the root, remove the root; print the root, remove the root; and so on. 

So, hopefully, we've just written a sorting algorithm, 

if everything works the way we expect.

Play video starting at :19:38 and follow transcript19:38

So, if I compile this, pq.cpp. Okay. That's nice. We compiled okay. 

And then I can run this, and— Let's see, a.out. I can pipe in input10.txt, 

and, hopefully, we will see ten numbers in sorted order, as a result. 

And we do! Okay. Excellent.

Play video starting at :19:58 and follow transcript19:58

It might be interesting to see how fast this really is. 

I mean, presumably, if every operation is running in log n expected time, 

then this will sort in n log n expected time—the same as randomized quick sort or 

merge sort, for example. 

So, let's see— If I run this on a big input... 

Remember, with the last module, I made an input of size 1 million. So, 

I can run it on that input, 

but I probably don't want to print out the output here because the output is going 

to have a million numbers in it. 

So, maybe I'll redirect the output to /dev/null. 

So, just throw away the output and 

just this will give me a sense of how fast it runs.

Play video starting at :20:33 and follow transcript20:33

And, it runs pretty fast. 

So that does seem in line with an n log n algorithm. 

If it was quadratic or worse, we definitely would have noticed. 

So, we finished our coding. 

Maybe, just— 

I want to say just maybe another word or two about the merging process and 

how we can maybe think about the merging process in a slightly different way, 

just to get a little bit more insight into what's really happening there. 

So, it turns out that you can think about the merging process maybe from 

an iterative vantage point, as opposed to a recursive vantage point. 

The two are completely equivalent, 

but it's nice to be able to see the same process kind of two different ways.

Play video starting at :21:12 and follow transcript21:12

So, one way to think about merging is I can take the two heaps that I'm merging, 

and, in each heap, I find what's called a null path. 

It's basically a path that goes from the root all the way down to a null 

at the bottom of the heap. 

And, since I'm using randomized merging, 

the way I'm effectively finding these null paths is by coin flip. 

So, heads, I step to the left; tails, I step to the right. 

That's how these paths are actually going to be determined. 

But, if you look at the heap property, 

that guarantees that these null paths are basically sorted sequences, 

and I can just merge those two sorted sequences in much the same way that you 

merge any sorted sequences— like with merge sort, for example. 

And, by splicing together those two null paths, 

that gives you the resulting merged heap.

Play video starting at :21:58 and follow transcript21:58

So, basically, the merged heap is what you get when you kind of zip 

together those two null paths into one long null path. 

And, all of the other subtrees that are hanging off of those null paths, 

they're still hanging off of the resulting kind of combined null path. 

They're intact, they're not really changing those other subtrees. 

So, this is kind of what the merging process actually looks like in more of 

an end to end iterative fashion. 

Our recursive process is doing this. 

It just maybe doesn't look like it from the recursive vantage point. 

So, if I step through a few steps of the recursive process, 

maybe it does make more sense.

Play video starting at :22:33 and follow transcript22:33

So, the recursive process starts out by merging the two with the four, 

the two roots of h1 and h2. 

The two is smaller, so that becomes the root of the merged tree. 

And I flip a coin to figure out if I merge to the left or to the right. 

And I flipped heads, I guess, in this case, 

so I went to the left. 

And so, my next step of the recursive merging process is merging the five with 

the four. And, the four is smaller, 

so the four wins. That becomes the root of the resulting merged tree, 

and, again, I flip a coin to figure out, "Do I merge left or right?"

Play video starting at :23:3 and follow transcript23:03

And, I guess, I flipped tails in that case. 

So now, I'm merging the five with the six, and 

the five is smaller, so that wins and so on. 

So, this really is the same process that the recursive process would have also 

generated in terms of efficiency. 

We could have analyzed the efficiency of this directly and 

also concluded that the expected running time is on the order of log n. 

For example, look at these null paths. 

They're formed by random coin flips. 

And so, what is the expected length of such a null path?

Play video starting at :23:34 and follow transcript23:34

That's actually really easy to analyze 

because, if you start at the root of the tree and 

just walk randomly down the tree by coin flips, then, at every step of your walk, 

there's a one half chance that you step to the smaller of your two children, 

and, thereby, halve, effectively, your subtree size. So, 

that satisfies directly the conditions of the randomized reduction limit. 

Your subtree size is halving at each step with probability of one half. 

And so the length of the resulting null path that you 

step down is going to be on the order of log n in expectation. 

That's true for both of these null path, 

so, if you merge them together, the total time taken by the merge is nothing more 

than the sum of the lengths of the two null paths. 

And, if both of those are log n in expectation, 

then the entire merge takes log n time in expectation. 

So, just another kind of nice way to look at the same process.

Play video starting at :24:24 and follow transcript24:24

So, that's the randomized mergeable binary heap, pretty cool data structure. 

And, I guess we've written yet another sorting algorithm along the way. 

[MUSIC]!