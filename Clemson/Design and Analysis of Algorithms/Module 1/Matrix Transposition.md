[MUSIC] 

So far, everybody following this module 

is to be applauded for suffering 

through what is perhaps a somewhat heavier schedule of 

mini lectures, covering just fundamental basic concepts. 

I wanted to close 

the module with something maybe a bit more fun, 

and it also showcases how you can solve 

slightly more advanced problems even with 

the fundamentals that we've 

talked about so far in this module. 

We're going to go back to the example that 

we introduced at the very beginning of the module: 

This was "in place" matrix transposition. 

So, you have a matrix that is 

represented in memory in row major format 

row 1 followed by row 2, and so on. 

And, you would like to rearrange the contents of 

that memory in place without using 

a substantial amount of extra space so that, now, 

the matrix is represented in column major format. 

There are a couple of ways we could consider doing this. 

And, our discussion today will be 

an interesting algorithm that is not maybe obvious 

—and its analysis is certainly not obvious— 

but we'll still be able to analyze it fairly in 

simple terms, using the techniques 

we've talked about so far in this module.

Play video starting at :1:17 and follow transcript1:17

As a warm up, let's look at a related problem. 

We'll see how it's related in a second. 

I call this the domination radius problem. 

Here, you're given as input an array of, maybe 

call them heights of individuals standing in a row, 

and we'd like to compute for each individual 

its domination radius. 

That is you look to 

the left until you're blocked by a taller individual, 

and then you look to the right until 

you're blocked by a taller individual, 

and you take the smaller of those two distances. 

That's your domination radius. 

This is basically the largest radius 

around you within which you are the tallest individual.

Play video starting at :1:55 and follow transcript1:55

If you want maybe some prototypical, 

real world application 

where this might be relevant, 

maybe I'm analyzing time series data— 

maybe stock market prices on various days. 

For every single day, 

I would like to know: within what radius, 

is the price on that day locally maximal? 

Is it maximal— 

If I look back two days and look forward two days, 

is it the best price over that radius around me? 

There could be other applications as well, of course. 

How can I compute 

the domination radius of each individual? 

Maybe the easiest approach is just 

motivated by the way I defined domination radius. 

And, for many problems, this is the right way to get 

started is: just think of what's 

the most obvious algorithm for the problem.

Play video starting at :2:43 and follow transcript2:43

Here, for each individual, 

I'm going to just scan left until 

I reach someone taller than me, 

scan right until I reach someone taller than me, 

and take the minimum of those two distances. 

Basically, exactly what the definition says. 

The trouble is this is maybe 

not the most efficient approach. 

It could run in quadratic time— 

actually Theta N squared, in the worst case. 

If you imagine maybe a triangular shaped array, 

then every single individual is going to end up 

scanning a very long distance in one direction. 

This approach, while simple, 

is maybe not the most efficient. 

But, interestingly, a very small tweak on 

this approach does have 

a remarkable impact on efficiency.

Play video starting at :3:27 and follow transcript3:27

If we do these two scans (left and right) simultaneously 

we scan outwards in both directions 

at the same time, stopping when blocked 

then the running time surprisingly drops 

down to just N log N. It's not obvious why that's the case, 

but let's maybe take a look at why. 

To do that, I think we're going to go back 

to an idea we introduced earlier, 

which was per element running time analysis. 

How much running time is accounted for 

by every element of data in the input. 

The twist on that idea, here, is 

that there are some elements 

that are going to cause us to do a lot of work. 

The very tallest element in 

our input is going to scan a very long distance, 

and so the tallest element 

inevitably is going to cause a lot of work. 

But, there's only one tallest element.

Play video starting at :4:15 and follow transcript4:15

There could be a lot of elements 

that cause a very small amount of work. 

We're actually going to divide 

up our elements into classes 

maybe a high work class of 

elements that scans a very large distance 

but there won't be too many of those elements, 

and then elements that do a smaller amount of work, 

scanning shorter distances, and we can 

tolerate having slightly more of those elements. 

We're going to add up the work done per element, 

but in a slightly more nuanced way. 

Let's think about what's the highest amount of 

work we could possibly do for any element? 

What's the largest possible 

scanning radius that we could see? 

I guess that would be N over 2, if you have 

an element who's dead center in the middle of the array, 

and you scan outwards from that element. 

Let's think about elements with 

a scanning radius maybe in the range from 

N over 4 (N/4) up to N over 2 (N/2) and 

let's say exclusive of N/4, inclusive of N/2.

Play video starting at :5:10 and follow transcript5:10

These are the high work elements, 

the elements from which you spend 

a lot of time scanning outwards. 

We can then think about a class of elements that's 

maybe not quite as bad in terms of amount of work. 

Maybe these are the elements where you scan 

a distance outwards in the range from N/8 to N/4. 

Then I have another class of elements 

which is slightly less work. From 

N/16 to N/8, in terms of the radius that they scan outwards. 

We can have several elements that 

belong to each of these work classes, 

if you want to call them that. 

How many such classes are there?

Play video starting at :5:47 and follow transcript5:47

Well, again, we're dividing by two at each step, 

so we're going to have a logarithmic number 

of these different classes. 

Now, let's maybe build a table and 

figure out some information about 

the elements in these classes. 

First of all, how much work do you spend per 

element or elements in each of these classes? 

Well, the elements in the highest work class, 

you could say that they scan outwards 

a distance of N/2. 

You could call that N/2 units of 

work because that's the radius outward they scan. 

If you wanted to, you could also call 

that N units of work because you're touching N elements 

you know, N/2 on each side. 

The factor of two is really 

not going to make a difference.

Play video starting at :6:32 and follow transcript6:32

It'll just end up being a factor 

of two in the final running time, 

which disappears inside of our big O notation. 

So, I'll go ahead and just call it N over 2 (N/2). 

Then, everything in the next class, 

the slightly less high work class, 

is going to take at most N/4 units of work because 

the maximum radius that 

those guys spend scanning outwards 

is over four and then N/8 and so on. 

Now we get to the key part of the argument. 

I want to know how many elements 

live in each of these classes. 

What's the maximum number of elements in each class? 

To get an idea of this, 

let's look at just the high work class elements, 

the ones that scan outwards at least N/4.

Play video starting at :7:17 and follow transcript7:17

So, if I look at my array, my array has size N, 

maybe let's maybe divide the array up into blocks. 

Each block has size N/4. 

It'll be obvious why we do this in a second. 

Divide the array up into blocks and, N may 

not be evenly divisible by N/4. 

There might be one very 

small partial block left over at the end. 

But what I argue, the crux of 

this argument is that, within each block, 

I can have at most one high work element. 

I can't have two.

Play video starting at :7:51 and follow transcript7:51

What would happen if I had two 

high work elements in the same block? 

That would be problematic because each of those elements 

supposedly scans out a distance of N/4. 

They would see each other when they 

scan outwards because they're close enough. 

And, one of them is presumably taller than the other? 

So, that one would block the other one 

and that is a contradiction that makes no sense. 

The scanning would stop for the shorter one. 

You actually cannot have two 

high work elements in the same block.

Play video starting at :8:23 and follow transcript8:23

They basically high work elements have to be 

spaced out by at least N/4 between them. 

You have, at most, one per block. 

And, I guess, you could have one in 

that little minuscule leftover partial block at the end. 

How many blocks are there? 

I guess there's the block sizes N/4. 

You'd have four blocks, 

and maybe plus one for the leftover block. 

So, I'll say at most four elements here, 

and then maybe plus one for that little leftover block.

Play video starting at :8:52 and follow transcript8:52

The same argument, if you do it 

in the other work classes, 

will tell you that there's at most eight elements 

in the next highest work class 

maybe plus one for that leftover block, at most, 16 

in the next class, maybe plus one again. 

Now, we're almost done. 

All we need to do is just figure out 

what's the total work that 

we're going to end up spending over 

all the elements in each of those classes? 

That's just the work per element times 

the max number of elements. 

If I multiply that together, 

let's see, the 4*N/2, 

that's going to give me 2N, 

and then the +1 times the N/2, 

that's going to give me a leftover little N/2. 

Then if I do the same thing in the next work class down, 

8*N/4 that's going to give me 2N. 

The plus one term is going to 

contribute a little, I guess, an N/4.

Play video starting at :9:46 and follow transcript9:46

Then again, 2N + N/8. 

I guess, if I just want a crude upper bound in each case, 

this is at most 3N. 

So, for each one of these, I'm spending, at 

most, 3N total work per class. 

All the elements in each of those classes 

collectively account for a most 3N work. 

There's a logarithmic number of classes. 

The grand total at the end of the day is going to be 

3N log N as an upper 

bound on the amount of work that I spend. 

So, that's the analysis of the algorithm.

Play video starting at :10:20 and follow transcript10:20

It turns out that this is 

actually a tight bound, in the worst case. 

This algorithm actually can take N log N time, 

if I want to maybe draw an instance that will 

make it take N log N time in the worst case. 

But, let's again look at our array. 

I'm going to draw a pattern that may 

be resembles a ruler. 

Let's make the tallest individual in the middle. 

Then I'm going to put recurse on both sides. 

I'm going to make slightly less tall individuals 

at the 1/4 and 3/4 marks.

Play video starting at :10:54 and follow transcript10:54

Then again, recurse on both sides and make 

slightly less tall individuals at the 1/8ths, 

3/8ths, 5/8ths, 

7/8ths marks, and so on, 

and then keep filling things in. 

There will actually be a logarithmic number 

of these levels of detail because of each time I'm 

recursing again on a half sized part 

of the current array. 

Now, look at the distance that I scan outwards. 

The tallest individual scans outwards in both directions, 

so scanning radius of N/2. 

We call that N/2 work. 

We could also just call that N units of work 

because we're touching 

all the elements as we scan outwards. 

How much work do we then spend on 

the second highest level of height here?

Play video starting at :11:36 and follow transcript11:36

These two individuals, collectively, 

scan outwards also in 

a configuration that touches the entire array. 

You could also say that you take N units of 

work at that level for 

those individuals scanning outwards. 

Again, for the next height level down, 

all of their scanning work, 

collectively, covers the entire array. 

So, that also takes N units. 

Since I have a logarithmic number of 

different levels of height here 

and N units of work per level, 

that's going to add up to N log N. In the worst case, 

this algorithm does indeed actually take N log N time. 

So, the running time in the worst case is Theta of N log N.

Play video starting at :12:17 and follow transcript12:17

Actually, it's interesting. 

There's a couple of different ways I could have 

even built that construction. 

Sp, if you like binary numbers, 

you can just count in binary, 

so look at the numbers 1, 2, 

3 up to 15 in this case. 

I've written them out in binary. 

You know, One is it's a 1 followed by a bunch of zeros; 

and then two is 0 1, three is 1 1, 

four is 1 0 0, and so on. 

If you write all these numbers out in binary 

and, for each number, 

you highlight the least 

significant 1 bit that also gives you 

that same ruler pattern that we just 

showed is a worst case example for our algorithm. 

So, just some nice mathematical 

or combinatorial constructions 

that give you the same patterns there.

Play video starting at :13:5 and follow transcript13:05

Another interesting factoid: it turns out that 

for this particular problem of finding domination radius, 

there is actually an alternative algorithm that 

we can come up with that runs in only linear time. 

And, it's actually also quite simple. 

We're going to implement that algorithm actually in 

our implementation discussion at the end of the module. 

So, you will see that as well. 

But the N log N algorithm that we just talked about, 

we're going to focus on that because 

that's the one that's going to translate 

towards solving our original problem 

of in place matrix transposition. 

Going back to this problem right here, 

the goal is to transpose 

our matrix to rearrange the contents of 

memory that represents our matrix from 

row major to column major format. 

It turns out that we will actually end 

up solving a slightly more general problem than that.

Play video starting at :13:56 and follow transcript13:56

We're actually going to solve the problem of basically 

applying any permutation in place to a length N array. 

The matrix transposition permutation 

is just a permutation of 

our memory that happens 

to change things from row major to column major format. 

But, we'll actually be able to, with 

the algorithm we discussed in a second, 

apply any permutation in 

place without using a substantial amount of 

extra memory as long as 

the permutation is well structured enough 

that we can always figure out two important things. 

So, given any element in our array, 

we have to know where it would 

want to move, according to this permutation, 

because every element needs to move 

somewhere when we apply the permutation, 

and then we also need to be able to figure out from where 

is the element moving that will 

occupy that particular location as well. 

So, the destination that I will move to and the source from 

which the element will move that will then occupy spot i. 

For matrix transposition, we can figure 

these things out pretty easily 

with a simple bit of mathematics. 

Given any location in our memory buffer, 

we can figure out what row and column that represents, 

and then swap the row in the column, 

and then that maps to 

a different spot in the memory buffer, 

which is where you would move if you were 

to have transposed the matrix.

Play video starting at :15:16 and follow transcript15:16

It's pretty easy to just mathematically figure 

out these two quantities, 

in the case of matrix transposition. 

But, there are lots of 

other permutations where you do have 

a nice implicit description of the permutation that lets 

you figure out these quantities on the fly, as needed. 

For any permutation where you know this information, 

a forward and a backward pointer from each location i, 

We can actually apply that permutation in place, 

and the running time is going to end up being 

N log N. Let's see how that works. 

There's one other observation that we 

need to make about the structure of permutations. 

In any permutation, if you start at some element, 

say at position i, 

then step forward to the location where 

i would need to move, according to the permutation, 

and then step forward to the location where 

that element would need to move and so on, 

you end up actually tracing out a cycle. 

Eventually, you'll come back to location i.

Play video starting at :16:12 and follow transcript16:12

It turns out that an alternative way to think about 

a permutation is just as 

a collection of these disjoint cycles. 

A cycle could be as simple as 

just one single element that gets mapped to itself. 

It could be two elements that just swap positions, 

or it could be something much 

longer, like I've drawn here. 

This is an alternative way to 

think about the structure of a permutation. 

It's just a bunch of cycles that are disjoint from each 

other; that collectively cover 

all the elements of the array that we're permuting. 

Enacting a permutation, 

actually moving the elements around 

according to that permutation, is 

just a matter of what you 

call rotating each of the cycles. 

For each cycle, you just want 

to move all the elements on the cycle 

one step in the direction of the cycle.

Play video starting at :16:59 and follow transcript16:59

So, element i is going to step 

forward and move to where it needs to move to. 

That's going to displace an element that then 

moves to where it needs to move to, and so on. 

You just step every element forward, 

one step around a cycle. 

That doesn't take much memory 

at all because you just need 

one constant extra space of memory to hold 

temporarily the element that's being 

displaced at the moment as you walk around the cycle. 

All we need to do to do an 

in place matrix transposition 

i.e. an in place permutation, 

is just rotate each of 

the cycles representing that permutation. 

Those cycles can be a bit 

complicated in terms of their structure, 

so we won't go the route of 

mathematically trying to figure 

out how those cycles look. 

We would just like an algorithm that generically works, 

irrespective of the cycle structure of the permutation in 

question. As long as 

we have this information for every element, 

we have a forward and a backward pointer that describes 

the structure locally of that cycle that the element belongs to.

Play video starting at :18:2 and follow transcript18:02

So, here's the algorithm. It's basically 

three lines of code, at a high level. 

So, what we're going to do is just scan across our array. 

We're going to rotate cycles as we see them. 

The trouble is, since we're operating in place, 

the difficulty here is remembering which 

cycles have been rotated and which ones haven't been. 

As you're scanning across, 

you're going to hit an element on 

this blue cycle and rotate the cycle. 

But then as you continue scanning, 

you're going to hit other elements on the cycle.

Play video starting at :18:33 and follow transcript18:33

You don't want to rotate the cycle at 

that point because you've already rotated it. 

But, how do you know that you have 

already rotated the cycle at that point? 

We would love to be able to maybe mark the elements on 

the cycle to indicate that 

the cycle has already been rotated. 

But, since we're operating in place, 

we don't have the luxury of using 

a huge amount of extra memory to mark those elements, 

so that approach is off the table. 

Instead, what we're going to do is 

designate one element on 

the cycle as the so called leader of the cycle. 

It'll be the minimum indexed element on the cycle, 

the first one we encounter 

as we're scanning through our array, 

and that element is going to be the one responsible for 

rotating the cycle. So, when we hit 

the leader of the cycle during our scan, 

that's when we actually walk across 

the cycle and actually do the rotation.

Play video starting at :19:23 and follow transcript19:23

We move every element one step forward along that cycle. 

For all of the non-leaders, 

we leave the cycle untouched. 

That's the high level algorithm. 

And, running time analysis wise, 

the actual rotation of the cycles isn't 

going to worry us because, collectively, 

we're just moving every element once when we rotate 

all the cycles (because every cycle gets rotated once). 

In total, that's only going to 

add up to a linear amount of 

running time for the work we 

spend rotating all of the cycles. 

The part that we worry about is actually 

trying to determine for 

each element as we scan through the array, 

is that element the leader of a cycle? 

That's really the question mark.

Play video starting at :20:7 and follow transcript20:07

That's the slow part of the algorithm. 

I'm scanning through the array. 

I'm looking at one element. 

Is that element the leader of its cycle? 

How could we determine that? 

Well, there are a couple of obvious ways we can do this. 

One is that we can just trace out the cycle.

Play video starting at :20:23 and follow transcript20:23

We can go through the motions of 

rotating the cycle without actually moving elements. 

So, from each element, you step 

forward and step forward and step forward 

you walk forward along the cycle, 

and eventually you'll come back to 

where you started because it's a cycle. 

But, if you ever encounter an element that has 

a lower index than the element i that you started at, 

you know that you weren't the leader because there's 

someone else on the cycle having a lower index than you. 

You could also walk backwards 

along the same cycle and do the same thing. 

You follow your back pointers and walk around the cycle. 

Again, if you ever encounter 

someone with a lower index than you, 

that means you were not the leader of the cycle, 

and, hopefully now, this is 

starting to look a little bit familiar. 

Remember, with our domination radius problem, 

we scanned left and right until 

we were blocked by somebody taller than us.

Play video starting at :21:13 and follow transcript21:13

Here, we're still scanning left and right, 

but in the context of walking around a cycle, 

and we stop when we're blocked by someone with 

a lower index than us within the array. 

so, it is actually very similar, 

and the same efficiency concerns exist. 

If you do either of these two approaches, 

the running time can end up being quadratic in 

the worst case because you 

could have one really long cycle, 

and these approaches could end up walking a fair distance 

across that cycle before they encounter 

somebody of lower index that blocks you. 

So, if you use either of these two approaches, 

you could end up with a quadratic 

running time in the worst case. 

However, if you do both simultaneously, 

like we did with the domination 

radius problem, then again, 

remarkably, the running time drops to just N log N 

and, pretty much, for exactly the same reason as before. 

So, if we go back and 

think about things in terms of our analysis, 

let's look at the reasoning 

behind why we got N log N 

for the domination radius problem and 

show that essentially the same reasoning gives us 

the answer for the in place permutation problem. 

Again, let's divide up our elements into classes. 

So, high work elements involve scanning 

a large distance both forward and 

backwards along their respective cycles, 

say within distance of N/4 and N/2.

Play video starting at :22:37 and follow transcript22:37

We're going to have the same classes of 

elements based on how much work they spend. 

We have the same bounds on work 

per element because we're still 

scan and touching the same number 

of elements during those scans. 

The max number of elements actually 

is pretty much also the same. 

The argument maybe is a little bit 

different because instead of applying it to an array, 

it's actually being applied to a collection of cycles. 

Let's maybe think about that a little bit more carefully, 

and let's focus on the high work class again. 

Remember, in the high work class, 

elements all scan a distance of at least N/4. 

If we think about an arbitrary permutation, 

it's a collection of cycles.

Play video starting at :23:20 and follow transcript23:20

Here's all of our different cycles in the permutation. 

And, some of those cycles are really small, perhaps. 

Maybe there's less than N/4 elements 

in some of those cycles. They're really small. 

Those tiny little cycles, 

they can't even have a high work element 

on them to start with. They're too small. 

Because, if you had 

a high work element on such a small cycle, 

these high work elements presumably scan 

a distance of N/4 before they are blocked by something.

Play video starting at :23:50 and follow transcript23:50

If your cycle is less than N/4 to start with, 

you'll come back to where you started and stop scanning 

before you reach that N/4 radius. 

We don't even find 

any high work elements on these smaller cycles. 

What about on the larger cycles? 

So, if you have, on a larger cycle, 

you can have a high work element, 

but, again, they still have to be spaced out 

by a distance of at least N/4. 

So, if I walk forwards 

around the cycle from a high work element, 

I have to walk at least a distance of 

N/4 before I can find the next high work element. 

If you had two high work elements that were 

within N/4 of each other along that cycle, 

then they would see each other when scanning outwards, 

and one of them has a lower index than the other 

and would block the other during its scan. 

The same reasoning applies.

Play video starting at :24:46 and follow transcript24:46

You have to have the high work elements 

spaced out by a decent amount, 

and that's why you can't have too many of them. 

If you wanted to make the argument a bit more precise, 

you could say that, for each high work element, 

take the next N/4 elements 

along its cycle in the forward direction, 

and, I'm going to just lay claim 

to those N/4 elements. That's my territory. 

These N/4 elements are owned 

by the high work element 

that was at the beginning of that block. 

No other high work element can appear within that range, 

and no other high work element can lay 

claim to those elements as its territory. 

So, every single high work element has 

its own private range of size N/4, at least, 

that it lays claim to as its territory. 

Those territories are kind of disjoint from each other.

Play video starting at :25:37 and follow transcript25:37

And, since every high work element 

takes N/4 things off the table, 

you can't have more than four high work elements, 

because there's only N elements 

in the world to play around with here. 

There's a couple ways we could argue it. 

This is just just one such way. 

But, that basically gives us 

the same result as we had in our table. 

There's at most four high work elements. 

We don't even get that plus one because we 

don't even have that leftover 

little block because things are cyclic. 

That's why it actually works out even more 

cleanly in the cyclic case.

Play video starting at :26:8 and follow transcript26:08

So, the total work that we spend here is 

actually 2N for each of these work classes. 

And so, we actually instead of 3N log N, 

we get 2N log N 

as our upper bound on the total amount of work. 

That's basically it for the analysis. 

We can do not only in place matrix transposition, 

but a wide range of 

other permutations as long as the permutation 

has enough nice structure to it that we can 

figure out where elements need to move in real time. 

I'll leave this with you. 

Hopefully, it's nice to see 

that even slightly more advanced examples are 

still quite approachable using 

the basic techniques that we've 

talked about in this module. 

[MUSIC]![[Screenshots/Screenshot 2025-08-26 at 1.14.42 pm.png]]

![[Screenshots/Screenshot 2025-08-26 at 1.14.58 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.24.10 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.25.13 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.27.20 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.27.37 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.28.33 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.28.49 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.29.22 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.30.03 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.30.16 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.31.36 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.32.05 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.33.15 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.34.48 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.35.32 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.36.24 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.36.32 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.38.28 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.39.41 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.42.32 pm.png]]![[Screenshots/Screenshot 2025-08-26 at 1.43.05 pm.png]]