[MUSIC] 

The study of data structures goes hand in hand with the study of algorithms. 

And throughout this class, we're going to study data structures quite extensively, 

as this is very important for the design of efficient algorithms. 

At this point, we're just going to get the conversation started and 

talk about some basic ideas in data structures. 

Basic data structures and some basic techniques for analyzing data structures. 

We're going to focus our attention on a very important subclass of data 

structures, namely those for representing sequences, sequential data, and 

there are two very prominent and very important data structures in this space. 

Hopefully these are objects that look familiar to you if you've done 

a substantial amount of programming. 

That would be the array and the linked list, very simple data structures.

Play video starting at ::53 and follow transcript0:53

The array is just a contiguous block of memory holding a sequence of information. 

And you can easily index into the array in any given location and 

modify or retrieve the i’th element in constant time. 

The linked list consists of a bunch of individually allocated blocks of memory, 

kind of strewn haphazardly through memory. 

Where each block is a very lightweight structure holding an actual element of 

data, some sort of payload. 

And then also having a pointer to the next block in the sequence. 

So starting from the head element, 

you can walk down the linked list until you reach the element that you care about. 

Sometimes you have a doubly linked list where every element points to the next 

element and also the previous element, allowing you to walk in both directions.

Play video starting at :1:39 and follow transcript1:39

Arrays and linked lists are very easy to code up from scratch. 

In most languages they have built-in versions of array-like data types and 

linked list-like data types. 

So these are very easy data structures to conjure up and 

to use in most programming languages. 

The examples on my slides here are written in C++ but 

the code is similarly easy in most other languages. 

Now, if we look at the pros and cons of arrays versus linked lists, 

we see that some of them are good at certain operations, 

some of them are not so adept at other operations. 

Trade offs like this are extremely common in the area of data structures. 

Anytime you want to implement a given abstract data type, 

like a sequence or a set or a priority queue, there are often many choices for 

how underneath the hood you could actually represent that data structure, 

like an array or a linked list or something else.

Play video starting at :2:33 and follow transcript2:33

And there are usually a lot of pros and cons in terms of running time for 

each of those choices. 

So it's important to understand the strengths and 

the weaknesses of all of these different options for implementing data structures. 

For example, with the array we've already mentioned, it's very 

easy to index into the array and retrieve or modify a value in just constant time. 

The Achilles heel of the array is that it is not adept at inserts and 

deletes in the middle of the sequence. 

Because of its contiguous nature, 

if you were to insert an element in the middle of the array, 

you'd have to scoot over a large chunk of elements to make room for the new element. 

And that would take you linear time. Theta N time in the worst case.

Play video starting at :3:14 and follow transcript3:14

Similarly, if you delete an element, you'd have to shift back 

a block of elements to kind of plug the gap left by the deleted element. 

Now, this issue doesn't exist if you're doing inserts and 

deletes at the endpoints of the array. 

And we'll see in a couple of slides there are several data structures, 

like stacks and queues, that are essentially nothing more than 

sequences where you interact only at the ends of the sequence. 

And those can be implemented quite efficiently. 

Although if you're using an array for this, you do need to be cognizant 

of the issue that most of the time arrays live inside 

blocks of memory that we've allocated from the system, and you want to make sure 

that you're not going to wander off the end of that block of memory, 

because then you're accessing memory that you don't own. 

So maybe, as a quick aside, we should probably come to an understanding of 

how much time we expect it to take to actually allocate a block of memory and 

memory allocation. 

It can be a bit complicated in a real system. I think. 

for simplicity's sake, let's maybe just make a simplifying assumption that 

allocating a block of memory of any size will just take us constant time.

Play video starting at :4:21 and follow transcript4:21

That's perhaps not fully realistic, but it's not too far off. 

So a reasonable assumption perhaps. 

Of course, when you get a block of memory, it usually comes to you uninitialized, 

filled with garbage values. 

And so you would possibly need to also consider the running time needed to 

initialize your memory after allocating it. 

And that could be substantially more than constant time. 

So moving on to the linked list, the tradeoffs here are kind of 

complementary to what they are with the array. 

So here the slow operation is actually accessing the i’th element.

Play video starting at :4:53 and follow transcript4:53

Because to reach the i’th element, you have to start at the head element and 

painstakingly walk down the linked list until you reach the element that 

you care about. 

That takes linear time in the worst case, however, once you have reached the element 

or the location list, that you care about, you can very easily, in constant time now, 

splice in a newly allocated element, or you can delete an element. 

So surgery on linked lists is very efficient as long as you have 

kind of located the location in the list that you care about. 

So one other related issue on the subject of memory allocation and 

arrays is that it's very common to not know in advance how big your 

array needs to be to hold your input. 

Like if you're reading in elements from an input file, 

adding them one by one to the end of an array, 

you sometimes don't know in advance how many elements are going to be in the file, 

so you don't know how big to allocate your memory buffer to hold the array. 

A common way of dealing with this is by periodically upsizing 

the array whenever its corresponding memory buffer fills up. 

So if the memory buffer fills up, you allocate a new memory buffer of usually, 

say, twice the size of the original, 

and you copy all the contents from the old buffer into the new buffer.

Play video starting at :6:9 and follow transcript6:09

And that gives you some breathing room so 

that you can then continue extending your array. 

And then if that memory buffer fills up, 

you again allocate a memory buffer that's twice the size of that and 

copy the contents into the new memory buffer, and so on. 

It's common to use a factor of 2 for expansion, any constant factor will work. 

These data structures, these expanding arrays are very common in many languages. 

In C++, it would be called a vector as a built in data type. 

So the interesting thing here is that if you look at a sequence of operations, 

most operations are very fast. 

You're just dropping a new element into the end of the array and that's it.

Play video starting at :6:45 and follow transcript6:45

But occasionally you have a slow operation, 

the ones that cause an upscaling of the underlying memory buffer. 

Because you have to, in order n time, 

copy the n elements of your existing array into the new memory buffer. 

And so this sort of non-uniform performance profile is actually really 

common in a lot of data structures. 

You have mostly fast operations, but occasionally a slow operation due to 

the need to pause and maybe do some garbage collection or 

reorganize the internal state of your data structure. 

And so how do we actually describe the running time of these sorts 

of operations that mostly run quickly but occasionally run slowly? 

It seems like worst case analysis doesn't really work well here. 

You could certainly say that the insert operation takes order n worst case time.

Play video starting at :7:37 and follow transcript7:37

But that doesn't really faithfully recount how efficient this data 

structure really is. 

It might scare somebody away from using the data structure because it makes 

it sound much worse than it actually is. 

Most operations are actually much faster than that. 

So in this sort of setting, it's common to use what we call amortized analysis, 

where we don't look so much at individual isolated operations. 

But we average the running time of an operation over a sequence of operations, 

where the expensive operations kind of come out in 

the wash when averaged together with a lot of really fast operations. 

So in this case, in the case of a vector like this, it turns out that the running 

time of adding a new element to the end is just constant amortized. 

So what that means mathematically is if you start from an empty structure and 

you do any sequence of k operations, the total running time is order k.

Play video starting at :8:29 and follow transcript8:29

That's exactly what you would have gotten if every operation took just constant 

time, full stop. 

But here, individual operations are allowed to take more than constant 

time just over the sequence of operations. 

It still adds up to at most order k in the worst case. 

So this is still a worst case, 

running time just averaged over a sequence of operations. 

We'll actually study amortization in more detail later in the course. 

There are several methods for doing amortized analysis that we don't want to 

get into in detail here, but maybe, let me just take a minute to try and 

convince you that this particular case does indeed give you a constant amortized 

running time just for the exact case here of an expanding array or a vector. 

And to do that, all you really need to do is focus on the amount of extra work 

that's involved with the upscaling operations.

Play video starting at :9:20 and follow transcript9:20

Every operation here normally just takes constant time, which is fine. 

All we have to do is kind of add up the amount of extra work that we're doing with 

the upscalings and show that over a sequence of k operations starting with 

an empty structure, that that will add up to at most order k. 

And the nature of that extra work is kind of well structured. 

It's basically kind of a geometric series where we're adding up powers of two. 

For example, when we scale up from a buffer of size four to a buffer of size eight, 

that takes four extra units of work, because you're copying over those 

four elements from the smaller buffer into the larger buffer. 

And so we basically just need to sum up 1 + 2 + 4 + 8 

dot dot dot until we reach k, the size of the final. 

If you're doing k operations, just to make things a bit concrete, suppose k is 100.

Play video starting at :10:8 and follow transcript10:08

So I do 100 inserts. 

That means the final buffer size is going to end up, I think, is 128. 

That would be the power of two just bigger than 100. 

And that would mean that the amount of work we spend on upsizing is this series 

1 + 2 + 4, all the way up to 64. 

Because the last up size operation, we did, 

we would have copied 64 elements into that larger buffer of size 128. 

So what is this sum 1 + 2 + 4, all the way up to 64? 

Conveniently, if you add up a series of powers of two like this, 

it always adds up to one less than the next largest power of two.

Play video starting at :10:48 and follow transcript10:48

So 127 in this case. 

There are a couple ways that you could see this, actually, 

maybe one nice way is if you're a fan of binary numbers. 

If you think about the binary number 1 1 1 1 1 1, however many ones that is, 

that binary number represents the sum 1 + 2 + 4 + 8 + 16, up to 64, 

because there's a one in each of those digit positions. 

And now what happens if you add one to that number? 

Well, that gives you the binary number 1 0 0 0, 

followed by a bunch of zeros, where now the one bit is in the 128’s position. 

And so this gives you a nice proof by binary number addition 

that this sum of 1 up to 64 gives you 1 less than 128. 

So in general, this sum is going to end up being at most two k, because the 127 

number here, that's at most just, it's the power of two, basically just above k.

Play video starting at :11:43 and follow transcript11:43

So the amount of extra work that we do here is, in general, 

going to be upper bounded by two k, which is on the order of k. 

And now we're done because the total work we spend is order k for 

all the constant time operations that we do, 

and then order k for all the extra work that we do as well. 

Over the sequence of operations, we spend a total of order k time, so we're all set. 

So this is amortized analysis. 

We'll talk about it in much more detail later on, but 

it's good to have in your vocabulary. 

Okay, moving on. 

Let's revisit really briefly the array and the linked list, 

because we have some frowny faces on our slide.

Play video starting at :12:21 and follow transcript12:21

These correspond to operations that are weak spots of these data structures. 

They take linear time in the worst case. 

That can be a really big impediment if N is a very large number. 

If you're, say, doing a bunch of inserts in the middle of a sequence, 

you might not want to use an array because it's very slow with that. 

So I wanted to give you guys a glimpse at ways that people had tried to basically 

improve the array or the linked list to get rid of these weak spots, 

to build fancier data structures that kind of balance out the running 

times of all these operations more effectively. 

We'll talk about these in more detail later in the semester, so 

later in the course. 

So I won't go into a huge amount of detail, but I think it's worth just 

looking at these ideas just to kind of get a sense of what people have tried to do, 

what approaches they've used to improve upon arrays and linked lists.

Play video starting at :13:15 and follow transcript13:15

So with arrays to start with, 

you can do something that maybe is akin to what you would find in a library. 

So at your local library, you'll notice they sometimes leave gaps on the shelves, 

so that if you add a new book, 

you don't have to move too many books over to accommodate the new addition. 

You can do the same thing with an array. 

You can intentionally leave periodic blank spots, gaps, so 

that now if I insert a new element, I don't have to move over too many things, 

I just have to move things over until I hit the next gap. 

And that could be more efficient. 

Of course, that also requires the addition of a lot more complex machinery to 

figure out even how to index into the i’th element, 

because the gaps shouldn't count in that calculation. 

And you also need some complicated machinery built on top of this structure 

to manage the gaps.

Play video starting at :14:1 and follow transcript14:01

You don't want to have too few or too many of them. 

You want to make sure that they're distributed somewhat uniformly. 

This is actually a somewhat complicated data structure. 

I haven't actually seen it used that often in practice, but 

I think it's just nice to kind of see the idea behind it. 

At the end of the day, you can actually build something of this sort that takes 

log N time to index into the i’th element and modifier or retrieve it. 

And it takes log squared of N amortized time to do inserts or 

deletes anywhere in the sequence. 

And that's much better than the order N that you would have gotten 

from the original array.

Play video starting at :14:35 and follow transcript14:35

I guess, one quick note about what does log squared of n mean, 

in case you haven't seen that notation before? 

So log squared of n is log of n, 

quantity squared, log of n times log of n. 

This is actually different from if you take log of n squared, 

that's what that means, is log of the quantity n squared. 

And by properties of logs, that's the same thing. 

You can move the two up front. 

That's the same thing as saying just two log n, which is on the order of log n. 

So these are two very different things, log squared of N and log of N squared.

Play video starting at :15:12 and follow transcript15:12

Just good to kind of know the notation here. 

How do we fix a linked list and make it run more efficiently? 

Well, the downside of a linked list is scanning all the way down the linked list 

to find the element that you care about. 

So we can fix this with an idea called a skip list that builds on top of our linked 

list, basically an express lane. 

So on top of our original linked list, we build several sparser and sparser copies 

of that list, each one having roughly half the elements of the list below it. 

And these kind of express lanes let you walk down the list much faster. 

And if you implement this thing properly, you can get all major operations, 

inserts, modifies, whatnot, to run in log n expected time.

Play video starting at :15:56 and follow transcript15:56

There's some very clever use of randomization. 

Built into the standard implementation of a skip list. 

We will talk about this later on, so I won't give you the details now. 

But the picture kind of hints at why this should be effective at 

addressing the weak spot of a linked list. 

There are also quite a few other related data structures to a skip list, 

notably binary search trees and B-trees, 

which are kind of like binary search trees with a higher branching factor. 

We'll talk a lot about those later in the semester because those are very 

prominent and very powerful data structures. 

They can also represent a sequence where all major 

operations take logarithmic running times.

Play video starting at :16:37 and follow transcript16:37

So at the end of the day, it may end up being that the array or the linked list 

are not the best choices for representing sequential data, but rather something like 

a skip list, a binary search tree, or a b-tree could end up being a better choice. 

Okay, let's round out our discussion of sequential data structures by going 

back to the structures that only interact with a sequence at its endpoints. 

And one prominent example here is the queue where you're inserting elements on 

one side of a sequence and you're removing them from the other side of the sequence. 

The first element to be inserted is the first element to leave the structure. 

So it's a first-in, first-out, or FIFO data structure. 

Very easy to implement, especially in using a cool idea called a circular array, 

which is an array that kind of logically wraps around within the memory space 

you've allocated for it. 

So here, you kind of keep track of two indices or 

pointers to the front and the back of the array.

Play video starting at :17:34 and follow transcript17:34

And if you're inserting a new element at the back of the array, 

then you just increment the back pointer. 

If the back pointer runs off the end of your memory buffer, 

it just cycles back around to the beginning of the memory buffer. 

Same thing for removing the front element of the queue, 

the front pointer increments. 

And then if it increments off the end of the memory buffer, 

it cycles back around to the beginning. 

So the contents of your queue here just kind of snakes around and wraps around 

within the space of the memory buffer that you've allocated for it. 

It's kind of a nice idea. 

You don't have to use a circular array to represent only queues.

Play video starting at :18:10 and follow transcript18:10

They can represent other sorts of array-like structures if necessary. 

So what would be maybe an example of where you 

would find a queue in a real computing system? 

So maybe one nice example is on the Unix command line, 

if you chain together a bunch of commands using pipes. 

If you haven't seen this notation before, what that means is you take the output of 

one program and you feed it into the input of the next program, 

whose output then gets fed into the program after that. 

So you can actually compose programs together, these simple programs together, 

and get some very elaborate functionality as a result. 

In this case, cat will print out the contents of a file. 

We feed the results to grep, 

which then prints out only the lines that match the word algorithm.

Play video starting at :18:55 and follow transcript18:55

And then we feed that into word count dash l, which just counts the lines in the output. 

So this aggregate command would just count how many lines in file 

match the string algorithm. 

Where is a queue in all of this? 

Well, if you run this command, what happens is all these three programs, cat, 

grep and wc, they get launched in parallel. 

That is to say, our operating system is going to be alternating in quick 

succession between running a little bit of cat, a little bit of grep, 

a little bit of wc, and so on. 

As cat is running, it's producing output. 

And where does that output go?

Play video starting at :19:31 and follow transcript19:31

It's temporarily stored in a queue, it gets pushed into a queue. 

And then when we have a context switch and grep starts running, 

it's going to then consume elements out of that queue that cat was populating. 

So each of these little pipes here might represent an internal queue in our 

system that is a temporary buffer for holding the output of one program 

while it's waiting for the next program to switch in. 

So queues are very easy to implement from scratch. 

But most languages also have built-in implementations of queues as well. 

A relative of the queue is the stack. 

Here, we interact with the same end of a sequence.

Play video starting at :20:7 and follow transcript20:07

We push things onto the top of the stack, and 

we also pop things from the top of the stack. 

Stacks, similarly, extremely easy to implement yourself in code, or 

they're also supplied as built-in objects in most programming environments. 

These are last in, first out, instead of first in, first out, and 

they're used in a wide variety of situations. 

Maybe one prominent example is if program is executing and 

you call a function, then you need to put on hold the current function, 

kind of save your state of execution. 

So when the function you called terminates, you can then resume executing 

from the point you left off in the current function. 

And we use a system, there's a stack in the system that basically does that. 

It kind of holds the state of all the currently pending function calls.

Play video starting at :20:53 and follow transcript20:53

So anytime you call a function, this adds a new frame on top of our stack. 

Anytime you terminate from a function, it unstacks that frame and 

resumes the execution from the frame below it. 

In this particular example, just to kind of give you one concrete example. 

This prints out a linked list backwards, 

which is kind of the unnatural direction for printing a linked list, 

because the pointers usually go forwards in a linked list instead of backwards. 

But you can easily print a linked list backwards with a recursive function. 

All it does is step one, print everything but the first element recursively. 

So head points to next is the second element of the linked list, 

which is the head of everything but the first element.

Play video starting at :21:34 and follow transcript21:34

So we print everything but the first element recursively. 

And then the very last thing we do is we print the head element. 

And if you think about this computation, kind of trace through it, 

you'll see that it basically is stacking up a bunch of recursive function calls 

corresponding to the elements of our linked list. 

And then when each of those calls finally terminates and unstacks, 

it's going to print out on the way down that series of unstackings 

that's going to print out the elements in reverse order. 

I guess we could have just used a normal stack for essentially the same process. 

We could have traversed our linked list and pushed everything into a stack and 

then popped everything off of that stack. 

And the elements will come out of the stack in reverse order from 

the order that they were pushed.

Play video starting at :22:17 and follow transcript22:17

So that would be another way of looking at essentially the same process, 

maybe more from an iterative perspective. 

So one final idea that's important not only in data structures, but 

in algorithms and in computing in general, is abstraction. 

And there's a lot of benefit for thinking abstractly and for 

abstraction in software development. 

Suppose, for example, I'll just kind of highlight this with an example, 

that you want to write a computer program or 

design an algorithm that uses a double-ended queue. 

This is 

yet another sequential data structure that you interact with its endpoints. 

A double-ended queue is a structure where you do inserts and deletes at both ends. 

It's kind of a hybrid between a queue and a stack.

Play video starting at :23: and follow transcript23:00

In fact, I've heard it amusingly called a quack in some applications, 

kind of a mixture of a queue and a stack. 

But the technical term for it is a double-ended queue, or sometimes a deque. 

And if I'm actually writing an algorithm that uses a double-ended queue, 

I would like to think about the deque at a high level, as it's just a data structure 

that supports a certain set of operations, pushing new elements onto either 

the front or the back, or popping elements off of the front or the back. 

And I'd like to be able to interact with it in code. 

In simple terms, just conjure up a deque, tell it to push something on the front or 

the back, tell it to pop something from the front or the back. 

At this point, I really don't want to trouble myself by thinking about 

all the low level details that went into implementing that deque. 

So I'm kind of thinking about things at a certain level of abstraction.

Play video starting at :23:52 and follow transcript23:52

Of course, underneath the hood, there is somewhere an implementation of 

that deque that has a substantial amount of detail involved. 

Maybe it uses a circular array, maybe it uses a double linked list. 

There are lots of ways I could have implemented the deque that when I'm 

actually using the deque, I don't worry about that. 

It helps relieve the cognitive burden of building a complex system, 

because I only kind of think about things at one level of detail at a time. 

I only think about one thing at a time, and 

I don't think about all the things at once, that would be overwhelming. 

This also lets you build very complicated systems in a bottom up fashion. 

I build a deque by implementing all of its operations, and then I basically package 

that up into a black box, give it a nice well defined interface.

Play video starting at :24:34 and follow transcript24:34

And then I can use that at a high level to build more substantial, 

more complex algorithms without worrying about the details that went into that 

lower level implementation. 

And then I can take that algorithm and package that up into a black box, give it 

a nice interface, and then build an even more complicated algorithm out of that. 

This lets me manage complexity, kind of thinking in abstract terms at the right 

level of detail, always without thinking about everything at once. 

It's also useful for software engineering to enforce these abstraction barriers. 

Later on, I could come in and change out the underlying implementation of my deque. 

And hopefully, if I do that the right way, in code, 

I won't actually have to change any of the implementation that uses the deque, 

because it adheres to a standard interface. 

As long as the interface doesn't change, everything will still work properly.

Play video starting at :25:23 and follow transcript25:23

So abstraction is useful for a wide range of reasons, 

both kind of in theory and in practice. 

These are a couple of simple and common ideas in the world of data structures. 

We will see many more over the next few modules, but 

good to at least know some of the terminology and the basics. 

[MUSIC]![[Screenshots/Screenshot 2025-08-25 at 6.03.40 pm.png]]

**==Written In C++==**
![[Screenshots/Screenshot 2025-08-25 at 6.05.20 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 6.06.26 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 6.07.36 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 6.10.43 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 6.12.02 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 6.13.05 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 6.15.33 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 6.16.37 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 6.16.53 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 6.35.35 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 6.38.05 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 6.40.00 pm.png]]