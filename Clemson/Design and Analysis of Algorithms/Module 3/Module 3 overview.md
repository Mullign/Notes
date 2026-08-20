[MUSIC] ![[Module 3 overview.pdf]]

Welcome to Module 3, 

where we talk about one of the most important ideas 

in all of algorithmic computing recursion. 

There are a lot of very exciting things 

one can say about recursion. 

It appears extremely prominently in algorithm design. 

There are lots and lots of algorithm 

design techniques based on recursion. 

There are many problems that you can successfully 

approach via recursive solution techniques. 

In this module in particular we're going to 

focus on a technique called Divide and Conquer, 

which we've briefly introduced in the past. 

But in future modules as well 

we'll also see other techniques like 

dynamic programming for solving 

optimization problems that are inspired by recursion.

Play video starting at ::49 and follow transcript0:49

A lot of times recursion gives 

you the ability to simplify 

the process of solving a problem by 

only having to figure out a small part of the solution, 

and to figure out the rest of the solution, 

that involves just solving 

a smaller leftover recursive subproblem. 

You can just delegate a lot of 

the work to recursion in that case. 

I like to joke with my students that 

recursion is a recipe for stress-free living, 

all you have to do is figure out what 

you're going to do in the next 5 minutes, 

and then just recursively 

apply yourself to the rest of your life. 

A silly example of the recursive mindset. 

I guess just don't think about the base case. 

Recursion has a lot to do with mathematical induction, 

a very prominent technique 

for proving things in mathematics. 

For example, if I want to prove 

that four to the N minus one is a multiple of three, 

that's relatively easy to do if I write 

out four to the N as four copies of 4^N - 1, 

and I group them so that I have 

now three copies grouped together.

Play video starting at :1:49 and follow transcript1:49

Three copies of anything 

added up is a multiple three, of course. 

Then what's leftover is 4^N - 1 - 1. 

That's a smaller version of 

the original formula that I was looking at. 

By induction I can claim that 

that must also be a multiple of three. 

Add together two multiples of three, 

you get a multiple of three. 

The core idea behind induction is that if 

you're trying to prove a statement is 

true for some value of N, 

you can assume that it holds for any value 

smaller than N. That helps you bootstrap 

solutions for larger values of N from those arising from 

smaller values of N. Don't forget 

you also need to prove it for base cases, of course.

Play video starting at :2:27 and follow transcript2:27

If you look at this from an algorithmic vantage point, 

what you can conclude is that 

if you're trying to prove that 

your algorithm properly runs and 

gives the right answer on an input of size N, 

you can assume by induction that it will 

give the correct answer on any input of size 

smaller than N. If your algorithm 

makes calls to recursively solve smaller sub-problems, 

you can assume by induction that it 

will get the right answer when it does that. 

Very close connections between recursion and induction. 

What sorts of things will we talk about in this module? 

We're going to focus a lot on 

the algorithm design technique of divide and conquer. 

We will look at methods for analyzing the performance 

of recursive algorithms in 

particular by solving what are called recurrences. 

These are recursively written expressions 

that describe your running time.

Play video starting at :3:21 and follow transcript3:21

We'll learn how to solve those, 

and figure out that your running time is 

N squared or N log N, 

just by eyeballing a recursive algorithm. 

We're going to get a lot of intuition 

and additional tools for 

our toolbox that will help us analyze these algorithms. 

We're going to study a wide range of 

prominent divide and conquer algorithms. 

In particular, we're going to focus in 

one entire lecture on a problem called Selection, 

which is a fundamental algorithm problem of basically 

finding the Kth largest number 

in an unordered set of numbers. 

We're also going to focus on implementation. 

We'll have a coding discussion 

where we walk through the process of 

recursive thinking and recursive coding on 

many different examples related to linked lists. 

We'll have an enrichment lecture, 

as usual, completely optional, also as usual, 

on the subject of the Fast Fourier Transform, 

one of the most famous algorithms of all time, 

also one of the most famous divide 

and conquer algorithms of all time.

Play video starting at :4:19 and follow transcript4:19

This really does highlight well the power of recursion 

and divide and conquer as an algorithm design technique. 

Then finally, we'll have a new homework assignment. 

I like this one a lot. 

It highlights an area of very active study at the moment, 

at the intersection between 

algorithms and the world of game theory. 

We're going to study a problem called fair division. 

Informally sometimes it's called the problem of 

cutting up a cake so that all of 

the participants who get a piece 

of the cake feel like they've received 

a fair size share of the entire cake. 

We're going to implement a 

divide and conquer solution for 

that problem in our homework assignment.

Play video starting at :4:59 and follow transcript4:59

Should be a lot of fun. 

Then of course moving 

forward through the rest of the course, 

we're going to see additional examples of 

algorithms that are inspired by recursion as well. 

Hopefully the tools that we come up 

with in this module will serve us 

well as we move forward and talk 

about more and more 

algorithms through the rest of the course. 

[MUSIC]