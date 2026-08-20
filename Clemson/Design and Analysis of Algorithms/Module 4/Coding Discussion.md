
![[Coding Discussion Slides .pdf]]



#include <iostream>
#include <tuple>
using namespace std;

struct Node {
  int key;
  int val = 0;
  int size = 1;
  Node *left = nullptr;
  Node *right = nullptr;
};

void update_size(Node *root)
{
  // update root size since left or right size might have gone up
  root->size = 1;
  if (root->left != nullptr) root->size += root->left->size;
  if (root->right != nullptr) root->size += root->right->size;
}

Node *insert(Node *root, int k)
{
  if (root == nullptr) {
    Node *n = new Node;
    n->key = k;
    return n;
  }
  if (k == root->key) return root;
  if (k < root->key) root->left = insert(root->left, k);
  else root->right = insert(root->right, k);
  update_size(root);
  return root;
}

pair<Node *, Node *> split(Node *root, int k)
{
  if (root == nullptr) return make_pair(nullptr, nullptr);
  if (k < root->key) {
    // recursively split left subtree
    pair<Node *, Node *> result = split(root->left, k);
    root->left = result.second;
    update_size(root);
    return make_pair(result.first, root);
  }
  pair<Node *, Node *> result = split(root->right, k);
  root->right = result.first;
  update_size(root);
  return make_pair(root, result.second);
}

Node *insert_balanced(Node *root, int k)
{
  if (root == nullptr) {
    Node *n = new Node;
    n->key = k;
    return n;
  }
  if (k == root->key) return root;
  int n = 1 + root->size;
  if (rand() % n == 0) { // insert at root with prob 1/n
    Node *L, *R;
    tie(L, R) = split(root, k);
    Node *n = new Node;
    n->key = k;
    n->left = L;
    n->right = R;
    update_size(n);
    return n;
  }
  if (k < root->key) root->left = insert_balanced(root->left, k);
  else root->right = insert_balanced(root->right, k);
  update_size(root);
  return root;
}

void print_inorder(Node *root)
{
  if (root == nullptr) return;
  print_inorder(root->left);
  cout << root->key << "\n";
  print_inorder(root->right);
}

Node *join(Node *L, Node *R)
{
  if (L == nullptr) return R;
  if (R == nullptr) return L;
  int T = L->size + R->size;
  if (rand()%T < L->size) { // with prob proportional to L->size
    L->right = join(L->right, R);
    update_size(L);
    return L;
  }
  R->left = join(L, R->left);
  update_size(R);
  return R;
}

Node *remove(Node *root, int k)
{
  if (root == nullptr) return nullptr;
  if (k == root->key) {
    // remove root
    Node *to_return = join(root->left, root->right);
    delete root;
    return to_return;
  }
  if (k < root->key) root->left = remove(root->left, k);
  else root->right = remove(root->right, k);
  update_size(root);
  return root;
}

Node *find(Node *root, int k)
{
  if (root == nullptr) return nullptr;
  if (k == root->key) return root;
  if (k < root->key) return find(root->left, k);
  return find(root->right, k);
}

class VirtualArray {
private:
  Node *root = nullptr;
public:
  int &operator[] (int key) {
    Node *n = find(root, key);
    if (n == nullptr) root = insert(root, key);
    return find(root, key)->val;
  }
};

int main(void)
{
  Node *root = nullptr;
  int x;
  /*
  while (cin >> x) root = insert_balanced(root, x);
  root = remove(root, 7);
  print_inorder(root);
  */
  VirtualArray A;
  A[999999999] = 17;
  cout << A[7] << " " << A[999999999] << "\n";
}

[Music] Dean: Binary search trees are definitely the star of this module, and so I thought it would definitely make sense for them to also be the focus of our coding discussion. Let's see if we can actually code up a balanced binary search tree, maybe using the randomized balancing mechanism that we've talked about in lecture that hopefully will be one of the simpler ways to keep the tree balanced. There are almost a limitless number of things you can do with binary search trees. I guess we need to figure out what are our goals for how to use the binary search trees that we're actually coding up. Maybe we can go back to the standard use cases of a binary search tree as either a set or a map. Maybe in each of those two cases, we can try and accomplish a simple goal. Maybe our first goal is just to implement a balanced binary search tree that represents a set of integers. 

It'll support insert, remove, and find, the major operations on a set, maybe the ability to print out an in order traversal. But basically just building a binary search tree that holds a bunch of integers. That'll be our first goal. Then we'll try and build on top of that, extend that to represent a map that gives us the functionality of a virtual array. Remember that maps often are accessed in many programming languages using this associative array notation. What I'd like to do is build a map that behaves like an array so that I can say something in my code like A[999999999] = 17. What that will actually do behind the scenes is look up the element in my binary search tree with a key of 999999999 and assign it a corresponding value of 17 because remember that maps are just a bunch of key value pairs that you're storing in the binary search tree. 

The benefit of doing this is that I'm actually emulating a large, sparsely filled array with substantially less memory than an actual array would take. A normal array would actually take one billion units of memory in order to be able to say something like this. But if we're emulating the array with a map, then it only uses an amount of memory proportional to the number of elements that are actually being stored in the array. All the other ones are treated like defaults, essentially. This can be a really beneficial thing to remember when you're writing code. Sometimes you don't need an actual array, but you can make a fake array that underneath the hood is actually just a map and that uses a lot less memory, and it's still just about as efficient. Every access to the array is going to take log n time if we use a binary search tree to represent the map. 

If we use later on a hash table, it would even be constant time for each access. Let's go ahead and start writing some code to build our binary search tree. Our first goal is just a set of integers using a binary search tree. I'll switch gears and go to my coding set up here. Let's start maybe emacs bst.cpp. A clean slate. I'll start the way I usually start with including iostream and maybe using namespace std. 

I guess if we're writing a binary search tree, we probably need a node structure for the binary search tree, so struct node. Every node is going to have an integer key since we're storing a set of integers, and it'll have a pointer to its left and right children. Maybe I'll default those to a null pointer so that it makes it easy to initialize new nodes, if I have to. I think I may also need to store in each node the size of its subtree because our balancing mechanism is going to require that when we do things like splits and joins and whatnot. I'll make that maybe default to one because if I create a new node, its size should just be one because it's just one single node by itself. If I want to create a binary search tree, this is my starting point. I just make a pointer to the root of the tree and that starts out as null, and then I'm just going to insert new elements into the tree. 

I guess maybe the first function I should write is an insert function. The way I typically would write that is insert, I'm passing in, I guess, the root of the tree and the key that I'm trying to insert. This function is going to return a pointer to the resulting root of the tree post insert because the root of the tree might change as a result of inserting k into it. The way I would call this function would be something like root = insert(root, 17), if I want to insert the value 17 into my tree. That says, hey, root, insert the value 17, and then that hands back a pointer to the new root of the tree, which I then update. How do I make this work? I guess insert is going to be a recursive function. 

Appropriate base cases are probably good to have a look at here. If the tree is empty that I'm insert into, if root is = to a null pointer, then I guess I probably just need to allocate a new node and hand back that one single new node. Maybe Node *n equals a new Node. Then I'm going to initialize that node. Everything else gets defaulted in that node structure, so I'm just going to initialize the key of the node to k and then return that node n. That's the easy case, that's the base case if I'm inserting into an empty tree. I guess there's also maybe an interesting case if the key that I'm asking to insert, what if that already exists in the tree? 

What if that is the same as the key stored at the root? I don't think I really probably want to store duplicates in the tree. Maybe in this case, I'll effectively just ignore the request to insert, I'll just return the root in that case. Now I can do the usual recursive delegation if the key that I'm trying to insert is less than the key of the root. By the binary search tree property, that key belongs in my left subtree. I will ask my left subtree to handle the insert. I'll call insert on roots left subtree and tell it to insert the value k. When I do that, that's going to hand me back a pointer to I guess what should now be my updated left subtree root. 

I'll set my left subtree to the result of what I get when I ask the left subtree to insert a new value. If that's not the case, I guess, then I just insert into the right subtree using the same approach. Ask the right subtree to insert the new key and then update its root accordingly. Now, at the very end here, I do need to return the root of the tree because that's what insert is supposed to return but I do think I need to pay attention to the subtree sizes because anytime you insert a new element into a tree, then certain subtree sizes are going to increase. This case where I create a brand new node, I don't think I need to do anything here because the default size of that new node was one so the subtree size is going to be set correctly. But I do worry that if I recursively ask my left or right subtree to do an insert, then the left or right subtree might update its size as a result of that insert, and so the root might then need to update its size in response to that. I might need to update the root size since left or right size might have gone up. 

How do I do that? I guess I could just recalculate the root size based on the root. Starts out with a size of one representing just itself, and then I would add into that the size of my left subtree and the size of my right subtree. Basically, just do a wholesale recalculation on the root size that takes the size of myself, one plus the left size plus the right size, that will recompute properly what the size of the subtree represented by root ought to be in response to possibly the left or the right sizes having changed during those recursive calls. I guess maybe I'm a little bit worried here that left and right might be null, so I probably want to do something like if the left subtree is not null, then I can add its size in. Let's see, if the roots right subtree is not null, then I can update the root size by adding in the size of the right subtree. Otherwise, I think I could have possibly crashed by trying to look at the left subtree size if the left subtree was actually null. 

I'm updating sizes as well as inserting the element in question. I think my insert function is actually done. Now I can actually call the insert function. I'm just going to read in a bunch of integers from standard input. As long as I can read in an integer, I'm going to just say root = insert(root, x). I'm just inserting a bunch of integers into the tree. Then what should I do? 

Let's maybe print out the contents of the tree. Do a print_inorder on my root. I guess I need to write an inorder traversal function here that prints out the contents of my tree inorder, print inorder and star root. That's a relatively simple function. If the root is null again, I'll do nothing. Otherwise, I'm going to recursively print the left subtree. I'm going to print out the key stored at the root. 

I can actually spell things properly, and then I'm going to recursively print out the right subtree. printf, root -> right. This should be a recursive in order traversal that will print out the contents of my tree. They should be printed out in sorted order. Actually this will be a good test maybe to compile and run. If I type in a bunch of arbitrary integers, I should get them back in sorted order from the binary search tree. There's a lot we still need to do. We haven't done anything regarding balance yet. 

This is a naive insert that just uses the binary search tree property to guide where it inserts new elements. If we insert elements like in increasing order, we're going to get a very unbalanced tree as a result. But let's compile and run just to make sure that things aren't going off the rails too badly yet at this stage. If I run my program and I type in 5, 4, 3, 2, 1, I get back 1, 2, 3, 4, 5. At least things aren't in a terrible state yet. It looks like we're actually building our binary search tree. However, I suspect it's going to be quite slow because of the fact that it's not balanced. 

In fact, we can probably highlight that. There's a Unix command called seq that just gives me a sequence of consecutive integers. That's probably about the worst case that I can feed to my program because that's going to generate a binary search tree in the shape of one very long right path, I guess. If I run this and I pipe it into my program, then my tree contains the numbers 1 through 10. That's good. If I'm really going to stress test this, maybe I need pipe to result into dev/null. Now I feed at 10 numbers, now I feed at 100 numbers, 1,000 numbers, so far so good. 

This should be a quadratic running time. I suspect maybe around 10,000, it's going to start slowing down and 100,000 should be pretty much out of reach. This is behaving as expected because our tree is maximally unbalanced. It is just one long path of length n where n is 100,000. Each of these inserts is taking on the order of n squared time towards the end of this process, which makes sense why it's running so slowly. We do need to address balance, I guess with our insert function. Should we do that now? Why not? 

Let's go ahead and do a balanced version of our insert function. I'll keep around the old insert function. Maybe I'll make a new version that tries to keep the tree balanced as it does inserts. Maybe we'll have a version of insert, we'll call it like insert balanced. We'll modify our code to do whatever we need to do to make things balanced. I guess if this is going to be recursive, I need to make sure it calls itself insert balanced instead of just regular insert. I'm also noticing that this update code is common to both. 

Let me factor that out and make it its own function just to clean things up a little bit. I'll make that updates the size of the root. Maybe I'll call it up date size to be a bit more descriptive. Update size on the root is going to just do this stuff here. Because I think I'm going to have to end up calling this in several different places at the end of the day. Here, I'm just going to call update size on the root. That's going to recompute the roots size and of taking into account changes that might have happened in the sizes of your left and right subtrees. 

I can do the same thing here in my insert balanced code, just to make that look a little bit simpler, I'm going to just call update size here at the end. How did we insert so as to keep the tree balanced? Remember, now, we want to keep the tree in a state that is as if we had just built it from scratch by inserting its elements in random order, and we have gone through in lecture kind of what it entails to keep the tree in that state probabilistically. I've actually included my cheat sheet on how to do that here. If you're inserting an element into an n-1 element tree, so you're inserting the nth element into the tree, then there's only one special case. There's the case where you might possibly insert the new element at the root of the tree. With probability 1 out of n, we should do an insert at the root using split, so we'll probably have to implement split, which I also have here on my cheat sheet, how that looks in terms of its recursive structure. 

Otherwise, we just insert recursively to the left or to the right, and I think that we already have that part because our function already recurses to the left and recurses to the right. All we really need is this extra bit where there's a slight chance that we insert at the root instead of delegating the insert to recursion. Let's see how to do that. With a one and n chance where n is going to be the new size of our tree, we should insert at the root. I look at my insert balance function. Then maybe if I am here before I delegate recursively, I'm going to flip a coin, say like, with probability 1/n, I would like to, I'll have to figure out how to flip that coin, insert at the root. How do you insert at the root? 

I guess we would call split to split the tree apart into two pieces. We'd have a left and a right piece, and they're going to be the result of calling split on the tree, so I'd split the tree apart on the key that I'm trying to insert into the root. Then that's going to give me back the result of those two pieces. How is the split function going to be written just so I can get the syntax right? The split function is going to take a node, which is the root of the tree that I'm splitting, and it's going to take a key, and it will split the tree on that key and return back, I guess, two roots of the two resulting pieces of the split. I actually have to return probably a pair of two things as the result of the split. If that's the way the split function is written, then I guess what I get back is a pair of two node stars. 

I'd like to be able to assign those simultaneously. I think there's a function in C++ called i, then let me tie those two things together in a pair and make them assigned in one fell swoop. If I do that, I think I need to include tuple as a header file, so I'm going to do that. I basically split the tree apart into a left and a right piece, and now I'm just going to install the new node at the root. I'm going to create a new node and initialize it. I guess I'm just copying the code from above that creates a new node, initializes it, and I'm installing it at the root, so my left and right pointers are going to be the two pieces of the split because I've split my existing tree apart, put the new node in at the root, and then its left and right subtrees are going to be the two sides of my split, basically. Then I'm going to return n. Probably before I return n, it looks like I've attached these two subtrees to n, so n's size isn't going to be correct. 

N's size is going to be one from just creating a new node, so I probably need to call update_size(n) to make its size appropriate. I can assume that the results I get back from the split have their sizes set correctly, so L and R have their sizes set correctly. I just need to set n's size, the new root's size properly. With probability 1/n, how do I flip a biased coin like that? What is n actually? N is going to be one plus the root's size because the root size is the current size of the tree. One plus that is the new size of the tree. 

I need to flip a coin with probability 1/n and do this. I'll take a random number mod n, that'll give me a random integer in the range zero through n-1, maybe if that just comes out as zero, then I will insert at the root because zero is only one of the n choices or how this number could come out as. It could come out as any number between zero, and n-1. This does indeed happen with probability 1/n. Though that should be my insert function in my balanced insert function. I need to, I guess still write the split function, that's going to be interesting because we have to return a pair of nodes as a result of splitting. Well, let's try and write it. 

I guess we have to tear off the band-aid at some point here. If I'm going to split a tree, we're going to have to do it recursively, so maybe there are some base cases involved. Maybe if I'm asking myself to split an empty tree, I'm going to return two empty trees. What I get when I make a pair of two null pointers. That's the base case. If I make it past this, then I'm actually splitting an actual tree now. Let's go back and look at the picture for how split is supposed to work. 

If I'm splitting a tree on a value k, then that should break the tree apart into two pieces, one piece having all the keys less than or equal to k, and one piece having all the keys greater than k, and I need to return the roots of those two pieces. I'm going to implement this recursively. I start at the root of my tree, and I'm going to ask basically either the left or the right subtree to recursively split itself. If k is less than the root's key, then I'm going to ask the left subtree to split itself. Otherwise, I'll ask the right subtree to split itself. If I look at what happens in this picture, the left subtree has dutifully split itself apart into two pieces, one of them is the piece here with the root node indicated, the other piece stays behind and becomes your new left subtree of the original root. When I hand back the results, I guess I hand back, one of them is the left side of the recursive split, and the other side is my original root. 

That's the pair of roots that I'm going to have to hand back, and something that's a mirror image of that if I split the right subtree instead. This is the case if k is less than the root's key. Let's look at doing that case perhaps. If the key that I'm trying to split on is less than the root's key, then I need to recursively split left subtree. I'm going to call split on the root's left subtree, and I'm going to tell it to split on the value k, and that's going to give me back a pair of two node stars. Let's just say that's the result of the split, and I need to figure out what to do with the result of that split. I'm going to have two answers. 

I'm going to have result.first, is the first root node that I get back from the split, and I get result.second back, that's the second result I get back from the split. If I go back and look at the picture here, I've split my left subtree, I get back two root nodes, result.first and result.second. I guess result.second stays behind and becomes my new left subtree of the original root, and result.first is one of the two answers that I need to return as a result of the overall call to split along with the original root. That doesn't look too bad. If we go back, we now know what to do with these things. Result.second that stays behind, the root's new left subtree is going to become result.second, and then I'm going to return the results of what I get when I make a pair out of result.first. That was the left side of the split, and then the original root is the right side of the split. 

That's the overall structure. I do worry that I need to update a size somewhere because I've changed the root's left subtree. The left subtree itself is the result.second, so I can count on split to update all the sizes that were part of the split. But I have made changes to the root's left subtree and that may change the root's size, and no one else is looking out for the root here, so I might need to do an update_size call on the root after I've modified its left subtree. A lot of mass has left the left subtree as a result of splitting the left subtree. I definitely, yes, need to update the size of the root. That's what happens if I recursively split the left subtree. 

Otherwise, I'm going to have to basically do the mirror image of this to split the right subtree instead. I will copy and paste, always a recipe for disaster. I'll split the right subtree and get back two pieces. Now I guess I'm going to set the root's right subtree to be the first of those two results because that's the piece that gets left behind and becomes my new right subtree. Then the results that I return, I guess the left side of the overall split is the original root. Then I guess probably result.second is the other piece, so that I think is the split function. A little bit on the technical side for this one, I'm not going to lie that was interesting to think through. 

Actually before we jump to claiming victory, let's compile this and actually run it and see what happens. If I compile update_size, too few arguments. Did I not even pass something to update _size? Let's see, update_size. I called it on root, I called it on root, I called it on root, I called it on n, I called it on nothing. That's not good. Let's call it on root. 

Compile, so we've compiled successfully. If I run like seq 10 and pipe that into a.out, then I get back. This is good. I get back, at least what I expect, 10 elements in sorted order when I print out the tree, it didn't crash on me or anything like that. There's a good reason it didn't crash on me, I think in my main function, I'm still calling the old insert, so I'm not even exercising the new code. Let's actually call the code that we just wrote, I called it what? insert_balanced or insert_balance? 

insert_balanced, okay. Let's actually call the code that I wrote. We still seem to be running properly, even if we run it on a bigger input, that's good to see. Let's maybe stress-test this. If I pipe the result into dev null and I run it on bigger and bigger inputs, then now that we're actually keeping the tree balanced presumably, it should run much faster. Remember that 100,000 was where the n^2 to the original unbalanced tree had trouble, so this is 100,000 right here. If I run it, excellent, it runs in the split second, and here's a million. 

Much faster, this is n log n versus n^2 again, so a pretty dramatic difference. We're almost, I think almost out of the woods, we've actually written maybe the hardest part. I think the split function is quite a doozy because of the pairs of things that are involved. The only remaining function that I think we promised to implement was the remove function. Let's go ahead and implement that and see how that works because that involves, I guess a call to join that has to have a random coin flip in it. If I have a node *remove, node *root, int k, so I want to ask the root to remove a particular key, and I'm going to pass back as a return value the new root of the resulting tree host removed because the root can change as a result. This should end up having a very similar structure to the insert function, I think. 

As a base case, root equals null pointer, return. I guess if I'm asking myself to remove from an empty tree, I should probably just return a null pointer because the key that I asked to remove clearly isn't there. There's probably an interesting case for if k is equal to the root's key. In this case, I'm asking you to actually remove the root. Then if you get past that case, then you're saying if k is less than the root's key, now we're going to be delegating things to recursion. Probably like my left subtree is going to be what I get when I ask it to do a recursive removal, remove(root->left, k); else equals remove(root->right, k). Since I've probably decreased the sizes of my left and right subtrees, I probably need to call update_size to update the root size and then return the root. 

This is almost the same code that I wrote for insert. It's just calling remove instead of calling insert. Then I guess I have to do something special if I'm removing the root. How did we remove the root node? How do you delete a node from a binary search tree? You replace it with what you get when you join its two subtrees together. All I'm going to do is call join on the left and the right subtrees of the root, I guess I need to write join, and that's going to give me back the new root. 

I'm going to basically want to return that. Although I need to, somewhere along the lines, delete the existing root. I need to delete root to release the memory that was allocated for the root node. Although now, this is probably not proper because I've released that memory, but then I've accessed the memory here with the call to join. I probably need to do things in a slightly different order to make sure I don't do that. Maybe I'll say something like node *to_return is equal to. I'm going to do the join first. 

Save the root of the joined tree. That's what I have to return at the end. Then after I've computed that, it's safe to delete the root, and then I can return the resulting tree that was the join of my left and right subtrees. Do I need to be careful with subtree sizes? I think I'll just let the join operation make sure that it updates subtree sizes appropriately. I think the remove function is actually correct now, and all I need to do is implement the join function. I need to basically write a join function that takes two trees, let's call them like the left tree and the right tree, and joins them into one tree. 

I'll write some base cases and then we'll work through exactly what has to happen with the join operation here. If L is empty, then I'm just going to return R, because I'm joining R with nothing in that case. If R is empty, I'm going to return L, because I'm basically joining L with nothing. If I make it past those two base cases, now we get to the interesting case where both L and R have contents in their respective trees. How do I actually do the join in this case? Maybe let's go to the whiteboard and remind ourselves of how the join actually works. I have an element, say, e. That's the one that I'm actually deleting, so e is getting deleted from the tree. 

E has a left and a right subtree, and those are the two things that I'm going to be joining together to get the new subtree, basically, that gets plugged in where e was. How do I join those two trees, L and R? If I zoom in on L and R, so here's L is going to have a root node, and it's going to have its own left and right subtrees, and R is going to have a root node and its own left and right subtrees. There were, remember, two cases with the join operation? I could either consider taking the entire right subtree and recursively joining it with the right subtree of L. I call join on those two things, and that's what becomes L's new right subtree. That's one possibility. 

The other possibility is the mirror image of that, I guess. If I want to draw a picture of that, I guess, it would be something similar. Again, you have L and you have R. Now the mirror image picture here would be I take all of L, and I'm going to join that with the right tree's left subtree. I take the join of those two things, and that becomes R's new left subtree. In the first case, the root of L is the final root of the joined tree. In the second case, the root of R is the final root of the joined tree. 

I have to actually make a biased coin flip decision between those two cases, because remember at the end of the day you want to make sure that a totally random element ends up as the overall root of the joined tree. So I need to choose between these two cases with probabilities proportional to the sizes of L and R. The first case, I choose with probability proportional to the size of L, and the second case, I choose with probability proportional to the size of R. The way I'm going to do that is I'm going to choose maybe an integer. If I have the L's size and R's size, I'm going to let maybe T be the total of L's size plus R's size. Imagine that I'm sampling a random point from an interval of size T. If that random point that I sample is less than L size, then I'm going to pick the left case, and that'll happen with probability proportional to the size of the left subtree. 

Let's see if we can actually implement these things in code, and we'll be close to being finished in that case. I have to make my biased coin flip. T was going to be the combination of L's size and R's size. I was going to say something like if a random number mod T, so there's T possible choices there, if that's less than, say, L's size, this happens with probability proportional to L's size. Then in this case, I'm going to be making L the root of the joined together tree and then joining R into it. I'm going to say that L's new right subtree is the result of recursively joining it with R. Then I'm basically going to return, I guess, L is the root of the joined tree, and I've changed its right subtree size, so I probably need to update the size of L before I return it. 

That's the left case, and then the right case is going to be pretty much the mirror image of that, I guess. In that case, R's left subtree is going to be the result of recursively joining L into it. Joining L into R's left subtree, I update the size of R and I return R, because now R is going to be the root of the joined tree. That's the join function that gets called by remove, and so now we actually should hopefully have working code that actually does the remove. I need to maybe test that out. Let's just make sure that it compiles, first of all. It does compile. 

That's good. Let's see if we can test that out. Maybe after I read in all my numbers, I'm just going to say root = remove(root, 7). I'll just remove seven from the tree, and then print it out inorder. If I compile, and let's maybe run seq 10 and feed that into a.out. What we get back is everything but seven. So far it looks like our implementation is doing what it's supposed to be doing. 

We have a fully balanced binary search tree that handles inserts, removes. Did we actually code the find operation? I've been writing so much code that I can't even remember. Do we need to write a find operation? We might need to write the find operation. Let's do that really quickly. That should be super easy. 

Node *find. Let's just return a pointer to the node in the tree that matches a particular key that we're looking for. If root = nullptr, return nullptr. I guess, if the key we're looking for is the root, then return the root. That's the answer. Otherwise, we can just delegate to recursion. If the key we're looking for is less than the root, then I'm going to return the result of calling find on root->left, k. Otherwise, I return find on root->right, k. We've written insert, remove, and find in our balanced binary search tree. 

Our first goal has been accomplished. Remember what our second goal was for this coding exercise. We wanted to emulate a large, sparsely filled integer array without using much memory. We'd like to be able to use this array notation to actually access a map of keys to integer values. If we're going to extend our data structure now to be a map, what all are we going to need to do? Hopefully, that actually won't be too difficult, because now a map is a bunch of key value pairs. We actually have a key and a value, and maybe the default value is going to be just zero. 

Now, everything should still just work. Every node in the binary search tree is just going to have a value of zero attached to it, and all of the other code that we wrote is still going to work just fine, because nothing interacts with values yet. All I need to do now is maybe write a little class that represents my VirtualArray. Maybe I'll have a class that's a VirtualArray class. What I want to have at the end of the day, maybe I'll comment out the code that I had written initially, because I don't want to have too much going on in main. I'm going to make a VirtualArray, or A, and I would like to be able to say something like A(999999999) = 17. That's my goal. I would like to be able to access A as if it were a regular array. 

This particular class is going to have to override the bracket operator, I guess, to return a reference to the value that you get when you look up an element in one of these binary search trees. I guess, inside of this class, it is going to have to have a node *root, which probably by default is a nullptr. But then in terms of the public methods in the class, I'm probably just going to have to override the operator brackets, where you pass in, I guess, the index. The operator brackets takes a value, which is the index that's within those brackets, and it's going to return, I guess, a reference to the value field of the corresponding node in my tree. I'm going to return an integer reference in this case. What's this operator going to do, I guess, I've asked it to look up a particular index. Let me call this key, because that really is the key that I'm looking up in my binary search tree. 

What if that key isn't present actually in the binary search tree? I could actually call find. N is going to be the result of calling find on that key. I guess I'll have to pass in the root and that key. What if that's null? What if n = nullptr? What if I didn't find the key that I'm looking for? 

In this example, that would actually happen. If I called A(999999999), that would invoke the operator brackets with key equal to 99999, which isn't in the structure yet. If it's not in the structure, I probably have to go ahead and add it to the structure. I'm going to just say that root = insert(root, key). At this point, the element has now been added to the structure with its default value of zero. Now I know it exists in the structure, so I can actually just return what I get when I call find on the root and that key, and that'll give me back a pointer to the node in the structure that represents that key, which I know exists because I just inserted it if it didn't exist, and I just want to return a reference to the value field. Did I call it value or val? 

I think I called it val. That's basically what I want to do. Just overload the array access operator here, and hopefully, that will let me treat this as if it was an array, so I can like print out A(7), and after that, I'll print out A(999999999). Let's see what that actually prints out. I compile and run. I get back zero and 17. That actually makes sense, because A(7) I haven't initialized yet. 

When I actually call A(7), that actually invokes this operator bracket with seven as the key, which causes seven to be inserted into the structure with its default value of zero, and that's what gets returned. A(99999) actually is set to the value 17 by that earlier statement. This does indeed seem to be emulating an array in the proper way, and using only an amount of memory that's proportional to the values that I've actually accessed from that array. I think we have now succeeded in both of the goals that we set out to achieve. We've built a balanced binary search tree with randomized balancing. We've used it to create a set of integers, and we've also used it to create a VirtualArray that is using map functionality, basically, to store key value pairs, but it operates like an array of integers. Hopefully, this has been informative, and hopefully, it also indicates that binary search trees are actually relatively easy things to code up. 

Maybe if you have a chance try coding them up yourself, they're really good for practice. But hopefully, this has been interesting, and I'll leave the rest of this with you. [Music]