In this video, we'll talk 

about some fundamental concepts and 

terminology used in 

the analysis of algorithm performance. 

The main idea here called 

O notation is something 

that I expect many of you have probably seen before, 

but this is an absolutely fundamental concept 

and something we'll be using 

throughout the rest of the course. 

So I definitely encourage you to take 

the time to make sure you understand it properly. 

In terms of making our discussion concrete, 

let's go back to our running examples 

of linear search and binary search. 

Remember, linear search scans sequentially through 

an array and takes 

at most N steps to find a target element. 

If you're searching instead a sorted array, 

binary search runs much 

faster in just a logarithmic number of steps, 

owing to the fact that every single iteration 

effectively reduces the problem size by half. 

In both of these cases, 

we've written the running time 

as a function of the input size 

N. That really highlights 

what we care about with performance analysis.

Play video starting at :1:8 and follow transcript1:08

We care about scalability, 

we care about how running time scales with input size. 

That is elegantly illustrated through the use 

of what's called asymptotic notation or O notation. 

Here we say that linear search takes O(N) 

time and binary search takes O(log N) time. 

Mathematically, the definition here 

is actually pretty straightforward, 

your running time is O of 

something if it's just upper bounded by a constant times 

that something for large values of 

N. This is why it's called asymptotic notation. 

We only care about the regime where 

N grows larger and larger. 

It doesn't matter at all what 

happens with small input sizes of two and three, 

we care about input sizes of 

a million and a billion and beyond.

Play video starting at :1:56 and follow transcript1:56

Let's maybe work through one simple example just 

to reinforce the definition 

and also highlight why this definition is so 

helpful in analyzing performance. 

Suppose we have some algorithm that we 

have painstakingly analyzed and we 

realize that the overall running time is 

exactly 7N^2+5N-2. 

This is the number of exact steps or 

machine instructions that our algorithm runs when we 

execute it on an input of size 

N. This probably took us a lot of work to 

come up with an analysis in 

this level of detail and we would 

probably hope that we wouldn't have to do 

that much work to analyze any given algorithm. 

Conveniently, asymptotic notation lets us 

come up with a much simpler concept 

of performance in this case. 

We could say that the running time for 

large enough values of N is maybe upper bounded by 8N^2, 

and since we're upper bounded by a constant times N^2, 

our running time is O(N^2). 

This gives us a much simpler picture 

of the algorithms running time.

Play video starting at :3:4 and follow transcript3:04

N^2 is certainly much simpler than 7N^2+5N-2. 

But it also highlights what 

really matters in the running time. 

The most dominant term in this running time, 

the one that really does impact 

scalability the most is the N^2. 

If N gets bigger and bigger, 

these lower order terms, 

the 5N-2, they're 

going to become increasingly irrelevant. 

They're not going to contribute much at all to 

the overall rate of growth of 

the running time as N grows large. 

The hidden constant here at the eight that also 

doesn't really matter that much in terms of scalability. 

Maybe all that that is due to is 

the fact that when we compile our algorithm, 

maybe it resulted in eight instructions 

in the middle of our inner loop, 

and that could have just as well been seven.

Play video starting at :3:50 and follow transcript3:50

Our algorithm would still be scaling at the same rate. 

The leading constant doesn't really matter. 

Lower order terms, they don't really matter. 

Asymptotic analysis, O notation, 

lets us really call out the part of our running time 

that matters that really is 

the part that determines scalability. 

It just focuses on the one term 

in our running time has the highest rate of growth. 

This can, unfortunately, 

sometimes lead to a loss of useful information. 

If, for example, you have two different algorithms, 

one of them has a running time of 7N and another one has 

a running time of 7,000N as their actual running times, 

then you might want to alert 

somebody that even though they both run in O(N) time, 

the second algorithm is 

likely to be a lot slower than the first.

Play video starting at :4:42 and follow transcript4:42

The way you would typically do 

that is you would tell somebody that, 

that second algorithm, it has 

a high hidden constant in it. 

We often convey side channel information that way. 

The running time is O event in both cases, 

but the hidden constant is much worse in the second case. 

Yes, we are losing information with 

O notation, but usually, 

this gives us a much simpler high level way 

to think about the performance of 

our algorithm that really does 

highlight what we care about, which is scalability. 

O has a number of relatives that are also 

quite useful for characterizing algorithm performance. 

If you recall, your running time is O(N6^2), 

if it's upper bounded by 

some constant times N^2 as N grows large. 

Similarly, Omega gives you an asymptotic lower bound.

Play video starting at :5:32 and follow transcript5:32

Your running time is Omega of N^2 if it is 

at least a constant times N^2 as N grows large. 

Theta gives you both an 

asymptotic upper and lower bound at the same time. 

Your Theta of N^2 if you are both O(N^2) and Omega(N^2). 

Maybe that means that you live in the range 

between 3N^2 and 8N^2 as N grows large. 

I like to informally think of 

these three notions as just less than equal, 

greater than equal and equal, 

in the event that you're 

looking at the asymptotic rate of growth of 

functions where lower order terms 

and leading constant factors don't matter. 

For example, if you're running time is Theta(N^2), 

it's equal to N^2. 

If it's O(N^2), 

it's less than or equal to N^2 in that sense.

Play video starting at :6:20 and follow transcript6:20

Let's look at a couple of common use cases just to get 

more familiarity with how 

these expressions tend to be used. 

The first two sentences in 

particular illustrate an important point, 

I think. They're very similar. 

The running time of the algorithm 

is O(N^2) and the worst case 

running time is Theta(N^2). What's the difference here? 

Really, the second sentence is actually 

telling you a little bit more information. 

It's really nailing down with certainty, 

the fact that in the worst case, 

the running time really does scale quadratically.

Play video starting at :6:53 and follow transcript6:53

The first sentence is a little bit more vague. 

It's only giving you an upper bound technically. 

For example, if your actual running time was just n, 

the first sentence would still be true mathematically, 

even though it would be very 

pointless for someone to describe 

such an algorithm as O(N^2). 

I think this highlights an important point. 

A lot of times in practice, 

you'll hear people just saying O all 

the time when they really mean Theta. 

For example, you'll hear somebody say 

the first sentence when they 

probably mean the second sentence, 

and I'm definitely guilty of that a lot myself. 

In this course, I would encourage all of us to try 

and use Theta whenever possible, 

because it does provide a bit more information.

Play video starting at :7:39 and follow transcript7:39

It gives you a lower bound as well as an upper bound. 

But in practice, you'll probably 

hear a lot of times people just 

saying O when they probably intended Theta instead. 

If we look at the third sentence, 

the algorithm uses Omega(n^2) memory. 

If I told this to you, 

I would probably be trying to caution you that, 

watch out, the rate of 

memory growth here is pretty substantial. 

The rate of growth in memory is at least 

quadratic in the problem size. 

The amount of memory that I use is 

at least a constant times n^2, maybe it's cubic, 

maybe it's even worse than that, 

but be careful because 

there's a lot of memory being used. 

If I look at the fourth sentence, 

consider the polynomial, 5x^10-3x^9+O(x^8).

Play video starting at :8:24 and follow transcript8:24

This is another common use of 

asymptotic expressions in mathematics. 

Here, it's basically just used to 

abbreviate the presence of lower order terms. 

I'm using an asymptotic expression as 

basically just a placeholder that saves me from 

writing a much more complicated expression 

and simplifies things by 

hiding an irrelevant part of 

the equation that is just of a certain order of growth. 

Then to give maybe a silly example, 

suppose someone comes up to you and says, 

I love you O(n^2). 

What should you think about that? 

Well, in my opinion, 

I'd be a bit concerned about 

pursuing a further relationship because remember, 

O is only an asymptotic upper bound. 

This person loves you at most a constant times n^2.

Play video starting at :9:9 and follow transcript9:09

Whereas if they say loved you Omega(n^2), 

then that would mean that there's 

no limit to how much they can love you. 

They love you at least a constant times n^2. 

Just a whimsical example, 

but also highlights how 

these types of expressions tend to be used. 

There are two other types of 

asymptotic expressions you might sometimes run into. 

They're perhaps a little less common 

than O, Omega, and Theta, 

but good to know in case you see them, 

that is o and little Omega, 

and they basically give you 

strict upper and lower bounds. 

If I ask you, can you solve this problem in o(n^2) time? 

I'm asking, can you solve it strictly faster than N^2?

Play video starting at :9:51 and follow transcript9:51

O but not Theta(n^2). 

If we go back to our informal sense of O, 

Omega, and Theta being less than or equal, 

greater than or equal, and equal, 

these two new expressions basically play 

the role of less than and greater than. 

Let's take a brief look at 

some common running times that we'll 

often see when analyzing algorithms. 

Maybe the simplest is order one, 

which is a little bit weird when you first see it. 

If you unpack that, that means upper bounded by 

a constant times one as n grows large. 

That just means upper bounded by 

some fixed constant independent of problem size. 

It would be certainly rare to see 

an entire algorithm running in constant time.

Play video starting at :10:33 and follow transcript10:33

That wouldn't even give you enough 

time to read the input. 

But you often see parts of 

an algorithm that run in just constant time. 

That's the fastest you could ever 

hope for an algorithm to run in. 

Beyond constant, you hit other very fast running times. 

Logarithmic is very common like with binary search. 

One quick note about logarithmic running times. 

Typically, you don't write the base of 

the logarithm if it appears in a O expression.

Play video starting at :10:58 and follow transcript10:58

You don't write O of log base 

2(n) or O of log base 3(n), 

you just write O(log of n). 

The reason is pretty simple, 

if you look at say log base (n) and log base 3(n), 

those differ only by a multiplicative scaling factor. 

Remember that constant factors 

disappear inside O expressions. 

Those are equivalent when you 

use them inside of a O expression. 

The only time when you do have to be 

a little bit more careful is if 

the log expression appears in maybe a bit 

more of a sensitive place like in an exponent. 

In that case, you would probably 

need to specify the base. 

For example, if I have maybe two to the power 

of log base 2(N) versus 

two to the power of log base 3(n), 

those two actually are quite a bit different.

Play video starting at :11:48 and follow transcript11:48

If I were to simplify those things, 

the rules of logs actually let me swap 

the two and the n and get an equivalent expression. 

This is the same thing as n to the log base 2(2). 

That's a useful trick to know. 

Same thing as N^1. 

If I look at the other expression 

and swap the two and the n, 

I get n to the log base 

3(2) and that is actually very different from N^1. 

Do be careful if you see a log in an exponent, 

then the base of the log actually will matter. 

Moving beyond log n, 

we also see similarly fast running times like n 

or n log n. These are 

very common like a linear running time.

Play video starting at :12:29 and follow transcript12:29

That means you're basically solving the problem 

just as fast as it takes to 

read the entire input of the problem. 

Usually, you can't hope to solve 

a problem in faster than linear time. 

But these are very good running 

times if you can achieve them. 

If your running time is linear, 

that means if the input size 

doubles, your running time doubles. 

That's a relatively good dependence to have. 

Beyond things like linear and n log n, 

you do start to see limitations on 

the size of problems that you can realistically solve. 

N^2, N^3, 

these are called polynomial running times because they're 

a polynomial function of the input size.

Play video starting at :13:4 and follow transcript13:04

Interestingly, in 

the theoretical computer science community, 

polynomial running time has 

become synonymous with the word efficient. 

If a theorist comes up to you and says, 

can you devise an efficient algorithm for this problem, 

they may be asking you, can you devise 

a polynomial time algorithm for this problem? 

Now, in practice, I would argue that 

polynomials like n to the third or n to 

the fourth aren't really that efficient. 

In this class, we're probably going to be 

focusing more on whether we can 

develop things like linear 

running times or n log n or maybe N^2, 

but not very large polynomials 

because those aren't very practical. 

Of course, if you move past polynomial running times, 

things get extremely impractical. 

You can definitely get 

to running times that grow extremely fast like 

exponential running times or 

even worse things like factorial running times or n^n. 

You can only solve extremely small problems 

if your running times are of those forms.

Play video starting at :14:2 and follow transcript14:02

But sadly, there are a lot of hard problems out there for 

which the best known running times 

we have are exponential. 

Lots of common running times that you 

see when you study algorithms. 

Let's maybe put our knowledge to practice and 

just test how well 

we understand these asymptotic expressions. 

Look at the following bit of code. 

This is a really simple bit of code. 

It just has two nested four loops, 

and inside those two nested four loops, 

I increment a counter. 

That just takes constant time.

Play video starting at :14:33 and follow transcript14:33

The question here and this is a prototypical type of 

question that you would find on many an algorithm exam, 

please highlight all of 

the expressions in this table that 

mathematically are correct representations 

of the running time of this bit of code. 

I'll let you pause the video for 

just a second and think about which of 

these expressions you think are correct 

in terms of describing the running time of this code. 

Then you can un-pause the video 

and we can talk about the answer. 

I have highlighted all of the correct answers. 

Let's go through those really quickly. 

The running time here is actually n^2 steps. 

That is O(n^2), 

it's also O(n^3) because n^2 is upper bounded by n^3.

Play video starting at :15:23 and follow transcript15:23

It's Omega(n) and Omega(n^2) 

because it's lower bounded by n. But Theta, 

remember is more specific. 

It's only Theta(n^2) because it's 

both upper and lower bounded by n^2. 

In terms of the o and little Omega, 

remember, those are strict, 

and so it's o(n^3) because 

n^2 grows at a rate strictly less than n^3 

and it's little Omega of n because it 

grows at a rate strictly faster 

than n. If these answers are confusing at all to you, 

you might want to go back and make sure 

that you review the definitions of 

these asymptotic expressions because we will 

be using them quite a bit 

over the course of the semester.![[Screenshots/Screenshot 2025-08-25 at 10.34.11 am.png]]![[Screenshots/Screenshot 2025-08-25 at 10.36.16 am.png]]![[Screenshots/Screenshot 2025-08-25 at 10.37.30 am.png]]![[Screenshots/Screenshot 2025-08-25 at 10.37.42 am.png]]![[Screenshots/Screenshot 2025-08-25 at 10.38.02 am.png]]![[Screenshots/Screenshot 2025-08-25 at 10.38.32 am.png]]![[Screenshots/Screenshot 2025-08-25 at 10.40.21 am.png]]![[Screenshots/Screenshot 2025-08-25 at 11.14.52 am.png]]![[Screenshots/Screenshot 2025-08-25 at 11.22.59 am.png]]![[Screenshots/Screenshot 2025-08-25 at 11.23.31 am.png]]![[Screenshots/Screenshot 2025-08-25 at 11.25.00 am.png]]![[Screenshots/Screenshot 2025-08-25 at 11.27.41 am.png]]![[Screenshots/Screenshot 2025-08-25 at 11.28.50 am.png]]![[Screenshots/Screenshot 2025-08-25 at 11.31.28 am.png]]