We are all about to become algorithm designers. 

What does the process of 

effective algorithm design entail? 

Maybe a good starting point for 

that conversation is to review some of 

the common objectives that we try and 

satisfy when we build a successful algorithm, 

and that really starts with correctness. 

As you can imagine, it is indeed 

quite important for your algorithm to 

well, to terminate, and also to output what you 

consider a correct or optimal solution 

for the problem at hand. 

Although sadly, even that is out 

of reach in a wide range of situations, 

there are a lot of problems out there that are 

known to be hard for one reason or another. 

Maybe with an optimization problem, 

it could be actually computationally 

intractable to find the optimal solution. 

In a lot of situations, 

you have to be content with the solution 

that is good enough, 

the best you can come up with 

in the amount of running time that you're given.

Play video starting at :1:1 and follow transcript1:01

Another prominent exception here 

might be the case of randomized algorithms, 

which we'll talk about in 

the next module pretty extensively. 

There are a lot of very well known randomized algorithms 

that actually could output the wrong answer. 

Although the whole point there 

is if you design them correctly, 

you can actually minimize the probability of 

that sort of failure down to 

the point where it's almost negligible. 

Even those algorithms can be 

deployed in practice quite successfully. 

Of course, a primary design consideration when 

designing algorithms is you 

would like them to be efficient. 

There are lots of dimensions 

to efficiency that we can consider. 

In this class and beyond, 

we typically focus on running time, 

so we want fast algorithms, 

but you could also try and build 

an algorithm with a small memory footprint.

Play video starting at :1:49 and follow transcript1:49

In a parallel or distributed setting, 

maybe you want to focus on the number of 

processors that you're using or minimizing 

the amount of bandwidth used for 

communication between those processors. 

You could even look at parameters like power or heat. 

I guess those would be 

interesting both at a very large scale and 

maybe even in a very small scale 

setting like on a small embedded processor. 

Lots of interesting objectives you can think 

about in terms of algorithmic efficiency. 

Then one final idea that I would advocate that 

belongs on this list of first class design objectives, 

and that's simplicity and elegance. 

I think there's a lot of benefit that we get by 

keeping these in mind as we design our algorithms. 

If you try and simplify your thought process, 

that not only helps you 

articulate an algorithm more clearly, 

it helps you analyze the algorithm more effectively, 

it helps you implement the algorithm, 

it helps you debug the algorithm.

Play video starting at :2:44 and follow transcript2:44

An often overlooked criteria here, 

but I think it's very important to keep 

simplicity on this list of our top-level objectives. 

Now, another important aspect of 

algorithm design is how you explain an algorithm, 

how do you describe an algorithm. 

I have on this slide two examples of 

simple algorithms for searching 

an array to find an element. 

One of them is linear search where you simply loop over 

the contents of the array and stop 

when you find the element that you're looking for. 

The other one is binary search, 

and this works if your array is sorted. 

This is also a very natural algorithm. 

You look in the middle of the array.

Play video starting at :3:22 and follow transcript3:22

You compare what you're looking for 

to the middle element of the array, 

and then you can, 

after that, restrict your search to either the first 

or the second half of the array as appropriate. 

How would we describe these two algorithms? 

I guess what I just did actually is 

a perfectly valid way to describe those algorithms. 

You can just use regular old text 

or describe them in English prose. 

As long as you're being clear 

enough about the steps of the algorithm, 

that's a perfectly reasonable way to describe algorithms. 

You can also, of course, 

commonly describe algorithms in code 

or probably more commonly in pseudocode, 

which is something that looks like computer code, 

but it's a little more high level 

and a little more abstract, 

and it frees us from some of 

the burdensome administrative requirements of 

many programming languages so you 

don't have to declare variables or things like that. 

It lets us focus on 

the essence of what's important 

in describing the algorithm.

Play video starting at :4:20 and follow transcript4:20

It also keeps our exposition language independent. 

Because if you're writing your algorithms all in C++, 

then when C++ goes out of style, 

then now you have to rearticulate 

them in some other language. 

Keeping things at a high level in 

pseudocode helps you keep things abstract, 

but still in enough detail so that you could 

easily translate things into 

an actual programming language. 

Now, as an interesting note, 

I've written on the slide here, 

I've been a little bit sloppy maybe in how I've 

described a binary search in particular. 

I might say, "restrict 

the search to the first half of the array." 

You might say, well, if N, 

the size of the array, is odd, 

then it doesn't really make sense to talk 

about half of the array or something like N/2. 

This is actually pretty common.

Play video starting at :5:8 and follow transcript5:08

When we describe algorithms 

in the interest of simplicity, 

we usually tolerate a little bit 

of what you could call sloppiness. 

We generally try and describe things 

on simple terms at a high level and keep them 

uncluttered with low level details that are presumably 

not super important for 

the high level analysis of the algorithm. 

I don't want to worry about what happens if N is odd. 

I have to round up or down when I take N/2. 

Presumably, whoever is implementing 

the algorithm can work out those details pretty easily. 

I think it's much more important to be able 

to articulate things on simple terms. 

Usually when we talk about algorithms, 

we'll say things like "half" or 

N/2 with the implicit understanding that, yes, 

when it comes time to implement, 

there's a few other low level 

details that we'll have to sort out, 

but we'd like to just keep the exposition, 

at least, at a high level.

Play video starting at :6: and follow transcript6:00

Now, while I have your attention on these two algorithms, 

this is a good point to mention 

that algorithm choice really does matter. 

If you're searching an array of size one billion, 

for example, then linear search 

might have to search through 

every single element in the array. 

It might have to take up to a billion steps. 

Whereas binary search is actually much more 

efficient because binary search, in each step, 

it basically reduces the effective size 

of your problem by half. 

You start with a problem of size N, 

then you move to a problem of size N/2, N/4, N/8. 

This is actually a really common 

phenomenon that we'll see 

again and again when we study 

many different algorithms and data structures. 

Anytime you have an algorithm that effectively 

reduces the problem size in 

a multiplicative fashion at each step, 

that algorithm is only going to take 

a logarithmic number of steps.

Play video starting at :6:53 and follow transcript6:53

We can say that binary search is 

going to require log base 

2 of N steps before it zeros in on the answer. 

Even if N is a billion, 

log base 2 of N is only 30. 

Here you can see there's a rather profound difference in 

the running time and the number of 

steps required for each of these two approaches, 

which really does drive home the point that 

choosing the right algorithm 

really does make a big difference. 

We've been throwing around the word 

algorithm already quite a bit, 

and given that this is a class in algorithms, 

it would perhaps be remiss of me 

to not even attempt to define what an algorithm is. 

Let's close our short discussion here with 

an attempt to define the word algorithm. 

That's actually relatively easy to do. 

It's just a well specified set of steps or 

a procedure for solving a computational problem.

Play video starting at :7:40 and follow transcript7:40

I guess informally you could say 

it's just a computational recipe.