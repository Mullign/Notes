![[Solving Recurrences.pdf]]
![[Screenshot 2025-09-10 at 10.02.07 am.png]]
[MUSIC] 

Recursive algorithms like divide and 

conquer algorithms may initially seem hard to analyze, 

but with the right tools in our toolbox, 

we can usually make short work 

of that task in many cases, 

solving for the running time on site. 

In this discussion, 

let's properly introduce the divide and 

conquer technique and talk about how to 

analyze the running time of 

divide and conquer algorithms. 

Divide and conquer is a pretty well named technique. 

But the technique is what the name suggests. 

To solve a big problem, 

we partition it up into 

smaller sub problems and that's done 

in a very problem specific fashion. 

Typically, the partitioning is multiplicative in nature. 

So you divide into two sub problems of 

size N over 2 or three sub problems of size N over 3.

Play video starting at ::51 and follow transcript0:51

You typically don't divide into one sub problem 

of size 1 and another one of size N minus 1. 

It's typically more balanced than that. 

The sub problem sizes don't have to be equal. 

But typically they are, 

and it is important that 

the sub problems should have the same form as 

the original problem because we'll be using 

the same algorithm just recursively to solve them. 

Now once you've solved the sub problems, 

you recombine their solutions again in 

a very problem specific fashion to 

somehow get a solution to the bigger problem. 

That's divide and conquer in a nutshell. 

We have already seen a couple of 

prominent examples of divide and conquer algorithms.

Play video starting at :1:30 and follow transcript1:30

Probably the prototypical divide and conquer algorithm 

is merge sort that where to sort an array of size N, 

and you first sort the first half recursively, 

you sort the second half recursively and then 

merge those two sorted sub arrays together. 

Quick sort would be another prominent example. 

To quick sort an array, 

you partition it into two pieces based on 

some choice of a pivot element and 

then recursively sort those two pieces. 

Quick sort is a little bit interesting because 

oftentimes we look at 

the randomized variant of quick sort, 

where it's hard to predict the sizes of the two pieces. 

So many of the techniques we're about to talk about 

are maybe less easy to apply to quick sort. 

For quick sort, we might need 

to use more techniques from 

say randomized analysis from the previous module. 

How do we typically describe the running time of 

a recursive algorithm like 

a divide and conquer algorithm?

Play video starting at :2:23 and follow transcript2:23

Since these algorithms are themselves recursive, 

it makes sense that we 

describe their running time recursively. 

We can write what's called a recurrence, 

which is a recursively defined expression 

that describes the running time of a recursive algorithm. 

If we use merge sort as our running example here, 

if you want to merge sort an array of size N, 

let's say T of n is 

the amount of time it takes to do that, 

then what components make up T of n? 

Well, there are two recursive sorts of size n over 2, 

and then there's a merge that runs in linear time. 

We can say that the time it takes to 

sort a size n array is 

twice T of n over 2 because there are two recursive sorts, 

plus Theta of n because there's a merge. 

This is a recursively 

defined expression for the running time, 

known as a recurrence. 

Of course, with most of these recurrences, 

you have a base case where if you're 

trying to solve a problem of constant size, 

that only takes you constant time.

Play video starting at :3:16 and follow transcript3:16

It's usually easy to write a recurrence that 

describes one of these divide and conquered algorithms. 

The interesting part is solving that recurrence to get 

something that's more of 

an explicit formula in terms of problem size. 

So something that just says, 

the running time is on the order of 

n log n with no recursive terms to deal with. 

And so that's our task for 

the rest of our discussion here. 

How do you go from the recursive description 

of an algorithm as 

a recurrence to a solution that just describes 

directly the running time as 

a function of the input size? 

So first things first, 

it turns out that you can usually 

clean up recurrences and simplify them. 

So they're a little bit less daunting.

Play video starting at :3:59 and follow transcript3:59

If you look at merge sort again, 

then the actual recurrence, 

remember n could be even or odd, 

so that the actual recurrence would 

probably be something like T of n is 

T of n over 2 rounded up plus T of n over 2 rounded down. 

Because that works in 

the case where n is even or n is odd, 

and then of course, plus the Theta n term due to the merge. 

Conveniently, these little things 

like floors and ceilings, 

the small additive offsets within these recursive terms 

actually don't have any impact on 

the asymptotic form of our solution, 

and you can safely ignore them. 

If you had a term like T of n over 2 plus 7, for example, 

with a small constant additive offset inside of it, 

you can just ignore that plus 7. 

It won't actually contribute anything to 

the asymptotic form of the solution. 

Since floors and ceilings are 

themselves nothing more than small additive offsets, 

you can ignore those as well. 

Also, the term here that's not recursive, 

the Theta n at the end, 

you can actually just turn that into 

plain old n because Theta n 

just means a constant times n. If we replace that with n, 

assume the constant is 1, 

that's really only going to change 

the solution by a constant factor 

and it also won't affect 

the asymptotic form of the final solution.

Play video starting at :5:17 and follow transcript5:17

At the end of the day, we can end up solving 

a much simpler looking 

recurrence than what we started with. 

Usually when you see a recurrence, 

try and simplify it and clean it up first and 

then look at how to actually 

compute an explicit solution for it. 

Now, a useful approach to keep in the back of 

your mind for approaching almost any type of recurrence, 

especially those you might not 

otherwise know how to solve, 

is you can just simply take the recurrence 

and expand it out algebraically by 

a couple of levels and look for patterns that might 

suggest what the final form of the solution would be. 

If I take the merge sort recurrence, 

for example, and just expand it out by a few levels, 

simplifying as I go, 

you might notice this emerging pattern 

of n + n + n and so on. 

Then you realize, the argument here on 

the recursive term is decreasing 

from n over 2 to n over 4 to n over 8 and so on. 

I'm probably going to end up with a logarithmic number 

of those plus n terms 

giving the n log n. This is 

one way that you can approach solving recurrences.

Play video starting at :6:18 and follow transcript6:18

It's maybe a little bit messy though 

and we would hope that we'd be 

able to solve most of these divide and 

conquer recurrences much more easily. 

Indeed, that will be the case. 

If we maybe focus our attention on 

a restricted class of recurrences just for simplicity, 

this is a restricted class of recurrences, 

but it does cover almost every type of recurrence we're 

likely to see with most 

simple divide and conquer algorithms. 

Here, we're going to focus on 

an algorithm that to solve a problem of size n, 

it basically breaks it up into 

A sub problems of size n over b, 

and then it spends f of n time 

in both the decomposition part of the algorithm 

and the part that recombines the solutions of 

the sub problems once we solve them recursively. 

Let's consider a recurrence of this form. 

This is, again, it's a restricted type of recurrence, 

but it's also quite general it captures 

just about every recurrence we're going 

to see in our examples that follow. 

To solve a recurrence like that, 

we can actually do an algebraic expansion, 

but in a more convenient way, 

we're going to actually expand out 

the recurrence as a tree.

Play video starting at :7:26 and follow transcript7:26

Take again, the merge sort recurrence, 

and I can start to expand it out in a tree like form. 

The non recursive part n, that ends up at the root, 

and then I have my two copies of T of n over 2, 

and then I expand them. 

They're going to expand into n over 2 plus 

two copies of T of n over 4 each. That's the idea. 

I do essentially an algebraic expansion, 

but in the form of a tree. 

This tree pretty much 

depicts the recursion tree of merge sort. 

What's the last thing merge sort does?

Play video starting at :7:57 and follow transcript7:57

Well, the last thing it does is a merge, 

it takes linear time to combine 

two big arrays into one size n array. 

This is the final merge. 

What happens in the next level of recursion down? 

Well, in that level of recursion, 

you're creating two sorted arrays of size n over 2, 

and you're spending n over 2 work 

in each of those sub problems doing that. 

The next level of the tree talks about how much work 

you spend and one level deep in the recursion. 

Then the next level is going to be 

two levels deep in the recursion. 

What we're actually going to end up 

doing here is adding up 

the total amount of work we spend level by level, 

which corresponds to adding up how much work 

the algorithm spends per level of recursion.

Play video starting at :8:42 and follow transcript8:42

At the very end, we spend n units of work, 

one level into the recursion, 

we're spending twice n over 2, 

which is also n units of work, and so on. 

Conveniently, we also still get this n + n + n pattern 

log n times for a running time of n log n. 

This is where we're heading. 

We're going to take 

the recurrence that we're dealing with, 

expanded out in a tree, 

and then add up the total amount of work done by 

the algorithm on a level by level basis, 

which corresponds to adding up the amount of work 

done per level of recursion in the algorithm. 

Here it's quite easy because you 

get the same contribution per level, 

and it's pretty easy to see that there 

are logarithmically many levels 

because you're decreasing from n to n over 2 to n over 4 and so on. 

But what happens if you have 

a different contribution per level? 

Let's look at maybe a different recurrence, 

this would correspond to a situation 

where to solve a problem of size n, 

I break it up into two sub problems 

of size n over 3, recursively solve those, 

and I spend n units of work in 

the partitioning part of 

the algorithm and then the recombining part at the end, 

where I put the solutions back together.

Play video starting at :9:53 and follow transcript9:53

If I expand this out as a tree, 

something interesting happens if 

I add up the work per level. 

I actually end up with a geometric series that 

decreases from n to two-thirds of n to four-ninths of n. 

The most amount of work I actually 

spend is in that last level of 

the algorithm where I spend order 

n time putting all the solutions back together. 

The recursive parts actually don't 

seem to add up to as much here because 

the amount of work for 

these recursive levels is dropping 

off according to a geometric series. 

If I want to find the total amount 

of work spent by the entire algorithm, 

I just have to add up 

a decreasing geometric series. How do I do that? 

Well, in the last module, I think it was, 

we actually looked at techniques 

for adding up geometric series.

Play video starting at :10:43 and follow transcript10:43

There are, of course formulas for doing it. 

My favorite approach was, 

we called it shifting where you 

can take the series and you 

shift it over and subtract it 

from itself to cancel out a lot of terms. 

But at the end of the day, 

since all we care about is 

an asymptotic expression for the solution, 

like a big O expression, 

we actually don't have to do any work when 

adding up a decreasing geometric series. 

Look at this example right here, 

I have a decreasing geometric series, 

n-squared (n^2) + three quarters n^2 + three quarters^2 n^2 ... Maybe it's a finite series. 

Maybe it keeps going infinitely. 

However, if I add that series up, 

it's upper bounded by 4 n^2 in this case.

Play video starting at :11:24 and follow transcript11:24

It will always end up being upper bounded 

by some constant times n^2, 

and in asymptotic expressions, 

we don't care about constants. 

The answer is basically going to 

be the first term of the series, 

at least in an asymptotic sense. 

If you want to add up a decreasing geometric series, 

the answer is just its first term, 

Theta of its first term. 

You actually don't have to really add it up. 

You just notice that it's a decreasing series and say, 

oh, the answer is Theta of the first term of the series. 

In terms of our tree, that was 

the term that was sitting at the root. 

Now, what if we have an increasing geometric series?

Play video starting at :12:1 and follow transcript12:01

I guess, don't be fooled. 

That is just a geometric series 

that decreases but written backwards. 

The answer there, at least asymptotically, 

is going to be Theta of its last term. 

So we can actually really make 

short work of adding up a geometric series. 

If you know if it's decreasing versus increasing, 

the answer is just going to be basically 

Theta of the first or the last term. 

Now if we go back to the problem of adding up 

all the work in this tree that 

is how much work we spend per level of recursion, 

it's a decreasing geometric series. 

The answer is going to be Theta(n).

Play video starting at :12:35 and follow transcript12:35

If Theta of the contribution at 

the root level because that's the first term. Very easy. 

You don't actually have to do much work 

to get the final form of the solution. 

Similarly, you can actually 

also get increasing geometric series. 

This would be a recurrence that does that. 

To solve a problem of size n, 

I divide it up here into three sub problems of size n over 2, 

and I spend n units of work in 

the non recursive part of the algorithm, 

both subdividing and recombining things. 

If you were to expand this out as a tree, 

you end up with an increasing geometric series.

Play video starting at :13:12 and follow transcript13:12

The final answer here is going to be 

Theta of the contribution of the final term, 

which basically describes the contribution of the leaves. 

Remember that each leaf as 

a base case just contributes a constant, 

really the answer here is 

just the number of leaves in your tree. 

And there's actually a simple expression for that. 

This one might actually be worth memorizing. 

It's just n to the log base 2 of 3 (n^log_2(3)). n^log_b(a) in the form 

of the recurrence that we're dealing with here. 

Let's maybe actually do the math on 

that just to make sure that that's clear. 

Here's the tree and the corresponding increasing 

geometric series that it gives.

Play video starting at :13:52 and follow transcript13:52

It was n and then three-halves n, then three-halves^2 n and so on. 

But we really are interested in what's the last term in 

that series that describes 

the contribution just due to the leaves. 

Since each leaf is contributing a constant amount, 

we really just care how many leaves are there. 

That's easy to calculate because 

our branching factor here is 3. 

This number here is the branching factor. 

The number of leaves is going to be 

3 to the power of something because every 

step we take down the tree, 

we triple the number of nodes in the tree. 

What's the depth of the tree?

Play video starting at :14:29 and follow transcript14:29

It's going to end up 

being 3 to the depth of the tree. 

Well, every step down the tree, 

we're dividing by two. 

It's going to end up being 

3 to the power of log_2 of n. 

Because of convenient properties of logs, 

I can actually swap the 3 and the n 

and I get something that's equal. 

That's n^log_2 of 3, n^log_b of a. 

That's a useful expression to 

remember because that's the answer you get in 

the increasing case when you have 

a geometric series level by level that increases. 

We basically now know how to 

analyze a divide and conquer algorithm, 

it's just a matter of putting things together.

Play video starting at :15:14 and follow transcript15:14

If we look back at the form of our recurrence, 

we're solving A sub problems of 

size n over b, and then maybe spending n to the alpha time, 

not in the recursive parts of the algorithm, 

in the subdivision and recombining steps. 

Then the observation here is if you expand 

out the work done by 

your algorithm in the form of a tree, 

if you add up the amount of work 

of per level of recursion, basically, 

this will always end up giving you a geometric series, 

and that geometric series will either be decreasing, 

increasing, or staying the same at each level. 

It's easy in all three of 

those cases to know what the answer is. 

If the solution is a decreasing geometric series, 

then the root is the answer, 

because the answer is 

Theta of the first term in the series, 

and the root is just going to be 

this term right here, the n to the alpha. 

We already saw if you have 

an increasing geometric series. 

The answer ends up being this n^log_b of a. 

That's the contribution of the leaves.

Play video starting at :16:15 and follow transcript16:15

Then finally, if the series is unchanging, 

you get the same contribution per level. 

Well, the contribution on each level is 

going to be this n to the Alpha, 

and you have a logarithmic number of levels, 

so you're going to get n to the Alpha times log n. 

Only three possible cases, 

and as long as you can figure out what case you are in, 

it's easy to know what the answer ought to be. 

Sometimes this is just given 

to you explicitly as a formula. 

If you read an algorithms textbook, 

a lot of times they will basically present 

you with the master method for solving a recurrence, 

which basically gives you 

a formula for the answer of the recurrence. 

What you do is you're 

looking at a recurrence of this form, 

and the crucial comparison 

is the alpha versus this log_b of a term. 

Whichever one is bigger wins.

Play video starting at :17:6 and follow transcript17:06

If alpha is the bigger term, 

then the answer is Theta of n to the Alpha. 

If the n^log_b of a term is bigger, 

then the answer is that n^log_b of a. 

If they're equal, then you 

actually get this n to the Alpha log n. 

A lot of times you'll 

find the solution of a recurrence articulated this way. 

If you like formulas, 

that's by all means, there's your formula. 

But to me, I like to know the intuition behind this. 

These three cases really just correspond to 

the situation where the geometric series that 

you get when you expand out in 

a tree form is decreasing unchanging or increasing 

and a lot of times if you're looking 

at a recurrence that you are trying to solve, 

you can figure out which of these cases is 

happening by mentally expanding out 

that tree by just one level 

because all it takes is one level 

before you know if the series 

is decreasing, or staying the same.

Play video starting at :18:3 and follow transcript18:03

And therefore, with just a little bit of practice, 

you can mentally realize, I expand the tree out, 

it's a decreasing series, 

so the answer is just whatever was at the root. 

So you don't even really have to 

memorize formulas per se. 

I think my suggested approach is in your head, 

expand out the tree by one level, 

and then there are three possible cases, 

you know which case you're in, and 

then you know what the answer ought to be. 

At this point, it's just up to doing some practice. 

Let's look at a couple of 

recurrences and work through their solution. 

You'll also have plenty of practice exercises 

to work through just to 

build your familiarity with doing this analysis. 

If we go back here, let's look at, 

I have written down a number of different recurrences, 

and let's just go through 

and talk about how to solve them.

Play video starting at :18:55 and follow transcript18:55

So the first recurrence is 

the familiar merge sort recurrence. 

I probably don't even have to solve that one. 

That one, of course, we know, 

solves t of n = Theta of n log n. It's just merge sort. 

Remember with that one we already showed, 

if we expanded out, we got n on every level of our tree. 

So that was an unchanging geometric series. 

So let's take a look at the second recurrence now.

Play video starting at :19:21 and follow transcript19:21

The second one is just meant to scare you, 

but it's really just merge sort again, 

because remember that small additive offsets 

in these recursive terms can be safely ignored. 

And so this boils back 

down to the merge sort recurrence with the 

same exact Theta of n log n solution. 

What about the next example, 3T of n over 2 + Theta of n? 

I think we actually looked at that as well. 

Let's in our heads, 

see what we can do if we're expanding that tree out. 

What's going to be at the root of the tree? 

The root of the tree is going to have an n 

because that's going to be the non recursive part.

Play video starting at :20: and follow transcript20:00

Then we're going to have a branching factor of 

three because we're breaking 

it up into three recursive sub problems, 

each of size n over 2. 

If you expand this out by one level, 

you're going to get three copies of 

T of n over 2 on the next level 

of the tree with an n at the root. 

This is just a 

straightforward algebraic expansion of that recurrence. 

Now what happens if I were to expand those T of n over 2? 

Those would effectively turn into n over 2 

and three copies of T of n over 4, I guess. 

But I don't even need to worry about the next level down. 

All that I really need to worry about is that 

each of these is going to turn into an n over 2.

Play video starting at :20:44 and follow transcript20:44

At the next level down, 

I actually get 3n over 2. 

It's an increasing series. 

I went from n to 3 halves of n and so on. 

I know in that case, that the answer is going to end up 

being Theta of n^log_b of a, log_2 of 3. 

That's the one formula that I pretty much like to 

memorize because it makes 

things easy in the increasing case. 

What if I instead had 

a Theta of n^2 term in that same occurrence? 

If I go back to my tree picture, 

the root is going to have an n^2 now, 

and when I expand out these 

T of n over 2 is the next level down, 

that's going to give me an n over 2^2 which is 

actually n^2 over 4 and so if I have three of those, 

I'm actually going to end up with, I guess, 

3n^2 over 4 in the next level.

Play video starting at :21:38 and follow transcript21:38

This actually gives me a decreasing geometric series. 

I go from n^2 down to 

3 quarters n^2 and so on because it's decreasing, 

this is really the easiest case, 

the answer is just whatever is sitting at the root, 

so Theta of n^2 would be the answer. 

So it takes a little bit of practice to be able to do 

this and maybe the master method is a more familiar, 

better approach for you, 

but I still like to mentally try and expand the tree out 

and apply the true intuition behind the master method. 

Let's go more quickly through these and I'll let you 

do the actual tree expansion 

on your own in your own time. 

If we do expand out the next one, 

you're actually going to get an unchanging series. 

It's very similar to the one we 

just did instead of three quarters, 

you're going to get four quarters, 

which is just n^2 at the next level. 

This one is going to end up being n^2 log n.

Play video starting at :22:36 and follow transcript22:36

Because you're going to get n^2 

on every level of the tree and there's 

a logarithmic number of levels. What about the next one? 

I have n^2 at the root, 

and this one gets a little 

tricky to think about there's 

a branching factor of eight, 

and each one of those expands into a T of n over 3. 

So what's going to happen if I expand those terms out? 

Those are going to turn into 

I guess n over 3^2 which is going to be n^2 over 9, 

and I have eight of them. 

I'm actually going to end up with I think 

eight ninths of n^2, the next level down. 

This is actually a decreasing series, 

and I'm going to end up with a total running time 

of just n^2 because 

that's the contribution at the root level in this case.

Play video starting at :23:28 and follow transcript23:28

What about the next one? 

81T of n over 3 + Theta of n^4? I think that's going to be 

unchanging because 81 is 3^4. 

This one is going to end up being 

unchanging n^4 just times a log n factor. 

In an unchanging series, 

you basically just add a log 

to whatever the non recursive term is. 

Actually, the next one is interesting. 

This is one that I see students messing up quite often.

Play video starting at :23:59 and follow transcript23:59

If we expand this 

is an algorithm that breaks up a problem of size n 

into two sub problems of size n over 2 and spends 

a constant amount of work doing the decomposition. 

If you expand this out as a tree, what do you get? 

You get a constant contribution at the root, 

and then you have two copies 

of T of n over 2 in the next level down. 

If you expand them out, 

what are they going to turn into? 

They're going to also turn into 

a constant plus two copies of T of n over 4 and so on. 

If you look at the contribution per level, 

you're going to get one and then two, 

and then four, this is an increasing geometric series. 

The answer is actually going to be dominated 

by what's at the leaf level, 

n^ log_b of a is n^log_2 of 2.

Play video starting at :24:49 and follow transcript24:49

This is actually going to end up as linear. Beta of n. 

And then finally, 

this ridiculous recurrence 1,023, 

which is one less than 1,024, 

which is 2^10, 

I think that one less makes this 

into a decreasing geometric series, 

and so this is going to end up being just Theta of n^10. 

So these end up not being that 

hard to solve once you get 

a little bit of practice doing this. 

[MUSIC]