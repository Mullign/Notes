![[../Module 2/p0j6pK_OQLSCoRQn4n9aiA_0f3b5c90b06d42829c162b241f2e83f1_Optional-Enrichment-Lecture---Cache-Oblivious.pdf]]![[subtitle (1).txt]]
[MUSIC] Welcome to our first
enrichment lecture. These are completely
optional in terms of what you're expected to learn from the
course content. I thought it
would be nice to include a little
bit of fun, advanced material to show how what we're learning in our current
module can be extended in ways that have interesting impact both in theory and in practice. Today, we're
going to focus on what we could call memory conscious models
of computation. How do we design
algorithms and data structures with a closer eye on
memory usage. So the starting point maybe of our
discussion here is our standard RAM
model of computation being very oversimplified
in terms of memory. It basically assumes that every memory access takes constant time, full stop. And that's quite
inaccurate in some ways. If you look at real
world memory systems, memory access can not only take a huge amount of additional time beyond
other operations like just adding two
numbers together, but also how you
access memory really does matter in terms of
caching, for example. If you imagine
for a second that your main memory is
divided up into blocks, which is often the case, then as suppose you scan through memory
sequentially, The first element
in one of the blocks that you hit, you're going to
transfer that block into a faster
cache memory and subsequent access
to elements in that block will
therefore be much faster. Then when you cross a
block boundary again, you might have
cache miss and transfer the next block into your cache memory. But then subsequent
accesses within that block are
again much faster. Access patterns
that sequentially scan through
memory or that have locality of access where
you're accessing nearby elements to elements you've
accessed before. That's usually
much faster than an access pattern
that jumps around haphazardly
throughout memory. And often hits blocks
of memory that you don't yet have in
your cache memory. Real world memory systems, two features of them. A lot of times your memory is segmented into
these blocks. Maybe think of
1K, 2k, 4k, age sizes would be typical maybe
for these blocks. Memories are
also organized in hierarchical stacks. You have a cache memory that's very fast
and somewhat small. You've got your
main memory, which is much larger, but also much slower
to access. If you're looking
for an element that's not in
the main memory, maybe you have
to go to disc. Which is much larger still, but
substantially slower. We're talking
possibly orders of magnitude slower. As you walk down the different levels of this memory hierarchy, Typically, when you
access an element, say from a main memory that's not in the cache, you don't just
transfer that one element
into the cache. You transfer the
entire block from main memory into the cache that contains
that element. You have a hierarchical
memory with block transfer
between the levels. Knowing this about the way memories
are organized, how can we now design
algorithms and data structures to fine tune their
performance accordingly? One application we
have talked about in this module is
representing a matrix in memory. We've talked about
how to store it row by row in row major order
or column by column in column
major order. If we want to think about how the indexing works, maybe it will be convenient to
think of an n by n matrix where n
is a power of two, just for simplicity. In that case, there's a really nice way
that you can compute the index of an element within the overall
memory buffer. Using the index of its
row and of its column. If you're dealing with row major format,
row major order, then the overall index of an element within the full memory
buffer holding the matrix is just
the concatenation of the binary number representing the row and the binary number
representing the column index
of that element. Vice versa, if
you're storing an element if you're storing things in
column major order, Then the index
of an element in the matrix is given by the concatenation of the binary number
representing its column and
the binary number representing its row. Not too hard to see that. Like in row major order, your row is the
high order, it consists of the high order
bits of your index and the column is
the low order bits. Makes sense because if you're storing things in row major order
and you walk around within
the same row, only changing your
column index, you're only changing
the lower order bits of your memory address. That's pretty
cache friendly. You're only moving around locally to nearby
addresses. But if you are storing a matrix in row
major order and you walk around up
and down in a column, That's maybe not so good because now you're
actually changing your row index and that's the high order
part of your address. That's making a more
substantial change. That's causing you to jump around quite a bit and that might involve a
lot of cache misses. This actually suggests an
interesting question. What if you have
an access pattern in your matrix
that moves around locally both within a row and within a column? It seems like neither of these two
representations would be ideal by itself for
that access pattern. Could there be a
different access pattern that maybe is
more equitable in terms of or more
balanced in terms of the attention
that it pays to both rows and columns? Yes, there is one.
Interestingly, what you get the way you get
it is by taking the binary representation
of the row and the binary representation
of the column and actually interleaving those two binary numbers to get the index at which you would
find an element in the memory buffer that stores the entire matrix. This, as you can see, pays more equal attention to both the rows
and the columns. If you are at a
location and you move around that location
by changing your row and your
column index slightly. In either case, you're
only changing of the low order bits of your index in the
memory buffer. You're not actually moving that far in memory. This might still be
relatively cache friendly. What does this actually
look like in terms of how the matrix is
being serialized? There's actually a nice
picture behind it. So you could
actually say this is a representation of your
matrix by quadrants. You take the matrix, you divide it up into
four quadrants, and here we really do
want to assume that the matrix is square and that it size
is a power of two, so this works out nicely. You divide the matrix
up into quadrants, and then you
just write out in memory, the
first quadrant, the upper left, the
upper right, lower left, and lower right as
the four big chunks of the matrix in memory. Then you proceed to recursively subdivide the quadrants in
the same way. The top left
quadrant here, I've subdivided it into quadrants and
represented them in memory as well. This is pretty
much identical to data structure
for storing two dimensional
data called a quad tree that you might have heard of and
that we might touch on later
in the semester. It basically divides
two dimensional data up into quadrants and then further recursively subdivides those quadrants and then subdivides
and subdivides. It's a recursive spatial subdivision of our data. And that does,
indeed correspond to this interesting bit
interleaving pattern. Just, for example,
if you look at the four big chunks that represent our
matrix and memory, the high order bits of those chunks would
necessarily have to be zero zero, zero one,
one zero, and one one. If you look at
the four quarters that represent our
matrix in memory. If we just look
at one of those, like the yellow chunk,
all the addresses in that chunk
start with 01. That makes sense
because that's the upper right quadrant with all of the rows
in that quadrant, they start with the
high order bit of 0 because they are
the first half of all the rows. All the columns in that quadrant start
with 1 because they're the second half of all of our columns. If you interleave, you have addresses that
start with 01, and that makes sense with the picture
that we've drawn. I think this just
highlights the fact that you can store data in many
different ways, some of which
may be more cache friendly than others. This question extends to many other
different domains. Maybe I have data that is structured
according to a graph or a network organizational
structure. And you'd like to
know how it should be stored in memory to
be cache friendly. That might entail
taking this graph, this network and
ordering the nodes of the graph to
store them in memory in some sequence. How do I optimally
sequence the nodes of a
network so that nodes that are connected tend to be near each other?
Because what you typically do
with algorithms on graphs and
networks is you walk around locally from one node to another following
these connections. What's a good way to sequence these
nodes in memory? That preserves
this kind of locality. This is related to lots
of questions about graphs and
networks related to maybe visualization. If you'd like to draw
a nice embedding of your graph in one
dimension or maybe two dimensions so that nodes that
are connected end up nearby each
other in that embedding, very
similar question. We'll actually touch on these specific
questions later in the
course when we talk about graphs
and networks. There are some very
elegant techniques you can use to
address them as well. So let's work
towards maybe a more concrete model of computation that is a little bit more
memory conscious, that takes memory
access into account, and it's a little bit more realistic
in describing the performance of memory-bound algorithms and
data structures. Algorithms and data
structures where the memory
component is really the dominant part of
the running time. For simplicity,
we're going to consider just a two
level memory system, cache and main memory. Again, these are segmented into blocks of size B, and the cache has a
total size of M. It has M over B blocks of size B that fit
into the cache. Now, again, we're going to do block transfers. If you access
an element from main memory that's
not in the cache, the entire block
containing that element will be
moved into the cache. And we'll talk in just
a second about some of the fine details about when you move something
into the cache. Another page has to be evicted from the cache, which one do you evict? There's a little bit of fine print that we
need to get through. But the interesting
thing here is your running
time is now basically only
concerned with the number of block
transfers from main memory to
cache. That is it. That's all. You don't even worry about things
like additions, multiplications,
comparisons, all those other operations that in the RAM model
took you constant time. Those are treated
as being free now. Because we're
assuming that we're looking at
an algorithm or a data structure for
which memory access really defines
the performance. Here your performance
really just boils down to how many pages are transferred
to the cache. That's it. It's a very simple
outlook on running time. All you count is
page transfers. That's all. Cache misses. And that is your
running time. How can we design
algorithms and data structures
that perform well in this setting? First thing,
let's go through a little bit of
the fine print because with real
world caches, we do have a couple
of assumptions we need to sometimes make. One that may not
come to mind, but it actually
is sometimes a constraint of
actual hardware. We're going to assume just for simplicity that our cache is what's
called fully associative, which means that
a page from main memory can actually be placed anywhere
in the cache. Sometimes because of
hardware constraints, a page from main
memory can only be placed in certain
locations in the cache, but the fully
associative assumption is not a terribly
bad assumption. That simplifies
things a little bit. We also need to
think about the cache page
replacement policy. Whenever you bring a
page into the cache, you have to evict an existing page
from the cache. How do you pick the
page that you do evict? We're going to
make a somewhat unrealistic simple
assumption here that we use what's
called an ideal or an optimal page
replacement policy. Basically, we
assume that we have a crystal ball and
that we will be evicting the page that is needed it's going to be accessed the farthest
away into the future. It's the least pressing. If you look at all the
pages in our cache, you can with our
crystal ball, say, this page is going to be accessed pretty soon. I want to keep
it in the cache. But this page, it's going to be a long time
before I need it. Maybe that's
safe to evict. That's o that is actually the optimal thing you
could do with a cache. Of course, most
people don't have a crystal
ball where you can predict that information about your cache pages. In practice, you
typically use a page replacement policy that's much simpler. I've listed two common
ones on the slide. Here are the least
recently used or first in first out page
replacement policy. Those are basically what the acronyms suggest
they should be. Those are common page
replacement policies you might find in a
real world system. It turns out that if we make this assumption of an ideal page
replacement policy, that doesn't affect
things too much. It basically means
you kind of experience in most systems a
constant factor slow down based on what you would actually
see if you were using an LRU or a FIFO cash
replacement policy. In particular, if
your running time on an ideal cache only slows down by a
constant factor when you have the
size of the cache, then the running time on an ideal cache will
still be within a constant factor
of what it would be on an LRU or a FIFO cache.
You can prove that. I won't go through
the details of that. But basically,
these assumptions are not terrible to make. They'll still give you pretty reasonable
performance estimates. It's pretty safe to ignore all the content
on this slide, just wanted to go
through a few of those lower level details for those who might
be interested. Okay. Now let's think
about how to design good algorithms in this two level
memory system. Now we have to think
about the performance in terms of how many pages are transferred from
main memory to cache. We can actually design algorithms that
are fine tuned to get the best
possible performance knowing the parameters
of our cache. The main parameters are M, the size of the cache, and B, the block size. And so we call an algorithm
cache aware if it tunes its
performance based on knowledge of these
two parameters. For example, if we look at the world's
simplest problem, that is searching a
sorted length in array, and that's what
we started out by learning binary
search to do that. It turns out that
the optimal number of page transfers you
can hope to expect, you can show is
log base b of n [log_b n], where the block size
is part of that bound. That's the best
you can hope to do. One can prove that. Interestingly,
regular binary search does not achieve
that bound. We'll see why in a second. Binary search and that
makes sense because binary search isn't using the parameters
of our cache. It's not using M or B
in any meaningful way. It's just doing what binary search normally does. But you can actually
generalize binary search to a multi way
search that uses the block size in
an informed way and actually does achieve this optimal number
of block transfers. Let's look at
binary search and generalizations
thereof. So with normal
binary search, same algorithm that
we're familiar with, you look at the
middle element of your sorted array and you recurse
left or right. Every single step
of the algorithm is essentially having the size of the sub array that we're now
considering. Eventually, if you think about
how that works, pretty much every
access that binary search
makes is hitting a new page because you're jumping around by quite
a large distance, usually as you're
running the algorithm. But eventually,
binary search will narrow its focus to a sub array that
actually finally fits within a single
block in your memory. At that point, everything
else is just free. Because remember that
only block transfers count towards your
running time. The rest of the
binary search, the part that
happens within a single block costs you zero. It's
completely free. To figure the
running time of binary search in this new model
of computation, all you need to
do is figure out how many steps does
it take to get from your original
problem of size N down to a problem
effectively B, your block size,
because at that point,
everything is free. So, and you imagine that every step
along the way is hitting a new page in your cache and causing a memory transfer
until you get to the block
size B and then everything is free from
that point onwards. How long does that take? Well, you're reducing by a multiplicative factor of two from n down to B, that takes log of n
over b [log (n/B)] total steps. A log of n over b, that's log of n minus log of B. That's actually
not so great compared to the optimal bound that I
just mentioned. In a perfect
world, the best you could hope to achieve
is log base b of n, which is actually log of n
divided by log of B. That's a much
better bound. That's many fewer steps, many fewer block
transfers than log of n just minus log of
B. Binary search, just vanilla
binary search by itself is not great, it's not optimal compared
to what you could potentially achieve in
a cache aware setting, that makes sense
because binary search isn't doing anything with the parameters
of our cache. But what if you did
try and customize binary search
with knowledge of your block
size, for example. Here's what you could
do in that case. Just in order to fit
things on my slide, I'm taking B equals two, very small block size you can hold two
elements in a block. I've divided up my array
now into two pieces, but three pieces with two delineating
elements, and I'm going to store those two
delineating elements in a block because a block can hold two things. Imagine these two
yellow elements, 13 and 31 stored
in one block. With one memory transfer, I can pull in that block. And figure out where
the target element I'm searching for lives. Is it less than 13? Is it 13-31? Is it
bigger than 31? With just a single
block examination, I can figure that out. Now I've effectively
reduced my problem down to a third of the original
array in size. I know which of these
three blocks of size n over three I
now belong to, and I can continue
recursively repeating the same process within those blocks. You can imagine this makes a substantial amount of progress if your block
size is really big. Typically b
is like 1,000 or something of that
order of magnitude. In that case, your yellow block here at
the high level. Is going to have
1,000 numbers in it, and you're going to from that one block
examination, be able to effectively jump to a sub problem of size that's 1000th of
the original array. You make a much larger
rate of progress here, you're instead of dividing by a factor of
two in each step, you're dividing by a
factor of b plus one, which is much faster. If you continue
this process, you actually build
something that in data structures we
know as a B tree. It's a tree with a
branching factor, I guess, of a technically B
plus one because every node here holds
B elements of data. And so that
delineates between B plus one branches. In this case, we basically take
the contents of our original sorted
array and we store it in memory in blocks as
the tree suggests. Here, if you want to find your way to any
element of data, you only have to look
at three blocks, the yellow block
at the up top and then a middle level block and then a block
at the bottom. Only examining three
blocks in total. And it turns out that
this is optimal. This only takes
log base b of n steps. Why is that? Well, basically
the depth of this tree is log
base b of n? I guess it's log
base b plus one of n because every
step down the tree, you have a branching
factor of b plus one, and so the footprint of the number of active nodes in the tree grows by a
factor of b plus one, every single level you
move down in the tree. The depth of such a
tree is on the order of log base b
plus one of n, which is the same
asymptotically as log base b of n. So this is optimal. This is an optimal
algorithm for searching a sorted array
in the cache aware setting where we're
allowed to look at the cache parameters
and design a memory layout
for our data that behaves optimally in terms of the number
of blocks we have to examine in order to
find a target element. Now we get to the
interesting part because these parameters, M and B, the parameters
that define our cache. They're sometimes
hard to know. They’re system
level parameters. They might be different in many different systems. It might be hard to find those parameters on
any given system. Moreover, in a multi
level memory system with several levels
of memory hierarchy, the parameters might
actually be different for different levels of
the memory hierarchy. If you tune your
algorithm to a block size that's
good for your cache, it might not be
good for the memory to disc interface. So this presents a couple of messy
challenges. How are we supposed to
design or fine tune or algorithms now that it might be hard to know
these parameters. This leads to
what I think is an extremely elegant
model called the Cache Oblivious Model. So an algorithm, we
call it cache oblivious if it does not know the parameters M and B
of the caching system, and yet its performance
is still within a constant factor
of what you would be able to
achieve optimally, were you in a cache
aware setting? A cache oblivious
algorithm doesn't know M and B, but yet it still
comes within a constant factor
in terms of page accesses of what you optimally could
have achieved had you known M and B. It's a cool idea. Just to give you a
really basic example, suppose you want to
reverse an array. A very common way you
do that is you start at the two endpoints
of the array and you work your
way inwards. You're scanning inwards
with two pointers and swapping the
elements as you go. That will reverse
the array. That is essentially
just doing a sequential scan
through memory, which we know is about the most optimal
thing you can do from a cache
perspective. That's going to do n
over B block transfers because you're just
scanning sequentially through your n elements. That's the best you
can hope to do for any algorithm that
reverses an array. There's nothing
magical about what the optimal solution
is in this case. Your algorithm for
reversing an array, it actually
didn't explicitly know or make use
of knowledge of B, and yet it still
is achieving what would have been
the optimal bound had you known B. This is a very trivial
example that just illustrates how you
can be optimal, even though you don't know the parameters
of your cache. One nice thing about this is if you now look at these multi level
memory hierarchies, if I go back all the
way to the beginning to our discussion about multi-level
memory hierarchies, Remember that our model for cache
obliviousness only looks at the two level
memory hierarchy model with just a cache
and a main memory. If we're within a
constant factor of optimal for a two
level memory system, not knowing the
parameters of the cache, then that would
hold actually for every single
consecutive pair of levels in our
memory hierarchy. We're within a
constant factor of optimal for every one of those because
our algorithm doesn't really depend on the cache parameters, whatever they
are, we're within a constant factor
of optimal. As long as our
hierarchy has only a constant
number of levels, and as long as you're only losing a constant factor relative to optimal for every consecutive
pair of levels, you're still losing
only a constant factor across the entire
memory hierarchy. This means that
if you design a cache oblivious
algorithm, You only need to
worry about a two level memory system for the design and
analysis of the algorithm, but applied to a more general
hierarchical memory with a constant
number of levels, you're still only
going to be losing a constant factor in
performance relative to what you could
have optimally achieved had you
finely tuned the algorithm based
on the parameters of every single level
worth of caching. Okay. So cache oblivious
algorithms. It's an interesting
world now because for almost every algorithm and data structure
problem out there, you can now ask, well, can I solve it in a way that is cache oblivious? That's really
not an obvious question to answer
in many situations, even for simple problems. It turns out that for a large number
of problems, the algorithms you would learn in a class like this one are actually
not cache oblivious, even for simple
problems like searching a sorted
array or sorting, your standard algorithms, we already showed that binary search is not
cache oblivious. It doesn't use the cache parameters in any
meaningful way. Also, your
textbook sorting algorithms that
are really fast like merge sort and Quicksort, they use a number of
block transfers that is not actually
optimal according to what you can prove
as an optimal bound. You actually have to think very deeply
sometimes about how to build cache
oblivious analogs of algorithms for these
standard problems. This opens up an entire world of
additional problems, building cache
oblivious versions of standard algorithms. For the rest of
today's discussion, I just want to talk
about the simple problem of how to make binary
search cache oblivious, how to search
a sorted array in a cache
oblivious fashion. I'll try to describe this maybe two
different ways. Remember that
we did show how to achieve the
optimal bound on the order of
log base B of n in the cache aware model, where we built
essentially a B tree. But this memory layout for our array requires
that we know the value of B because we
need to know how big the blocks
are so that we can lay out this tree
and store elements of data in these
size B nodes. What if you don't
know B though, how do you build this
tree in that case? That's what we're going to try and attempt to do. We're going to try and achieve log base B of n memory transfers
on the order of that, but without
knowing B. To start with,
I'm going to do something similar to
what we did before. I'm going to build
a tree effectively, a hierarchical
decomposition of my array that has a tree like
structure to it. I'm going to
divide the array in this case up
into blocks. Each block is
going to have size square root of n, and there will be square
root of n of them. And I'm going to be a bit fast and loose
with constants here, things being rounded up, things being rounded down. Imagine that there's root n blocks of size root n and the elements that
delineate the blocks. I'm going to
elevate them up to a higher level
block here, and that's going to
have size root n, that's also going
to basically be a sorted sequence
in and of itself. Here I have a
high level block that's a size root
n sorted sequence, and the elements
of that block delineate these
lower level blocks, each also of size
root end that are themselves also
sorted sequences. This is just a two
level B tree with a branching factor of
root n. Using this, I can reduce my
original problem of finding a target
element in a sorted array of size n. I can reduce that to two sub problems
of finding a target element in a sorted array of
size square root of n. I first look at the yellow root block here. That is a sorted
array of size root n, and I will search
through that to find where my
target lives, and then that
will point me to a lower level block, also of size root n, that is also a
sorted sequence. I basically now
have to just do two searches in
sorted sequences of length root n. N to the one half. To solve
my original problem. If everyone's
happy with that, now is when things get interesting because
I'm going to do the same process
recursively within those blocks. Here I have a
whole bunch of sub problems of
size root n. I'm going to
now proceed to decompose each one of those the same way
that I have done this. Each one of these
blocks of size root n is going to
get decomposed, so it looks like
this picture. It's going to have a
high level block of size root of root of n and lower level blocks of size root of root of n. What that is
effectively going to do, each one of these
blocks now gets decomposed into a
two level hierarchy. In total, I now
have four levels in my tree that
I'm building, and each sub problem
now is size root, root, n. N to the
one fourth. It's convenient that the four and the
four match here. Then as I continue my recursive
decomposition, one more level
of recursion and now I have
eight problems of size root root root
n. N to the one eighth. Again, it's nice to see that the
eight and the 1/8, the eight is in common
between the two of those. We'll use that a second. But that is my
decomposition. I would like to
represent in memory the structure of my elements this
way, basically. I'm going to decompose
things this way. What do I mean by
that? Let's be a little bit more precise. In my original
decomposition, what I'm going to do
is I'm going to store this top level block
first in memory, and then I'm
going to store the lower level blocks. And then for the
top level block, that's the thing
I'm storing first. I'm going to now think, In storing that block, I would like to
actually store the recursively
decomposed version of that block. Instead of storing
that block is just root n element, I'm going to store what recursion would have me store for that block. In memory, I have
the first block representing the
high level block, and then the low
level blocks. Those blocks of memory
are then further recursively rearranged according to this
same process. Okay. Remember that when binary search
reaches the point where you have
a sub problem of size less than B, everything else is
free at that point. Even though this decomposition
keeps going down until we have a base case of essentially
single items, you can mentally think
of the process as stopping when you reach a sub problem of size B. When your decomposition
gets down to little sub problems
of size B, then yes, they are being
further decomposed, but at that point, everything fits
inside a block and everything from
that point on is free. It's as if your
decomposition stops at that point
for performance analysis purposes. And all you
want to know is how many sub
problems exist once the decomposition has reached that point. Because that's
the number of blocks you effectively
have to look at. Each subproblem fits in a block at that point. And so the number of sub problems
is the answer. It is the number of blocks you're
going to have to examine along the way towards searching for
your target element. So now we just have to figure out what this trend
looks like. We have n to the one half, n to the one fourth,
n one eighth. Eventually, that
gets down to n to the one
over something, which is let's just say that's B, that's
the block size B. That's when the
sub problems reach our target
block size. We know that
the one eighth, the eight is the same here as the eight sub problems. Whatever this exponent is, the question
mark is the same as the question mark here. That actually
lets us solve for the question mark, and it actually solves
two blog base b of n, which is what we want. We end up with at the level where
the decomposition reaches the
block size of B, we have exactly
on the order of log base B of n
sub problems, I.E., that many blocks
that we have to visit in order to
find our answer. That is one way to think
about how to build a cache oblivious version of binary search, I guess. This maybe also
highlights why building cache oblivious
algorithms is maybe not the easiest
thing in the world because this is about the simplest
problem you can think of. Searching a sort array, and even that is not exactly trivial in
terms of how to build something
that's cash oblivious in this setting. For those of you
who are wondering, well, this is a little
hard to picture. It feels like there's
a tree happening here with all this recursive
decomposition. Let's maybe look at maybe another viewpoint of the same process
that maybe highlights the structure
a little bit better. If we think back
to binary search, a common way that we think about binary
search from a data structure
perspective is as a binary
search tree. You take the middle
element of your array, that's the root of the tree, and
then recursively, the left and the
right sides are then also built into
little binary trees, where the middle
element is the root of those subtrees
and so on. You can think of the
binary search process as the process of
starting at the root of your binary search
tree and going left or right by comparing against the target element that
you're searching for. If I'm searching for nine, I start at the root, I go left because
9 is less than 12, it's bigger than 5, it's bigger than 8. I just walk down
the tree and that's how I
find something. And the height of the
tree is the number of elements I have to
examine along the way. The number of comparisons
I have to make. In this case, I
guess I have to look at four things walking
down the tree. What if I have the ability to pack elements
into blocks? What if I have a
big block size? What I could do is maybe represent my
binary tree in memory as indicated by
these yellow blocks, basically, super
nodes, effectively. If I have a block
size of three, then I can maybe fit what were originally
three elements, three nodes now into
the same block. And so I can
actually store my tree as these yellow
blocks in memory. Now the nice thing is, walking down to find an element with the
same process as before, only has to pull two
blocks from memory. It's going to have to examine the root block and then one of the
lower level blocks, and that's all. Instead of visiting
four nodes along your path from the
root down to a leaf. Now you only have to
visit two blocks. We've built a higher
branching overlay on top of our original
binary search tree. You could think
of this as also a b-ary tree of
some sort where each block now
has a branching factor of four, I guess, because that
top level block now has effectively
four leaves that are each roots of the lower level
blocks below you. And we can actually do this process in general. If we take abstractly, suppose you have a
complete binary tree. Here's a binary tree. If you have n leaves
in your binary tree, then the height of the tree is
going to be log n That's a pretty
well known fact. If you have a
height of log N, then, well, actually, it's easy to see that
that leads to having n leaves because every
step down the tree, you're doubling the
footprint of the tree. And so the total
number of leaves at the bottom is going
to be just two to the power
of the height, two to the power of log n. And that is synonymous
actually with n. Another nice
trick with logs is you can take the
two and the n and just swap them
and you get n to the log base two of two,
which is n to the one. What if I cut a tree
in half height wise? I draw dividing line at the halfway mark
in terms of height. How many leaves do I
have at that point? At that point, I've only
been able to double my footprint for
one half log n levels of the tree, and the number of
leaves I get at this halfway point is two to the one
half log n. That is synonymous with square root of n.
N to the one half. I can again swap the
n and the two here, and you get square
root of n. This showcases a
decomposition very similar to what
I did before. Remember that earlier
I took my array. I divided it up into square root of n blocks of size square root of n, and then I had a
higher level block that had square root of n, those delineation points, square root of
n things in it. That's exactly what
I've just done. I've taken this
binary search tree that normally would
have n leaves and a height of log N, and I've divided it up
into a high level tree of half of log N and height with
root end leaves. Those leaves are
like the roots of these root and lower level trees that themselves also have
root and leaves. That's roughly
the decomposition that I had before. It's just may be viewed maybe a little
bit differently. If I want to store
my tree and memory, I first store the
top level tree. That's the first thing
I store in a block of memory and then
I store the low level trees
following that. And then now I'm
going to apply again, recursion to decompose
those objects. The high level tree that I stored first in memory, I'm going to now
further decompose it, divide it in
half heightwise, to a high level tree followed by low
level trees. I guess now the trees
are going to have root of root of n leaves. This is completely
analogous to the decomposition
that I built before, but it's maybe giving you a different
picture of it, a little bit more of
a tree like picture. And now, again, we can imagine this
decomposition, we decompose our tree
this way and then we keep subdividing each of those trees heightwise, into a high level tree
and low level trees, and then we subdivide
those and so on. We can stop that decomposition at
least mentally. Once the size of those trees fits
into a single block, just like before,
the decomposition is actually continuing
beyond that point. But once the
size of one of the little trees fits
into a single block, Everything is free
from that point on. There’s some elaborate process
where you're searching within the hierarchical
decomposition inside the block. But everything that
happens inside a block is
completely free. For all intents
and purposes, we can pretend like
our decomposition stops when we reach a tree size that fits
into a single block. The tree size
that fits into a single block is going to be on the order of B, either in terms of the
number of leaves of the tree or the number of elements in the tree, and the height
of such a tree is going to be the
logarithm of that. So you effectively
can think of this decomposition
happening down to the point where you have individual trees of height order Theta log B. Now, if you're searching
this structure, you're walking down
the overall tree on some path from the
root to the leaf, you're interested
in how many blocks you hit along that path. That's going to be the running time
of your search, how many blocks you hit. Basically, how many of these tiny little trees of size order B do we
hit along that path? Well, each of those trees has height on the order of log B. The entire height of
the overall tree is log n. And so on our
way down this path, the number of
blocks we hit is basically log of n
divided by log of B, and that is log base b of n. This is another way to see the same bound that on the way down the tree as
we're searching, we are going to only be hitting on the order
of log base b of n, blocks of memory during
the entire search. If we store the
elements we're searching according to this interestingly recursively
decomposed tree. This is sometimes
called a van Emde Boas tree layout, named after a famous
computer scientist who originally
came up with it. Some very
interesting ideas. This highlights,
I think that the cache oblivious model is a wonderful
model that's extremely practical because many
data structures and algorithms are
actually memory bound. This model might be much more descriptive
if used to develop algorithms
and data structures in memory intensive
situations. But as you can
see, that can sometimes require
a good bit of very careful
thought in terms of how to build something
that's cache oblivious, even for simple problems. I'll leave that with you and hope that
was enjoyable. Again, these
enrichment lectures are completely optional, but hopefully you'll find the content at least
somewhat interesting. [MUSIC]