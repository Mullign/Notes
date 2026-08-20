[MUSIC] 

In this video, we're going to continue using linearity of expectation to build 

insight into a number of key problems and processes. 

In particular, we're going to talk about a fun sorting algorithm called bucket sort. 

And we'll talk about ways we can decompose large problems into a large number of 

smaller subproblems to improve algorithmic efficiency. 

Maybe a good starting point here is to go back to balls thrown into bins— 

the favorite of probability theorists everywhere. 

So, when we introduced linearity of expectation, we showed that, of course, 

if you throw N balls into M bins randomly, you expect N over M balls per bin. 

Another quantity that turns out to be surprisingly useful in a lot of 

algorithm analysis is looking at the number of pairs of balls that collide; 

that end up in the same bin. 

That's also easy to analyze with linearity of expectation.

Play video starting at ::58 and follow transcript0:58

For example, if you define an indicator random variable X_ij for 

every pair of balls, i and j, that tells you: One, 

if that pair of balls collides or lands in the same bin; then we just want to find, 

by linearity of expectation—the sum of the expectations of those indicators. 

What's the expectation of X_ij? 

That's the probability that two balls collide. 

That's just one over M, because wherever ball i ends up, 

there's a one out of M chance that ball j ends up in the same bin. 

So, each of the expected values of the X_ij's— they're all 1 over M. 

So, how many of those am I adding up? 

Well, that's just how many pairs of balls are there?

Play video starting at :1:36 and follow transcript1:36

That's just N 

choose two: N times N-minus-one over two. 

If you're not familiar with combinations and permutations and 

that sort of notation, I'd recommend maybe taking a quick break to read about those 

because that's a useful concept in the world of discrete math that we do use 

quite a bit in our different analyses. 

So, all we do is we take N choose two times one-over-M, and 

that gives us the total expected number of collisions. 

The formula is N squared over 2M. 

I guess, it simplifies a good bit, 

if the number of bins is equal to the number of balls. In that case, 

you just expect, roughly, N over two total collisions. 

How might this be interesting or useful?

Play video starting at :2:16 and follow transcript2:16

There's actually a famous problem in recreational mathematics that kind 

of highlights the use of that previous calculation. 

It's called the so-called birthday paradox. 

It's called a paradox because the answer is surprising to many people. 

So, the setup here is you have N people in a room and you're wondering, 

"Well, how likely is it that you have a shared birthday among those N people?" 

And, usually the phrasing here is, 

"How many people do you need to have in a room before it becomes somewhat likely— 

like, probability is at least one half that two of the people have a shared birthday?" 

And, the answer here— it's surprisingly small: less than 20. 

We're assuming here, unrealistically, that every birthday is equally likely.

Play video starting at :2:57 and follow transcript2:57

One way that we can look at this is through that previous process. 

We can kind of think of taking the N people in the room and randomly mapping 

them into a set of 365 bins, corresponding to all of the possible birthdays. 

And now, a collision. If you get mapped to the same bin, that's a shared birthday. 

And so, using the same analysis that we talked about before, 

you see that the back-of-the-envelope answer to this question is roughly 

the square root of the number of bins— the square root of the number of days. 

That's the rough threshold at which you start to expect to see collisions 

happening. 

So, if N, the number of people, is just the square root of 365, 

then you expect half of a collision— 0.5 collisions.

Play video starting at :3:43 and follow transcript3:43

So, roughly around that point is when you start to expect to see that first 

collision happening. 

If you go much higher or much lower than the square root of the number of days, 

then you expect either very few collisions or a lot of collisions. 

This is a good back-of-the-envelope calculation to keep in your mind. 

Roughly, the square root of the number of bins is roughly when you start to see 

collisions, 

when you randomly map balls into those bins. 

That actually has a surprising number of applications. 

Imagine, for this course, that to build a quiz, 

I take a question bank of size N—it has N questions in it—and 

I just sample a bunch of random questions from that question bank. 

And, this is maybe not the best way that I could have built a quiz, 

because, normally, if I sample a question, then I want to take that question out 

of the question bank so I don't possibly resample it again.

Play video starting at :4:35 and follow transcript4:35

But, suppose I just sample with replacement— 

I just keep drawing random samples. 

It's not good if I draw a duplicate, 

because you don't want the same question to appear twice. 

And so, roughly, root N is the threshold where you can sample about that many 

elements with replacement from a pool of size N and 

have a decent chance of not seeing any duplicates. 

If you sample more than root N elements, 

then it's increasingly likely that you start to see duplicates. 

So the birthday paradox kind of phenomenon here. 

You can actually flip this on its head and 

estimate the size of the pool from the samples. 

So, imagine you're drawing a bunch of samples from a very large pool, and 

you're remembering the samples that you've seen.

Play video starting at :5:16 and follow transcript5:16

Once you have seen the first duplicate sample—say that's the Nth sample— 

that lets you maybe surmise that the size of the pool was roughly N squared 

because you can kind of use the same logic in reverse. 

When we study hashing later on in the course, the same phenomenon will 

be useful, because, usually, you don't like to see collisions 

when you do hashing. They do happen, but sometimes, in some applications, you want to 

minimize the number of collisions that you're dealing with. 

And, you can actually end up with a collision free scenario when you're 

mapping elements into a hash table, as long as you only very sparsely fill 

the hash table. 

So, if you map square root of N elements into a size N hash table, 

then there's a decent chance that none of them will collide with each other. 

So, we'll talk more about that when we study hashing later on in the course. 

And then, finally, maybe an application from distributed storage in a networked 

environment— 

If you take an object and store it redundantly on a square root of N random 

servers, out of a set of N servers, then by querying, again, a set of square root of 

N random servers, there's a decent chance you'll find the object.

Play video starting at :6:24 and follow transcript6:24

So again, the birthday paradox math tells you this threshold at which 

you balance the storage cost and the query cost. 

—So, a couple of interesting applications of the birthday paradox here. 

We'll actually also use that same mathematics 

in the analysis of bucket sort here. 

There's a reason that we introduced that process at the beginning of this 

discussion, because it will turn out to be a useful part of our mathematical analysis 

in this discussion here. 

So, here, I want to introduce yet another sorting algorithm. 

It's interesting because it sorts in just linear expected time. And, 

the reason we can sort so 

quickly is because we know something about the elements that we're sorting. 

We're assuming that we're sorting elements that are drawn from a known probability 

distribution.

Play video starting at :7:11 and follow transcript7:11

In this case, I'm going to, for simplicity, 

assume that probability distribution is a uniform distribution between 0 and 1, 

but this can be adapted for 

any probability distribution that we care about. 

So, I'm trying to sort these elements. 

I could, of course, do something very crude and very slow, 

like just run bubble sort on all N elements, 

but that would, of course, take quadratic time. 

So, to improve on that, 

what I'm going to do is drop the elements into buckets—into bins. 

Essentially, we're looking, again, at balls and bins happening. 

So, I'm going to divide this range from 0 to 1 into M buckets— 

M bins—that each represent an equivalent sized slice of that unit interval. 

So, the first bins represents all the numbers in the range 0 through 1 over M.

Play video starting at :8: and follow transcript8:00

The second bin represents all the numbers between one over M and 

two over M and so on. 

And when I map— So, I'm going to, in linear time, scan all of my input elements and 

just drop them into the corresponding bin that their value fits into. 

I guess, I could store each bin as either a linked list of values or 

maybe a vector of values. 

It only takes linear time in either representation to drop the elements into 

their respective bins. 

And since the elements are randomly chosen from zero through one, 

this is exactly a situation where I'm just dropping N elements into M bins randomly, 

effectively. 

So, the preceding math that we talked about applies in this situation in terms of 

expected number of balls in a bin or expected number of collisions and whatnot. 

So, now, to sort my elements...

Play video starting at :8:48 and follow transcript8:48

I'm just going to apply something very simple like bubble sort within each bin. 

So, I'm going to sort the contents of the first bin with bubble sort, 

sort the contents of the second bin with bubble sort, and so on. 

And then, just output the sorted contents of the bins in order, and 

that'll output all of my elements in sorted order. 

So, what would be the running time of doing this? 

Let's first do the back-of-the-envelope math where we won't quite do 

the math properly, but it'll at least give us the right answer. 

And then, we'll go back and see how to do the math properly. 

So all we do for the back-of-the-envelope math is we notice that 

we're running bubble sort inside of each bin.

Play video starting at :9:27 and follow transcript9:27

That's going to take quadratic time. In the number of elements in each bin, 

we expect N over M elements in each bin. 

So, kind of roughly, we would expect the square of that to be the amount 

of time we spend in each bin times M bins—M buckets. 

And so, the total amount of expected time that we anticipate spending here is 

N squared over M. 

That actually represents a factor M speedup over the original running time 

of just N squared, if we ran bucket sort on all the elements just directly. 

And so, this is a pretty big deal. 

We have, through this very simple bucketing approach, 

been able to reduce the running time quite dramatically.

Play video starting at :10:7 and follow transcript10:07

If we set the number of buckets to N— that's kind of the right choice— 

that, basically, makes the anticipated running time drop down to just linear. 

We wouldn't want to set it any higher than that, 

because, then, scanning the array of buckets would start taking more than linear time. 

So, this actually is the right answer. 

We do get linear time in expectation, but 

we do need to be a little bit more careful with the math that we're doing. 

So let's maybe switch to the whiteboard and 

do the math a little bit more properly, using linearity of expectation. 

So here's my setup. I have my array of M buckets.

Play video starting at :10:44 and follow transcript10:44

I'm going to go ahead and 

just assume that M is equal to N because that'll end up being the ideal choice. 

And, within bucket i, I'm going to define b_i as a random variable, 

telling me how many elements end up in that bucket. 

So, for example, we've already ascertained that the expected value 

of b_i is just N over M, or, in this case, one because N and M are the same thing. 

If I'm interested in the running time that I expect bubble sort to take when run on 

those b_i elements, the quantity that I really care about here is the expected 

value of b_i squared, because the running time of bubble sort is quadratic in 

the number of elements in that bucket. 

And so, here you might think, "Well. 

Can't I just take the expected number of elements in my bucket—i.e. one—and 

square that to get the expected running time of bubble sort?" 

And, here's where our back-of-the-envelope math wasn't quite right.

Play video starting at :11:38 and follow transcript11:38

It, basically, boils down to the fact that the expected value 

of b_i quantity squared is not, in general, equal to 

the expected value of the square of the random variable b_i. 

So, just to see that phenomenon, 

look at a very simple indicator random variable attached to a fair coin flip. 

So the expected value of x here is one-half. 

If I square that, I get one-fourth. 

If I instead look at the expected value of the quantity x squared, 

x squared is actually the same as x. 

And so, this has the same expected value as x. 

It takes the value one with probability one-half, or 

x squared takes the value 0 with the probability of one-half.

Play video starting at :12:19 and follow transcript12:19

These two things are not equal to each other. 

So, what I really want to care about for my algorithm analysis is the right hand side. 

This term is really the expected running time of bubble sort 

when applied to the b_i elements in my bucket, i. On the left hand side, 

that was the number that we had kind of used in our back-of-the-envelope analysis. 

And so, that's kind of where our back-of-the-envelope analysis wasn't quite 

technically correct. 

So what I really want to analyze is the expected value of the quantity b_i squared. 

How do I get a handle on that, 

the expected value of the square of a random variable?

Play video starting at :12:54 and follow transcript12:54

So, what I'm going to do there is actually take a look at b_i choose 2. 

So, that is the expected number— 

If I look at the expected value of that, that's going to be the expected number 

of pairs of elements that end up in bucket i— Or, equivalently, 

the expected number of collisions among those elements that end up in bucket i. 

And so, how can I analyze that?xxx 

Well, b_i choose two, as we all know, is b_i times b_i minus one over two. 

I guess I could rewrite that as just one-half of b_i squared minus b_i. 

That has a b_i squared in it, so, if I rearrange these terms to solve for 

b_i squared, I get that b_i squared is going to be equal to, 

if I can do my math correctly, twice b_i choose 2 plus b_i. 

And so, now, I've rewritten b_i squared in maybe a more convenient way.

Play video starting at :13:54 and follow transcript13:54

So, if I'm interested now in the total running time of all of my bubble sorts, 

I'm interested in what's the expected value of the sum of all of the b_i 

squared's. 

That's my total expected running time. 

By linearity of expectation, I can add this all up and I'm going to get that 

that's going to be twice the expectation of the sum of all of the b_i choose 2's, 

plus the expected value of the sum of all of my b_i's. 

The sum of all the b_i's— that is otherwise known as N, 

because that's just the sum of all the elements in all of my buckets. 

So, at the end here, I just have a plus N term. 

What about the sum of all of the b_i choose 2's? 

That's also a quantity that we have conveniently already analyzed in 

this discussion.

Play video starting at :14:46 and follow transcript14:46

That is the total number of collisions over the entire table. 

And we showed that that was roughly N over 2 if M and N were the same thing. 

And the twos here are going to cancel. 

So both terms contribute roughly N. 

And so here, the expected total running time that we spend for 

the entire bucket sort algorithm is just roughly 2N, order N. 

So, that's the end of our analysis. 

The core idea behind bucket sort is actually quite general and quite powerful— 

the idea that you can often take a large problem and 

divide it up into a substantial number of minimally interacting pieces that you then 

process individually.

Play video starting at :15:27 and follow transcript15:27

This, of course, also shows up a lot in parallel computation, 

where you're often looking for ways that you can carve up a big problem 

into independent subproblems that could be processed in parallel. 

The mathematics here is usually straightforward to do in a 

back-of-the-envelope fashion, and it usually results in a pretty dramatic speedup. 

For example, with bucket sort, instead of spending quadratic time on 

the entire input, you can divide things up into M pieces and 

spend quadratic time on every piece, and that gives you a factor of M in speedup. 

This approach is also related to maybe the algorithm design approach of divide and 

conquer that we'll talk about extensively in the next module, the only main 

difference probably being that divide and conquer, as more of a recursive approach, 

would then further subdivide the pieces as it continues to solve things recursively. 

Here, we're more talking about like just a one level decomposition of 

the problem into big pieces that you then just solve individually. 

Maybe as just one more example to highlight how this can be effective, 

consider that you have N points in the two dimensional plane, and 

you'd like to find the closest pair of points. 

This is a classical problem in computational geometry.

Play video starting at :16:34 and follow transcript16:34

We know many good algorithms for solving it relatively efficiently. 

But imagine that in a common use case here, 

the points are kind of uniformly spread out, say across a unit square. 

So, one way we could approach this is we could impose a grid on our points 

—say a square root of N by square root of N grid— 

That would give us N grid cells. 

And, if our points are indeed uniformly spread out, that means we basically have 

N balls that we're mapping into N bins, again, uniformly at random. 

So, you'd expect exactly one point to land in every grid cell. 

And so the algorithm here would be, basically— Instead of comparing every pair 

of points—which would be quadratic— you would only have to compare every point 

locally to the points that land in its grid cell— and maybe the neighboring grid 

cells, just in case the closest pair happens to straddle a dividing line. 

And that can be quite a bit faster.

Play video starting at :17:27 and follow transcript17:27

If you basically go through a similar analysis 

—almost the same analysis that we did with bucket sort—you reach the conclusion that 

this will take just linear expected time, because every point only gets compared to 

a constant number of additional points in expectation, 

compared to the quadratic time that you would have with the brute force algorithm. 

So, a substantial speedup that you get from this sort of idea of large scale 

problem decomposition into mostly independent smaller pieces. 

[MUSIC]![[8OyD5R4eR2WfCCsHhmjIQw_370800f786aa4251a4b292d2ae542cf1_Bucket-Sort.pdf]]![[screenshots/Screenshot 2025-09-05 at 3.07.13 pm.png]]![[screenshots/Screenshot 2025-09-05 at 3.07.22 pm.png]]![[screenshots/Screenshot 2025-09-05 at 3.07.31 pm.png]]![[screenshots/Screenshot 2025-09-05 at 3.08.13 pm.png]]![[screenshots/Screenshot 2025-09-05 at 3.08.34 pm.png]]![[screenshots/Screenshot 2025-09-05 at 3.08.47 pm.png]]![[screenshots/Screenshot 2025-09-05 at 3.09.25 pm.png]]![[screenshots/Screenshot 2025-09-05 at 3.09.51 pm.png]]