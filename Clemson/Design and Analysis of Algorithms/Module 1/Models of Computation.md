So far, we've swept under the rug, 

one important detail of our algorithm analysis process, 

which is what should count as 

one step in the execution of our algorithms. 

Let's maybe address that a bit more properly and also 

talk about an important topic in algorithm design, 

which is a model of computation. 

This actually touches on a very deep question or set of 

questions in computer science questions 

like what is a computer? 

How do you mathematically define what computation is? 

What is an algorithm, really? 

Is an algorithm the same thing as a computer? 

These are actually somewhat challenging questions 

and part of the reason that the top award in our field is 

called the Turing Award is because 

of some of the contributions that Alan Turing 

made towards providing a mathematical framework 

for defining what computation is.

Play video starting at ::52 and follow transcript0:52

For now, we're just going to be 

concerned with the much easier question 

of what should count as a single step in our algorithms? 

This leads us to the concept of a model of computation. 

We would like to develop algorithms that are generic, 

not tied to any particular 

hardware platform or configuration, 

and so we actually define 

an abstract computing environment 

on which our algorithms execute. 

That's our model of computation. 

Specifying a model of computation 

basically is akin to specifying 

the capabilities of our abstract computer 

that will be running our algorithm. 

We actually are going to use a pretty standard model of 

computation throughout this class called the RAM model, 

the Random Access Machine model. 

It's extremely simple.

Play video starting at :1:35 and follow transcript1:35

In fact, it's probably over simplified in many ways. 

Your memory consists of a large array of integer words. 

You can do random access into memory. 

You can given an index into memory, 

you can do a read or write in constant time. 

Then you can also do simple arithmetic operations 

like additions or multiplications or 

comparisons also in just constant time 

and that's the model. 

Very straightforward model of computation, 

there are some oversimplifications 

here compared to actual hardware, 

but on the whole, this is not a bad model to use. 

If you want to look at maybe some of the inaccuracies, 

you could say that things 

like addition and multiplication.

Play video starting at :2:17 and follow transcript2:17

The actual circuits that implement 

those operations may not actually have constant depth, 

and so assuming constant time for 

those operations may be a little bit aggressive. 

Also, sometimes operations like 

multiplication may be a little heavier than 

other operations like addition and so it may be 

a bit of a simplification to 

just say that everything takes constant time. 

But probably the worst offender here is memory access. 

A lot of times memory reads and 

writes take substantially longer 

than simple arithmetic operations 

on words that are stored in CPU registers, 

and that's not really captured by this model. 

Sometimes even memory writes take longer 

than memory reads because of 

the way real world memory systems with 

multiple levels of caching behave. 

We will see in our enrichment lecture this week, 

actually some models of computation do actually look more 

closely at the memory side of the picture 

and that it can be more realistic, 

better descriptive models in 

situations where your algorithm is memory bound. 

Another interesting question is 

how large should a word be?

Play video starting at :3:21 and follow transcript3:21

How many bits should there be in a word? 

A modern digital computer probably has 

32 bits or 64 bits in a word. 

In theory, for our abstract computing environment, 

we have to be a little bit careful. 

There's a Goldilocks principle here. 

You can't make the size of a word too small or too large. 

Too small and you've 

handicapped the model by quite a bit. 

In fact, you often have to 

assume that the size of a word is going to have 

to be at least on the order of 

log(N) if your input size is N, 

Because if you didn't have 

log_2N bits available in a word, 

you couldn't even count as high as N, 

and that would be a huge handicap for an algorithm.

Play video starting at :4:1 and follow transcript4:01

With an input size of N you couldn't even 

index into memory if you had 

N elements of data stored memory, 

you wouldn't be able to hold the index 

of an element of data in a word, 

and that would be a huge handicap. 

We usually assume that the size of a word has 

to be at least logarithmic in N. We 

also can't assume that the size of a word can 

be too large because then you'd be able 

to do unrealistic things and 

cheat by packing a lot of information into a single word, 

and then with one addition or multiplication, 

you could do a lot of things in parallel. 

You could do an unrealistically large amount 

of computation with one operation. 

This gets a little bit into the territory of subtlety. 

For the most part, we can 

safely ignore issues like word size. 

Of course, when you're actually 

writing a computer program, 

you do want to make sure you're not 

overflowing your integers and things like that.

Play video starting at :4:50 and follow transcript4:50

But this is an issue that you 

generally don't have to worry 

about on a daily basis 

as you're designing your algorithms. 

A couple of other prominent models. 

Oftentimes for problems like sorting and searching, 

we use the comparison based model, 

which is the same as the RAM model, 

except for elements of data that come from the input, 

We assume that they're like little black boxes. 

We don't assume anything about what they are, 

except that they can be compared pairwise. 

You can tell if one is less than 

or greater than or equal to another. 

But we don't assume that they're 

integers or strings or anything like 

that and this leads to 

a set of algorithms that are very generic. 

All they require is that their input be comparable.

Play video starting at :5:30 and follow transcript5:30

For sorting, for example, you can sort anything. 

You can sort strings, you can sort integers, 

you can sort real numbers. 

The algorithms are very generic and very simple. 

This does come with a price in terms of running time, 

though, as we'll see later on in this particular lecture. 

A related model that seems to usually give 

very similar performance guarantees 

as the comparison model, 

is sometimes called the Real RAM model, where it's again, 

the RAM model, but we 

make the unrealistic assumption just for 

simplification purposes that a word 

can actually hold a real number, 

and you can do exact arithmetic 

on real numbers and that's totally 

unrealistic because real numbers can be 

things like the square root of 2 or Pi, 

that are irrational, and you of course, 

can't represent those things exactly on 

a digital computer with finite precision. 

However, this can be 

a nice simplification if you're developing algorithms 

maybe involving geometry where 

the distance between two points can be irrational. 

It's nice to be able to not have to 

burden your thought process with issues 

like round off errors and 

precision related issues during the design process.

Play video starting at :6:36 and follow transcript6:36

You can design the algorithm 

pretending that you can do 

exact arithmetic on real numbers. 

Of course, at the end of the day, 

when you do implement these algorithms, 

you do have to contend with 

round off errors and issues of finite precision and such. 

We will actually over 

the course of the next couple of modules, 

we'll see a lot of different algorithms that 

run in different models of computation, 

and there are actually some running time 

implications based on model of 

computation that might make 

certain algorithms look better than others. 

But the distinction is 

maybe a little bit more superficial 

because they're doing the best they 

can within a particular model of computation. 

There's a little bit of an apples to oranges 

comparison that we might sometimes 

be tempted to make between algorithms. 

Just to give you an example, 

there's a very simple problem called element uniqueness, 

where you're given N elements of data, 

and you're supposed to determine 

if they're all different from each other. 

Are they all distinct, or are there duplicates present?

Play video starting at :7:33 and follow transcript7:33

It turns out that in the RAM model, our standard model, 

we can actually solve that problem 

in linear expected time, 

using techniques like caching, 

which we'll talk about in a future module. 

But in the comparison based model or the real RAM models, 

you actually have a lower bound. 

In the worst case, you can prove that any algorithm for 

solving this problem must take 

at least on the order of N log N time. 

Interesting distinction, and this 

exists for many different problems. 

If you have an algorithm for element uniqueness, 

like one simple approach would be 

like run merge sort to sort your input and 

then scan through the sorterd ordering and look at 

adjacent pairs and see if there are any duplicates. 

You can solve this problem in N log N 

time in the comparison model. 

That's actually optimal in the comparison model.

Play video starting at :8:12 and follow transcript8:12

You can't hope for any better result, 

at least in terms of worst case running time, 

an N log N algorithm in 

the comparison model is the best you could hope for, 

even though it doesn't match the order N that you would 

get from a RAM based algorithm. 

You have to be a little bit cognizant of 

model of computation if you're making claims about, 

if one algorithm is better than another. 

It's a little bit fraught to use that term, perhaps. 

In practice, of course, N is better than N log N. 

But locally within your model of computation, 

N log N is the best you could hope to do in this case. 

Following up on that, we will see over the course of 

the next few modules several algorithms that 

usually break down into two main categories. 

You have RAM algorithms that are 

inherently RAM algorithms because 

they require their inputs to be integers.

Play video starting at :9:6 and follow transcript9:06

That's the one feature of the RAM 

that really is a feature of the RAM. 

Each word holds an integer. 

These algorithms assume that 

their input consists of integers, 

and because of that, you can actually exploit 

that fact and get certain speed ups in your running time. 

You can use an input element as 

an index into an array because you know it's 

an integer and this lets 

you use things like lookup tables and 

hashing and other techniques 

that require integer valued data. 

One example we've already seen here is counting sort, 

which can sort an array of small integers, 

integers less than C quite fast 

in almost linear time if C is very small. 

On the other hand, you have algorithms that 

don't really make any assumptions 

about what their input elements are, 

and these are more of the comparison-based algorithms 

which can sort anything as long as it's comparable. 

Here you do pay a price in terms of running time.

Play video starting at :9:57 and follow transcript9:57

The best you could hope to do, 

we'll see in a second for 

a comparison based sorting algorithm is actually N log N. 

We've actually seen 

quite a few sorting algorithms 

so far that are comparison based. 

You selection sort, insertion sort, 

and bubble sort algorithms, for example, 

those are order n^2 worst case algorithms, 

and merged sort as an order N log N algorithm. 

Those are all comparison based sorting algorithms. 

Here again, you see this distinction where counting sort, 

being RAM based, could outperform these if C is small. 

But that's just because 

counting sort is operating in a more powerful, 

less restrictive model of computation. 

This is actually worth discussing 

the sorting problem in particular.

Play video starting at :10:38 and follow transcript10:38

There's a famous result that says that sorting in 

the comparison model cannot 

improve on this order N log N worst case bound. 

I want to spend a few minutes talking about that result, 

because this is also something 

that happens alongside a discussion of 

models of computation is you 

can actually prove lower bounds on 

or impossibility results showing that in 

certain usually restricted models of computation, 

there are limits to how fast 

you can solve certain problems. 

If we turn our attention to sorting. 

Here's a trick question, essentially, 

what's the fastest known running time 

for sorting n numbers? 

There's a couple of different choices here. 

The answer interestingly is it 

depends on your model of computation. 

All four of these answers could be correct, 

depending on what you adopt as 

your underlying model of computation.

Play video starting at :11:30 and follow transcript11:30

In the comparison model, 

we'll see in a second actually a proof that 

n log n is the best you could ever hope to 

do in terms of worst case running time. 

In the RAM model, interestingly, 

the fastest known algorithm that I'm aware of for sorting 

runs in n times the square root of 

log of log(n) in expectation. 

That's a relatively weird looking running time. 

Perhaps that suggests that there is 

an even faster running time yet to be 

discovered that we have just not found. 

If you have a RAM model with a small word size, 

say like order log(n) and bits in a word, 

you can actually sort in just linear time, 

which is interesting. 

Then just to take things to an absurd extreme, 

you could define a very unrealistic model of 

computation that has a single instruction 

that sorts N integers. 

In this just completely unrealistic hypothetical model, 

sorting would take constant time.

Play video starting at :12:21 and follow transcript12:21

Of course, your model of computation really does matter. 

Let's go back to the question of sorting, 

because that is a fundamental result that 

you'll probably see quoted several other times, 

this N log N lower bound on comparison based sorting. 

That's actually fairly easy to argue 

and it's related to the sort of puzzles you 

might see sometimes in the world of 

recreational mathematics involving 

coin weighing problems and balances. 

For example, if I have four coins, 

one of which is heavier than the rest, 

can I determine which one is 

the heavy coin with one weighing on a balance? 

It's pretty easy to see that the answer here is no, 

because the balance can 

only tell you three different things, 

basically less than greater than or equal. 

You have four different possible inputs 

that you have to be able to differentiate. 

A balance that can only reveal three possible states 

cannot differentiate between four 

possible inputs successfully.

Play video starting at :13:12 and follow transcript13:12

You can make this problem a bit more general. 

You could say something like I give you five coins, 

and now one of them is not necessarily heavier, 

but it could be heavier or lighter than the rest. 

Now there are actually 10 different input configurations 

that I have to be able to 

differentiate with my algorithm, 

the first coin being heavy, the first coin being light, 

the second coin being heavy, 

the second coin being light, and so on. 

I would like to now tell 

which coin is the different one and is 

it heavier light with two weighings on my balance. 

Here again, you can argue that the answer is no, 

this is impossible because as 

we mentioned are 10 different input configurations, 

and I need to be able to tell all of those apart, 

that if I only am allowed to use the balance twice, 

that only gives me the ability to 

differentiate between nine different things. 

The first weighing gives me three possible outcomes, 

less than equal or greater than. 

Then in each of those cases, 

I can apply the balance again 

to get three possible outcomes.

Play video starting at :14:12 and follow transcript14:12

There are only nine possible 

signals my algorithm can tell me. 

The algorithm can give me 

less than or less than greater than or whatnot. 

There's only nine possible traces through 

this flow chart that 

my algorithm essentially is a decision tree here, 

and there are nine possible leaves in this decision tree, 

each of which corresponds to 

the algorithm needing to tell 

me something about the output, 

like coin 3 being heavy. 

If I don't have enough leaves here to 

differentiate all of my 10 different input scenarios, 

then two different input scenarios 

are going to end up at the same leaf. 

They're going to look identical to my algorithm 

because they're going to generate 

the same comparison results. 

They're both going to be less 

than less than, for example, 

and so my algorithm won't 

be able to tell those things apart, 

and it will make a mistake on one of those inputs. 

Basically, if you think of 

your algorithm abstractly as a decision tree like this, 

you need enough leaves in 

your decision tree to be able to 

differentiate all the possible inputs 

that you expect to receive.

Play video starting at :15:10 and follow transcript15:10

Following up on that and 

heading more in the direction of sorting. 

Now suppose I have four 

coins that weigh different amounts, 

and I would like to sort them. 

I'd like to order them by weight. 

Again, with only two weighings. 

Again, you can conclude this is impossible 

because my sorting algorithm 

abstractly would have this form, 

it would be a decision tree that has 

two levels of weighings and 

there are only nine possible things 

I can differentiate with such a decision tree. 

There's only nine leaves in the tree. 

I have four coins 

that are all weighing possibly different amounts.

Play video starting at :15:44 and follow transcript15:44

There can be four factorial orderings, 

different orderings of four 

coins that weigh different amounts. 

There's four choices for the first coin, 

then three for the second, two for the third, and so on. 

So 4*3*2*1, there's 

24 different possible input scenarios, 

different orderings of the coins, 

and I have to be able to figure out which one of those is 

the case because each one of those has to 

be reordered differently in order to sort properly. 

I'm not going to be able to 

do that if I only have the ability to 

distinguish between nine different 

cases with my algorithm, 

my abstract decision tree that 

represents my algorithm here. 

This basically leads to 

the full proof of the lower bound on sorting. 

I have N coins and I like to sort 

them and the N coins may weigh different amounts. 

How many comparisons are necessary to 

be able to sort these coins properly?

Play video starting at :16:36 and follow transcript16:36

Well, again, let's think about our algorithm as 

an abstract decision tree that just consists of 

different applications of a balance 

because that's what a comparison is. 

It gives you a less than a 

greater than or an equal result. 

How many leaves am I going to 

have in such a decision tree? 

Well, each decision expands 

the footprint of the tree by a factor of 3. 

After two weighings, I 

have the ability to distinguish between 

nine different input configurations and 

then 27 and whatnot. 

Three to the power of the number of 

weighings is the number of 

leaves I'm going to have in my tree, 

and that has to be at least as large as 

the number of possible orderings I have to distinguish. 

The number of possible orderings of 

N say differently valued coins, 

that's going to be N factorial because N choices for 

the first coin and the ordering and 

then N-1 for the second, N-2 for the third.

Play video starting at :17:27 and follow transcript17:27

N factorial is the number of different orderings. 

N*(N-1)(N-2)(N-3) is a very large number. 

I need a lot of leaves. 

I need three to the number of 

weighings to be at least N factorial to 

differentiate all the possible input orderings 

that I would need to be able to tell apart 

from each other because every single one of those has to 

be reordered differently in order to sort properly. 

Now it's just math. 

I have to have three to the number of weighings, 

be at least N factorial. 

If you take the log of both sides, 

you get the number of weighings has to be 

at least the log base 3 of factorial, 

which by Sterling's approximation is on the order of 

N log N. You know that 

the number of weighings that you have to make, that is, 

the number of comparisons in 

the worst case for any sorting algorithm has 

to be at least on the order of N log N. Famous result, 

and this will have implications down 

the road in many areas beyond just sorting 

because there are lots of say data structures 

that can be used to sort and 

so this lower bound has implications 

on the performance of those data structures.

Play video starting at :18:28 and follow transcript18:28

This is just a little bit about models of computation 

and their implications in 

terms of performance of our algorithms.![[Screenshots/Screenshot 2025-08-25 at 2.45.40 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 2.46.12 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 2.46.31 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 2.49.48 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 2.50.47 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 2.52.20 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 2.56.45 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 2.58.38 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 2.58.47 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 2.59.43 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 3.00.12 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 3.00.20 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 3.00.42 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 3.01.52 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 3.02.02 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 3.02.46 pm.png]]![[Screenshots/Screenshot 2025-08-25 at 3.03.06 pm.png]]