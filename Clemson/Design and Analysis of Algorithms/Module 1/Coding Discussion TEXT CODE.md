#include <vector>
#include <iostream>
#include <stack>
using namespace std;

vector<int> H;

int get_height(int L, int R)
{
  int min_height = H[L];
  for (int i=L+1; i<=R; i++)
    min_height = min(min_height, H[i]);
  return min_height;
}

int solve1(void)
{
  int N = H.size();
  int best = 0;
  for (int L=0; L<N; L++)
    for (int R=L; R<N; R++) {
      int height = get_height(L,R);
      int width = R-L+1;
      int area = height * width;
      best = max(best, area);
    }
  return best;
}

int solve2(void)
{
  int N = H.size();
  int best = 0;
  for (int L=0; L<N; L++) {
    int height = H[L];
    for (int R=L; R<N; R++) {
      height = min(height, H[R]); 
      int width = R-L+1;
      int area = height * width;
      best = max(best, area);
    }
  }
  return best;
}

int solve3(void)
{
  int N = H.size();
  int best = 0;
  vector<int> L(N), R(N);

  // Compute L(i)'s
  stack<int> S;
  S.push(0);
  for (int i=1; i<N-1; i++) {   // O(N)?
    while (H[S.top()] >= H[i]) S.pop();   // O(N)
    L[i] = S.top();
    S.push(i);
  }

  // Compute R(i)'s
  while (!S.empty()) S.pop();
  S.push(N-1);
  for (int i=N-2; i>=1; i--) {
    while (H[S.top()] >= H[i]) S.pop();
    R[i] = S.top();
    S.push(i);
  }

  // O(N)
  for (int i=1; i<N-1; i++) {
    int height = H[i];
    int width = R[i] - L[i] - 1;
    int area = height * width;
    best = max(best, area);
  }
  return best;
}

int main(void)
{
  int x;
  H.push_back(0);
  while (cin >> x) H.push_back(x);  // O(1) amortized time
  H.push_back(0);

  cout << solve3() << "\n";    // O(N)
  cout << solve2() << "\n";    // O(N^2) !?!?!?!?!?
  cout << solve1() << "\n";    // O(N^3) !?!?!?!?!?!!?!?
}
