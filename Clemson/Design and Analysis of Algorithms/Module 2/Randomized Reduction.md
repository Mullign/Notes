In this video, we're going to add 

another simple and general tool to 

our toolbox for analyzing randomized algorithms. 

This one's going to be based on 

a very familiar and straightforward principle, 

one that we've already seen quite 

a few times in this course. 

It's the idea that if you start with a problem of size N, 

and in every iteration, 

you effectively reduce the size 

of your problem by a constant fraction, 

then you're on track to getting 

a running time of just order log N iterations. 

The prototypical example here 

is our good friend, binary search, 

where you start with the problem of size N, 

and then, in the next iteration, 

you've reduced it down to a problem of size N over 2, 

then N over 4, N over 8— 

Every iteration is effectively halving 

your problem size based on 

the reduction from the previous iteration. 

In randomized algorithms, they do this often as well. 

They start with a big problem and they try and reduce 

the problem size effectively 

down to smaller and smaller sizes 

that makes your problem usually 

easier and easier as you go. 

The trouble is, due to randomization, 

you can't always guarantee that you'll be lucky enough in 

every iteration to get a 

decent reduction in problem size.

Play video starting at :1:12 and follow transcript1:12

However, if you can at least show that 

a decent number of iterations 

lead to a decent reduction in problem size, 

then you are still on track to achieving 

a logarithmic running time in expectation. 

We can do this with a tool that I call 

the randomized reduction lemma. 

And, I've drawn it here in a way that really 

highlights the parallels to the preceding slide, 

showing that this really is just a baby step 

beyond that very familiar intuition that we 

already have for analyzing algorithms 

where you can reduce the problem size in each iteration. 

Here, what do we need to have 

happened to apply the randomized reduction lemma? 

Every single iteration of 

our algorithm independently has to 

have some constant probability, at least, 

of causing a problem size reduction. 

You have to at least have 

a constant probability of like 1/3 or 1/2 or 

something of reducing the effective problem size 

by some constant fraction— 

like 1/3 or 1/2. 

If that's the case, then 

the randomized reduction lemma tells 

you that you take only order log N 

iterations in expectation.

Play video starting at :2:22 and follow transcript2:22

A prototypical example of showing how easy this is to 

apply might be what you could 

call randomized binary search. 

Normally, with binary search, 

you are looking for an element, 

you compare it to the middle element of your array, 

and then recurse to the left or to the right. 

What, if instead, you compare the thing you're looking 

for to a randomly chosen element in the array, 

and then from there you recurse to 

the left or to the right? 

You can imagine that you're not always 

dividing the problem exactly in half at each step, 

but hopefully, in most iterations, 

you're getting still a decent reduction in problem size. 

One way to see this is: suppose you're lucky enough in 

any given iteration to choose 

an element in the middle third 

of your array to compare against. 

That happens, of course, with probability 1/3. 

If that's the case, then the sub problem in 

the next iteration is going to be at most 2/3 of 

the subproblem size in the current iteration 

because, irrespective of whether 

you recurse to the left or to the right, 

you're going to be leaving behind, I guess, 

either the first third or the last third of 

your array in the next subproblem that you look at.

Play video starting at :3:33 and follow transcript3:33

This satisfies the conditions 

of the randomized reduction lemma. 

So, with some constant probability in each iteration, 

we are reducing the size of 

our effective problem by 

some constant fraction. Wait a second. 

It looks like we have a question here in the front row. 

What's your question? Ah. Okay. Good question.

Play video starting at :3:54 and follow transcript3:54

So, the question here is, 

where did these numbers, 1/3 and 2/3 come from? 

Are these arbitrary? 

Could we have used different numbers? 

Could we have still gotten 

a reduction in problem size of 1/2, 

like we got with binary search? All good questions. 

It turns out that, yes, other choices 

of our constants could have also worked. 

I could have just as well said, "Well, 

"suppose that you're lucky enough in 

"an iteration to choose 

"an element to compare against that 

"lives in the middle half of your array."

Play video starting at :4:25 and follow transcript4:25

That happens with probability 1/2. 

If so, that guarantees 

that irrespective of the direction that you recurse, 

your subproblem in the next round is going to 

have a size, at most, 3/4 of what it was in 

this round because you're always 

going to be leaving behind 

either the first fourth or the 

last fourth of your array, 

irrespective of direction of recursion. 

Again, there's a constant probability 

that, in each step of your algorithm, 

you reduce the effective size 

of your problem by some constant fraction. 

What if you wanted that reduction amount to be 1/2, 

like it was with binary search? 

It turns out that that actually doesn't work here. 

That's a little bit too aggressive because 

the only way you can guarantee a reduction factor of 

1/2 is if you're lucky enough to 

compare against the exact middle element 

like what binary search does, 

because only then are both the left and 

the right-hand side subproblems size 1/2 of the original. 

If you compare against any other location in the array, 

one of the two subproblems on 

one side of you is going to be bigger than 1/2.

Play video starting at :5:30 and follow transcript5:30

To guarantee a reduction of size 1/2, 

you actually would have had to 

compare against the middle element. 

There's only a one out of N chance that the 

randomized binary search would have picked 

the exact middle element to compare against. 

That's not strong enough for randomized reduction. 

This needs to be a constant 

—like 0.1 or 1/2 or 1/3— 

a constant strictly bigger than zero. 

And, this other number has to be a constant 

strictly less than one, as the reduction factor. 

So, this actually wouldn't work as a set of 

parameters for the randomized reduction lemma, 

but, fortunately, other choices of constants do work. 

One quick note 

just in terms of the phrase randomized reduction lemma.

Play video starting at :6:12 and follow transcript6:12

This actually comes from a paper that 

I published several years ago, 

where I was basically advocating in 

this paper that this needs to be 

a first-class tool in 

everybody's toolbox for analyzing 

randomized algorithms and data structures, 

because it makes short work of 

analyzing many of 

our most familiar algorithms and data structures. 

The paper goes through maybe a dozen plus, 

very common randomized algorithms. 

It shows how, for each one, 

you can reduce the analysis down to 

just a few sentences or a paragraph, 

compared to what it used to be, 

using other standard tools from 

probability theory that people use 

to analyze randomized algorithms. 

My argument in the paper was, 

basically, that more people need to know about this. 

This should be a common tool. 

However, since people not in this particular class, 

may not have read this paper, 

you'll probably need to just bear 

that in mind if you're communicating 

with other people about how 

to analyze randomized algorithms. 

They may have a different toolset 

that they're familiar with, 

and so you may have to just take that 

into consideration when you're communicating with them.

Play video starting at :7:17 and follow transcript7:17

We will show later on in this module how to prove 

the randomized reduction lemma, so at least you 

can articulate the same concept 

using other ideas that they might be more familiar with.![[mZzHEn7fS566FpkSmo1Mlw_95ab537460044775a76c2f46f35760f1_Randomized-Reduction.pdf]]