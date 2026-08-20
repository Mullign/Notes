Problem 1 
#include <iostream>

#include <vector>

#include <cmath>

#include <iomanip>

using namespace std;

  

// This function (which will be compiled with our code

// when it is submitted to the grading system) takes

// an integer index i and returns A[i].

// If you pass an invalid index or call this function

// more than 32 times, you'll get back -1

int call_grader(int i);

  

// For testing on your own system, you can call

// this function instead. It uses an array of length 10

// with values 1000, 2000, 3000, ..., 10,000.

// Don't forget to switch your code back to calling

// call_grader() above before submitting.

int call_grader_local(int i)

{

int A[10] = {1000, 2000, 3000, 4000, 5000,

6000, 7000, 8000, 9000, 10000};

return A[i];

}

  

int main(void)

{

// Values for N and T are set in the grading system

// through environment variables, if present.

// If these aren't present, the default values are N = 10

// and T = 8400.

int N = 10, T = 8400;

if (getenv("N") != NULL) N = atoi(getenv("N"));

if (getenv("T") != NULL) T = atoi(getenv("T"));

  

int my_answer = -1;

  

// ----------------------------------------

// This is the part of main() you should modify.

// (You are welcome to write other functions above

// and call them here, but all your code should be

// submitted in this one file).

int left = 0;

int right = N - 1;

int best_index = 0;

int closest_distance = 999999999;

  

// Binary search loop

while (left <= right) {

int i = left + (right - left) / 2;

int value = call_grader(i);// call_grader_local needs to be switched to call_grader when you submit!!

if (value == -1) break; // Invalid index

// Update best answer if this value is closer

int distance = abs(value - T);

if (distance < closest_distance) {

closest_distance = distance;

best_index = i;

}

// If the found is an exact match, it is done

if (value == T) {

best_index = i;

break;

}

// Binary search: go left or right

if (value < T) {

left = i + 1;

} else {

right = i - 1;

}

}

my_answer = best_index;

// ---------------------------------------

  

// Afterwards, you should print out the value of

// an index i for which A[i] is closest to T.

// You should only print this number on standard output,

// nothing else.

cout << my_answer << "\n";

}


Part 2

