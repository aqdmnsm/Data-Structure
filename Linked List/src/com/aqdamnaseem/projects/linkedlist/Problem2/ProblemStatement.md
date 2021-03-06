## Check and Remove if a Linked List has a loop.

There are other parts to this problem like finding the loop and then finding the starting node of the loop.

We will solve this problem using Floyd's Cycle Detection Algorithm (https://en.wikipedia.org/wiki/Cycle_detection#Floyd's_Tortoise_and_Hare)


Let's try to understand Floyd's Algorithm with a simple example

Suppose there are 2 friends. Lets call them A and B

1. A and B daily goes for jogging at a Circular park<br />

2. A being lazy, jogs at speed "x". B is energetic and jogs at speed "2x". <br />

3. So if they both starts from a common point, A running at speed "x" and B running at speed "2x" then they will surely meet 
at the same location they started from.<br />
  
In fact if the starting point for A and B is different they will still meet, maybe not at same place but at some other point in track.

The other thing to notice is that even if A travels at "x" speed and B travels at "3x" speed, still they both will meet, 
but the numbers of cycles B to complete before meeting A will increase.

If there is no loop then B will reach the end of track and algorithm ends.

### Detecting Loop

Have two pointers, classically called hare and tortoise. Move hare by 2 steps and tortoise by 1. If they meet at some point,
then there is surely a cycle and the meeting point is inside the cycle.

Time Complexity  : O (N)<br />
Space Complexity : O (1)<br />

### Find the start of cycle

Take one pointer to starting position of the list and keep the other at the meeting point. Now increment both by one and the meeting point is the starting node of the loop.

Why this approach works? Let's see

Suppose 



				p_____________q_________________

				              |_________r_______|


Suppose p is the starting node of linked list,q is the firstnode of loop and r is the meeting point

 x - distance between first node of the linked list and starting node of loop (p to q)

 y - distance from the starting node of the loop to the meeting point node in the clockwise direction (q to r)

 z - distance from the meeting point to first node of the loop in the clockwise direction (r to q)

 now 

			distance travelled by slow pointer before meeting fast pointer = x + y
			distance travelled by fast pointer before meeting fast pointer = k* (y+z) +y

			where k is the number of rounds fast pointer go through before meeting

			also, distance travlled by fast = 2 * distance travelled by slow 
			
				       2* (x+y) = k* (y+z) +y
				       x = k* (y+z)-y
				       x = k * (loop length) - y 

Therefore if we keep one pointer(A) at start node of the linked list and other one(B) at the meeting point and keep moving them by same speed, they will meet at the starting node of loop

Time Complexity  : O (N)<br />
Space Complexity : O (1)<br />

### Finding the length of Loop

Keep one pointer fixed at the meeting point while increment the other until they are same again. Increment a counter as you go along and the counter value at meet will be the length of cycle.

Time Complexity  : O (N)<br />
Space Complexity : O (1)<br />

### Removing Loop

Keep one pointer fixed at the meeting point while increment the other until you reach a node whose next is the meeting point.

That node is last node of the loop. Set the next pointer of that node to null

Time Complexity  : O (N)<br />
Space Complexity : O (1)<br />

### Time Complexity Analysis

Note: The time complexity of the above algorithm is O(N) where N is no of nodes in Linked List. Lets try to prove this.

Suppose there are N nodes in Linked List, then in <=N steps either the fast pointer will reach the linked list end (if there is no loop) or slow pointer will be inside loop.

Let's say loop is of length M <= N, once slow pointer is inside loop, the distance between slow and fast pointer increases by one and when it becomes a multiple of M, they meet at a node and algorithm ends

Now distance will be a number divisible by M in <=M steps

So getting the slow pointer to the loop and meet fast pointer will take <= N + M  <= 2N  i.e. O (N)
