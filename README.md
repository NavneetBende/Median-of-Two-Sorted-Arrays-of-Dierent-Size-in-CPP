Median of Two Sorted Arrays of Different Size in C++
 

Here, in this page we will discuss the program to find the Median of two sorted arrays of different size i n C++ programming language. We are given with two sorted arrays say a[] and b[] of size n and m respectively. We need to find the median of these two sorted arrays.

Case 1 : If (n +m) is odd then the median will be (n+m)/2-th element .
Case 2 : If (n+m) is even, then median will be the average of the ((n+m/2)-1)-th and (n+m)/2-th element.

Sort First half in Ascending and Second half in descending order in C
Method 1 :
Take the size of first array and store it in a variable say n.
Now, declare an array of size n and then take n elements from the user.
Similarly, take another variable say m and take the size of another variable from the user.
Declare an array of size m and then take m elements from the user.
Now, create another array say arr3[] of size n+m.
Now, store the elements of arr1[] and arr2[] in arr3[].
Sort the arr3[], using sort function
Now, print the median : if (n+m) is odd then median is arr3[(n+m)/2]
Otherwise, median is ((arr3[(n+m)/2])+(arr3[(n+m)/2-1]))/2.
Time and Space Complexities :
Time-Complexity : O((n+m)log(n+m))
Space-Complexity : O(n+m)
Median of two sorted arrays of different sizes
Code for Median of Two Sorted Arrays of Different Size in C++
Run
#include
using namespace std;

int main(){

  int n;
  cin>>n;

  int arr1[n];
  for(int i=0; i<n; i++)
  cin>>arr1[i];
  
  int m;
  cin>>m;

  int arr2[m];
  for(int i=0; i<m; i++)
  cin>>arr2[i];

  int arr3[n+m];

  for(int i=0; i<n; i++)
  arr3[i]=arr1[i];

  int j=n;
  for(int i=0; i<m; i++)
  arr3[j++]=arr2[i];

  sort(arr3, arr3+(n+m));

  int median;

  if((n+m)%2==0)
  median = (arr3[(n+m)/2] + arr3[(n+m)/2-1])/2;

  else 
  median = arr3[(n+m)/2];

  cout<<median;
}
Input :
4
2 6 7 8


6
10 12 17 18 90 91

Output:
11
Related Pages
Given an array which consists of only 0, 1 and 2

Move all the negative elements to one side of the array

Minimum no. of Jumps to reach the end of an array 

Find Largest sum contiguous Subarray

Minimize the maximum difference between heights 

Method 2 :
Take the size of first array and store it in a variable say n.
Now, declare an array of size n and then take n elements from the user.
Similarly, take another variable say m and take the size of another variable from the user.
Declare an array of size m and then take m elements from the user.
Now, Create a variable count to have a count of elements in the output array.
Now, to merge both arrays, declare two indices i and j initially assigned to 0. Compare the ith index of 1st array and jth index of second, increase the index of the smallest element and increase the count.
Now, take two variables say m1 and m2 and store (n+m)/2 and (n+m)/2-1 in these two variables respectively.
Check if the count = (m+n) / 2.
And if (m+n) is odd return m1,
Otherwise, return (m1+m2)/2.
Time and Space Complexities :
Time-Complexity : O((n+m))
Space-Complexity : O(1)
Code for Median of Two Sorted Arrays of Different Size in C++
Run
#include<bits/stdc++.h>
using namespace std;

int main(){

  int n;
  cin>>n;

  int arr1[n];
  for(int i=0; i<n; i++) cin>>arr1[i];

  int m;
  cin>>m;

  int arr2[m];
  for(int i=0; i<m; i++) cin>>arr2[i];

  int i = 0, j=0, count =0, m1=-1, m2=-1; 

  for (; count <= (n + m)/2; count++) { m2=m1; if(i != n && j != m) { m1 = (arr1[i] > arr2[j]) ? arr2[j++] : arr1[i++];
    }
    else if(i < n)
    {
       m1 = arr1[i++];
    }
    else
    {
       m1 = arr2[j++];
    }
  }

  if((n + m) % 2 == 1)
    cout<< m1;

  else
    cout<< (m1+m2)/2;
}
Input :
4
2 6 7 8


6
10 12 17 18 90 91

Output:
11
Method 3 :
Take the size of first array and store it in a variable say n.
Now, declare an array of size n and then take n elements from the user.
Similarly, take another variable say m and take the size of another variable from the user.
Declare an array of size m and then take m elements from the user.
Now, Create a recursive function that takes both arrays along with their sizes.
Find the middle elements of both the arrays. i.e element at (n – 1)/2 and (m – 1)/2 of first and second array respectively. Compare both the elements.
If the middle element of the smaller array is less than the middle element of the larger array then the first half of the smaller array is bound to lie strictly in the first half of the merged array. It can also be stated that there is an element in the first half of the larger array and the second half of the smaller array which is the median. So, reduce the search space to the first half of the larger array and the second half of the smaller array.
Similarly, If the middle element of the smaller array is greater than the middle element of the larger array then reduce the search space to the first half of the smaller array and second half of the larger array.
Time and Space Complexities :
Time-Complexity : O(min(log(n), log(m)))
Space-Complexity : O(1)
Code for Median of Two Sorted Arrays of Different Size in C++
Run
#include<bits/stdc++.h>
using namespace std;

int MO2(int a, int b)
  return (a + b)/2; 

int MO3(int a, int b, int c)
  return a + b + c - max(a, max(b, c)) - min(a, min(b, c));

int MO4(int a, int b, int c, int d)
{
  int Max = max( a, max( b, max( c, d ) ) );
  int Min = min( a, min( b, min( c, d ) ) );
  return ( a + b + c + d - Max - Min ) / 2;
}

int medianSingle(int arr[], int n)
{
   if (n == 0)
     return -1;
   if (n%2 == 0)
     return (arr[n/2] + arr[n/2-1])/2;
   return arr[n/2];
}

int findMedianUtil(int arr1[], int n, int arr2[], int m)
{
   if (n == 0)
    return medianSingle(arr2, m);

   if (n == 1)
   {
      if (m == 1)
        return MO2(arr1[0], arr2[0]);

      if (m & 1)
        return MO2( arr2[m/2], MO3(arr1[0], arr2[m/2 - 1], arr2[m/2 + 1]) );

      return MO3( arr2[m/2], arr2[m/2 - 1], arr2[0] );
   }

   else if (n == 2)
   {
      if (m == 2)
       return MO4(arr1[0], arr1[1], arr2[0], arr2[1]);

      if (m & 1)
       return MO3(arr2[m/2], max(arr1[0], arr2[m/2 - 1]),min(arr1[1], arr2[m/2 + 1]));

      return MO4 ( arr1[m/2],arr2[m/2 - 1],max( arr1[0], arr2[m/2 - 2] ), min( arr1[1], arr2[m/2 + 1] ));
   }

   int idxA = ( n - 1 ) / 2;
   int idxB = ( m - 1 ) / 2;

   if (arr1[idxA] <= arr2[idxB] )
     return findMedianUtil(arr1 + idxA, n/2 + 1, arr2, m - idxA );

   return findMedianUtil(arr1, n/2 + 1, arr2 + idxA, m - idxA );
}

int findMedian( int A[], int N, int B[], int M )
{
   if (N > M)
     return findMedianUtil( B, M, A, N );

   return findMedianUtil( A, N, B, M );
}

int main(){

  int n;
  cin>>n;

  int arr1[n];
  for(int i=0; i<n; i++)
  cin>>arr1[i];

  int m;
  cin>>m;

  int arr2[m];
  for(int i=0; i<m; i++)
  cin>>arr2[i];

  int i = 0, j=0, count =0, m1=-1, m2=-1; 

  for (; count <= (n + m)/2; count++)
  {
    m2=m1;
    if(i != n && j != m)
    {
       m1 = (arr1[i] > arr2[j]) ? arr2[j++] : arr1[i++];
    }
    else if(i < n)
    {
       m1 = arr1[i++];
    }
    else
    {
       m1 = arr2[j++];
    }
  }

  if((n + m) % 2 == 1)
    cout<< m1;

  else
    cout<< (m1+m2)/2;
}
Input :
4
2 6 7 8


6
10 12 17 18 90 91

Output:
11
