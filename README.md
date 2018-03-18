# StackSorter

I worked with another student, Ali Siddiqui, while attending the University of Victoria, and together we developed a new way of sorting integers using a linked list of stacks.

To test the following sorting algorithms, run:
`javac Sorting.java`

Followed by:
`java Sorting`

If you want to test the individual files using your own testing suite, below is example code to test each version of the file.  In this code, we pass in an array to be sorted called “forSorting”:

VERSION 1
StackSorterV1 L = new StackSorterV1();

VERSION 2
StackSorterV2 L = new StackSorterV2();

VERSION 3
StackSorterV3 L = new StackSorterV3();


# Implentation Details:
The pseudocode for the main function of the algorithm is as follows

`sort(A)  
 Create new linked list of stacks  
 for i in 0 —> length of A  
  insert(a[i])  
  
 i <— 0  
 for i in 0 —> length of A  
  a[i] = remove()  
  increment i  
`
  
The sort() method simply reads every value of the array, A, and calls the insert method to insert them into the list. It then calls the remove method to systematically insert the items back into the array in sorted order.  
  
  
  
### The pseudocode for the insert function is as follows:  
`insert(value)  
 newNode = new node() //make a new node  
  
 if head == null // if the list is empty  
  push value onto the stack of the new node  
  head = newNode  
 else  
  node curr  
  if top of head stack >= value  
   push value onto head stack  
   return  
  
  for every node in list  
  if value <= top of current node stack  
   push value onto node stack  
   return  
  
  push the value onto newNode  
  add newNode to end of the list  
`
  
The insert function creates a new node. If there are no nodes in the list, it inserts the value passed in on the new node. It then makes head node equal to the new node. If there is at least one element in the list, it checks to see if the value is smaller than the top of the first list. If it is, it pushes the node onto the top of the first stack and returns. If it is not, it continues through the list and checks the top of every stack until it finds a stack such that the top element is larger than the value. If it finds a stack, it adds the value to the top of the stack. If it gets to the end of the list, without finding a stack, it creates a new node at the end of the list, and puts the value on the stack of the newly created node.  
  
  
  
The pseudocode for the remove function is as follows:  
  
`remove()  
 create new node min  
  
 keep track of previous node, initialize to null.  
  
 for every node in list  
  if top of min > top of next node  
   min = next node  
   previous = current node  
  
 a <— pop min  
  
 if stack on min is empty  
  if head = min  
   head = head.next // remove first node  
  if min is the end of the list  
   prev.next = null //remove last node  
  else  
   prev.next = min.next //remove node from middle of the list  
  
 return a  
`  
The remove function goes through the list every time, and pops the stack with the smallest element. It then checks to see if that stack is now empty, if it is, it removes that node from the list.  
  
Here is a diagram of what the stack might look like after the insertion step:  
  
Sample Input: [5 3 8 4 6 10 7 8 5 5]  

![alt text](https://github.com/mattpaletta/StackSorter/raw/master/images/sorting_diagram.png "StackSorter Algorithm Diagram")
  
So how does this algorithm do in terms of performance? Below is a graph comparing our algorithm to a number of other popular algorithms. You can download all of the code to test it yourself. In the testing functions, we created an array of varying size, and generated random numbers, and ran tests where each algorithm would sort the same array. We do this multiple times, and take the average between tests. When running the algorithm, you can specify the maximum size of the array you want to test, as well as the number of times you want to run each test. The code provided is written in Java.
  
![alt text](https://github.com/mattpaletta/StackSorter/raw/master/images/sorting_comparison.png "Sorting Algorithm Comparison")
  
From Top to Bottom (lower is better):  
- Selection Sort
- Stack Sorter V1
- Insertion Sort
- Stack Sort V2
- Stack Sort V3
- Merge Sort
- Heap Sort
- Quick Sort
  
  
You may have noticed that there are 3 versions of the algorithm in the graph above. The first version of the stack sorter algorithm used the pseudocode described above and used the built-in Java stack library. The second version was exactly the same as the first version, except we implemented stacks ourselves using linked lists. Going from the first to second version made a huge difference in performance, meaning out algorithm was now faster than Insertion sort. It turns out the built-in stacks library was written with Java 1.0 and never updated. So it isn't very well optimized for performance. The third version we introduced a hash table. The hash table makes an array based on powers of 10. We did this so that each list would be smaller, meaning it should theoretically take less time to sort. I thought I would explain version 2 in pseudocode for simplicity.  
  
Although we didn't implement them, we also came up with some theoretical ways of making our algorithm faster. If there was a way to further hash the values, such as by multiples of 10 or 100, each linked list would be shorter, meaning when inserting and removing, performance would be improved. Another possible way would be to store the minimum and second minimum from the stacks. And as long as the minimum stack is less than the top of the second minumum, remove from that stack, then return an array. This means that it cuts down on the number of times we go through the entire linked list. Also, if there was a way for a node to point to the next one during the insert process, then the remove function would be linear.  
  
  
  
Our system specs and Java version are as follows:  
  
Macbook Pro 13-inch, Mid 2012  
Core i5 @ 2.50Ghz  
8GB Ram at 1333 Mhz DDR3  
java version "1.8.0_60"  
Java(TM) SE Runtime Environment (build 1.8.0_60-b27)  
Java HotSpot(TM) 64-Bit Server VM (build 25.60-b23, mixed mode)  
No other programs were open on the machine at the time.  
