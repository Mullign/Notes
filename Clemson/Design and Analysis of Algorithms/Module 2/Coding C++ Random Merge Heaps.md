#include <iostream>
using namespace std;

struct Node {
  int key;
  Node *left = NULL;
  Node *right = NULL;
};

Node *merge (Node *h1, Node *h2)
{
  if (h1==NULL) return h2;
  if (h2==NULL) return h1;
  // assume h1 has smaller root
  if (h1->key > h2->key) swap(h1, h2);
  bool heads = rand()%2;
  if (heads)
    h1->left = merge(h1->left, h2);
  else
    h1->right = merge(h1->right, h2);
  return h1;
}

Node *insert(Node *h, int x)
{
  Node *n = new Node;
  n->key = x;
  return merge(h, n);
}

Node *remove_min(Node *h)
{
  Node *result = merge(h->left, h->right);
  delete h;
  return result;
}

int main(void)
{
  int x;
  Node *h = NULL;
  while (cin >> x) h = insert(h, x);
  while (h != NULL) {
    cout << h->key << "\n";
    h = remove_min(h);
  }
}

