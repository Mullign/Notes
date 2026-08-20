#include <iostream>

#include <vector>

#include <cmath>

#include <iomanip>

#include <algorithm>

using namespace std;

  

int N;

  

// This function (which will be compiled with our code

// when it is submitted to the grading system) takes

// a value v and compares the cutoff points c1 and c2

// for two players. These cutoff points are such that

// exactly v units of value are in [0,c1] and [0,c2]

// respectively for players 1 and 2. The return value

// is -1 if c1<=c2 and +1 otherwise.

  

// If your comparisons don't look like you are

// performing randomized quickselect, this function

// will notify the grader accordingly and your

// solution will receive a deduction of -25 points.

int compare(int player1, int player2, double v);

  

// For testing on your own system, you can call

// this function instead. Each participant has a

// triangular-shaped value function with uniformly

// spaced peaks, with player 0 having the _last_

// peak and player N-1 having the _first_. This

// makes the ideal ordering of players N-1...0.

//

// Don't forget to switch your code back to calling

// compare() above before submitting.

int compare_local(int player1, int player2, double v)

{

if (player1 < 0 || player1 >= N) { cout << "Invalid value of player1!\n"; exit(0); }

if (player2 < 0 || player2 >= N) { cout << "Invalid value of player2!\n"; exit(0); }

if (v < 0 || v > 1) { cout << "Invalid value of v!\n"; exit(0); }

  

double peak1 = 1-(1.0+player1)/(1+N), peak2 = 1-(1.0+player2)/(1+N);

double c1 = v<=peak1 ? sqrt(v*peak1) : 1 - sqrt((1-v)*(1-peak1));

double c2 = v<=peak2 ? sqrt(v*peak2) : 1 - sqrt((1-v)*(1-peak2));

return c1 <= c2 ? -1 : +1;

}

  

// Partition function

int partition(int *A, int left, int right){

int pivot = A[right], i = left, x;

  

for (x = left; x < right; x++){

if (A[x] < pivot){

swap(A[i], A[x]);

i++;

}

}

  

swap(A[i], A[right]);

return i;

}

  

// Quickselect function

int quickselect(int *A, int left, int right, int k){

  

//p is position of the pivot

int p = partition(A, left, right);

  

//k equals pivot

if (p == k-1){

return A[p];

}

//k is less than the pivot

else if (k - 1 < p){

return quickselect(A, left, p - 1, k);

}

//k greater than the pivot

else{

return quickselect(A, p + 1, right, k);

}

}

  

bool mycomp(int p1, int p2)

{

return compare_local(p1,p2,0.5) < 0; // Use compare_local for testing

}

  

int main(void)

{

// The value for N is set in the grading system

// through an environment variable, if present.

// If not present, feel welcome to set N to

// any value you want for local testing.

N = 30;

if (getenv("N") != NULL) N = atoi(getenv("N"));

  

// Below is the part of main() you should modify.

// (you are welcome to write other functions above

// and call them here, but all your code should be

// submitted in this one file).

  

// Temporarily, this just sorts all the players on

// their "1/2" cut points using the comparison

// function we are given above.

vector<int> P;

for (int i=0; i<N; i++) P.push_back(i);

sort(P.begin(), P.end(), mycomp);

  

// At the end, you should print out the order of

// the players for their allocations. Each player

// is an integer index in the range 0 .. N-1.

// You should just print these N numbers, separated

// by whitespace, and nothing else.

for (int i=0; i<N; i++)

cout << P[i] << "\n";

}