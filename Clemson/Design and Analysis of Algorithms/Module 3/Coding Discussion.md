
![[Coding Discussion Slides 1.pdf]]



#include <iostream>
using namespace std;

struct Node {
  int key;
  Node *next;
};

Node *insert_front(Node *head, int x)
{
  Node *n = new Node;
  n->key = x;
  n->next = head;
  return n;
}

void print_list(Node *head)
{
  if (head == nullptr) return;
  cout << head->key << "\n";
  print_list(head->next);
}

Node *read_input(void)
{
  int x;
  if (cin >> x) return insert_front(read_input(), x);
  return nullptr;
}

Node *insert_keep_sorted(Node *head, int x)
{
  if (head == nullptr || x < head->key)
    return insert_front(head, x);
  head->next = insert_keep_sorted(head->next, x);
  return head;
}

Node *read_input_sorted(void)
{
  int x;
  if (cin >> x) return insert_keep_sorted(read_input_sorted(), x);
  return nullptr;
}

int sum(Node *head)
{
  if (head == nullptr) return 0;
  return head->key + sum(head->next);
}

Node *reverse(Node *head)
{
  if (head == nullptr || head->next == nullptr) return head;
  Node *s = head->next;
  Node *l = reverse(s);
  s->next = head;
  head->next = nullptr;
  return l;
} 

pair<Node *, Node *> split(Node *head)
{
  if (head == nullptr) return make_pair(nullptr, nullptr);
  if (head->next == nullptr) return make_pair(head, nullptr);
  pair<Node *, Node *> heads = make_pair(head, head->next);
  pair<Node *, Node *> rest = split(head->next->next);
  (heads.first)->next = rest.first;
  (heads.second)->next = rest.second;
  return heads;
}

Node *merge(Node *a, Node *b)
{
  if (a==nullptr) return b;
  if (b==nullptr) return a;
  if (a->key > b->key) swap (a,b);
  // a starts with smallest element
  a->next = merge(a->next, b);
  return a;
}

Node *merge_sort(Node *head)
{
  // split list into 2 lists of size n/2
  // sort them
  // merge them
  if (head == nullptr || head->next == nullptr) return head;
  pair<Node *, Node *> heads = split(head);
  return merge(merge_sort(heads.first), merge_sort(heads.second));
}

int main(void)
{
  print_list(merge_sort(read_input()));
}




