# Ex6 Right Rotation LinkedList
## DATE: 21-08-2025
## AIM:
To write a Java  program to:
Create a singly linked list.
Rotate the linked list to the right by k positions.
Display the rotated linked list.
## Algorithm
1. Read n values to build the linked list and read k.
2. Find the length of the list and reach the last node.
3. Make the list circular by connecting last node to head.
4. Move length − (k % length) steps to find new tail.
5. Break the circle and print the list from the new head.
   

## Program:
```
/*
Program to  Right Rotation LinkedList
Developed by: SUBBIAH S 
RegisterNumber: 212223220111


import java.util.Scanner;

class Node {
    int data;
    Node next;
    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class prog {
    public static Node rotateRight(Node head, int k) {
        if (head == null || head.next == null || k == 0)
            return head;

        Node temp = head;
        int length = 1;
        while (temp.next != null) {
            temp = temp.next;
            length++;
        }

        temp.next = head;

        int stepsToNewHead = length - k % length;
        Node newTail = head;
        for (int i = 1; i < stepsToNewHead; i++) {
            newTail = newTail.next;
        }

        Node newHead = newTail.next;

        newTail.next = null;

        return newHead;
    }

    public static void printList(Node head) {
        Node temp = head;
        while (temp != null) {
            System.out.print(temp.data + " ");
            temp = temp.next;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        if (n <= 0) {
            sc.close();
            return;
        }

        Node head = new Node(sc.nextInt());
        Node tail = head;
        for (int i = 1; i < n; i++) {
            tail.next = new Node(sc.nextInt());
            tail = tail.next;
        }

        int k = sc.nextInt();

        head = rotateRight(head, k);

        System.out.print("LinkedList: ");
        printList(head);

        sc.close();
    }
}
 
*/
```

## Output:

<img width="882" height="256" alt="image" src="https://github.com/user-attachments/assets/6cc3aaf3-9af8-4331-a8fb-dc3d80997ee9" />


# Ex7 Removal of Nodes with a Specific Value from a Linked List
## DATE:26-08-2025
## AIM:
To write a java  program that removes all nodes from a linked list whose value matches a given integer (val) and returns the new head of the modified linked list.

## Algorithm

1.Move head forward until it reaches a node whose value is not equal to val. 

2.If the list becomes empty, return null. 

3.Start from the new head and traverse the list using a pointer (current).

4.If current.next contains val, skip that node 

5.Otherwise, move to the next node. Continue until the end, then return the modified head.


## Program:
```
/*
program that removes all nodes from a linked list whose value matches a given integer (val) and returns the new head of the modified linked list.
Developed by: SUBBIAH S
RegisterNumber: 212223220111


*/
class RemoveNodes {
    static class Node {
        int data;
        Node next;

        Node(int data) {
            this.data = data;
            this.next = null;
        }
    }

    static Node removeElements(Node head, int val) {
        
        while (head != null && head.data == val) {
            head = head.next;
        }

        if (head == null) return null;

        Node current = head;
        while (current.next != null) {
            if (current.next.data == val) {
                current.next = current.next.next; // Skip node
            } else {
                current = current.next; // Move ahead
            }
        }

        return head; // Return new head
    }

    static void display(Node head) {
        Node temp = head;
        while (temp != null) {
            System.out.print(temp.data + " ");
            temp = temp.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {

        Node head = new Node(1);
        head.next = new Node(2);
        head.next.next = new Node(6);
        head.next.next.next = new Node(3);
        head.next.next.next.next = new Node(6);
        head.next.next.next.next.next = new Node(4);

        System.out.println("Original Linked List:");
        display(head);

        int val = 6;

        head = removeElements(head, val);

        System.out.println("Linked List after removing value " + val + ":");
        display(head);
    }
}
 
*/
```

## Output:

<img width="577" height="178" alt="514427177-3fc5c634-4b7f-4c1f-a939-42d281793676" src="https://github.com/user-attachments/assets/8b491571-ae80-4bdb-9d3d-3aa8c413a212" />



## Result:
The java program successfully removes all nodes with the specified value (val) from the linked list and returns the new head.

# Ex8 Detection of Cycle and Finding the Starting Node in a Linked List
## DATE: 28/08/2025
## AIM:
To write a program that detects a cycle in a linked list and returns the node where the cycle begins.
If there is no cycle, the program should return null without modifying the linked list.
## Algorithm
1.Start slow = head and fast = head.

2.Move slow by 1 step and fast by 2 steps until they meet or fast becomes null.

3.If fast becomes null, return null (no cycle).

4.Move slow to head, keep fast at meeting point.

5.Move both one step at a time until they meet — this node is the cycle start.


## Program:
```
 /*
program that detects a cycle in a linked list and returns the node where the cycle begins.
If there is no cycle, the program should return null without modifying the linked list.
Developed by: SUBBIAH S
RegisterNumber: 212223220111

*/
class DetectCycle {

    static class Node {
        int data;
        Node next;

        Node(int data) {
            this.data = data;
            this.next = null;
        }
    }

    static Node detectCycle(Node head) {
        if (head == null || head.next == null) 
            return null;

        Node slow = head;
        Node fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;          
            fast = fast.next.next;     

            if (slow == fast) {        
                break;
            }
        }

        if (fast == null || fast.next == null)
            return null;

        slow = head;
        while (slow != fast) {
            slow = slow.next;
            fast = fast.next;
        }

        return slow;   
    }

    public static void main(String[] args) {

        Node head = new Node(1);
        head.next = new Node(2);
        head.next.next = new Node(3);
        head.next.next.next = new Node(4);
        head.next.next.next.next = new Node(5);

        head.next.next.next.next.next = head.next.next;

        Node cycleStart = detectCycle(head);

        if (cycleStart != null)
            System.out.println("Cycle starts at node: " + cycleStart.data);
        else
            System.out.println("No cycle detected.");
    }
}
  
*/
```

## Output:

<img width="798" height="175" alt="514427923-9d8d99fc-0ab8-4708-8517-3b5c6a2663a6" src="https://github.com/user-attachments/assets/9cf07013-1fb6-4b49-94e4-8696175c6272" />




## Result:
The program successfully detects whether a cycle exists in the linked list.
If a cycle is present, it correctly identifies and returns the node where the cycle begins.


# Ex9 Finding the Longest Length of Nested Set in a Permutation Array
## DATE: 02-09-2025
## AIM:
To write a program that finds the length of the longest set s[k] defined as s[k] = { nums[k], nums[nums[k]], nums[nums[nums[k]]], … },where the iteration stops before a duplicate element occurs.

The task is to return the maximum size among all such sets.
## Algorithm
1.Create a visited array to mark elements already used in any set.

2.For each index k, if it is not visited, start building the set S[k].

3.Keep moving to nums[current], marking each element as visited.

4.Count each step until you reach a visited element (duplicate).

5.Update the maximum count found so far and return it.  

## Program:
```
/*
program that removes all nodes from a linked list whose value matches a given integer (val) and returns the new head of the modified linked list.
Developed by: SUBBIAH S
RegisterNumber: 212223220111

*/
import java.util.Scanner;

class LongestSet {

    public static int longestSetLength(int[] nums) {
        boolean[] visited = new boolean[nums.length];
        int maxLength = 0;

        for (int i = 0; i < nums.length; i++) {
            if (!visited[i]) {
                int count = 0;
                int current = i;

                while (!visited[current]) {
                    visited[current] = true;
                    current = nums[current];
                    count++;
                }

                maxLength = Math.max(maxLength, count);
            }
        }

        return maxLength;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter the array size: ");
        int n = sc.nextInt();

        int[] nums = new int[n];

      
        System.out.println("Enter " + n + " elements:");
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }

        int result = longestSetLength(nums);
        System.out.println("Maximum size of S[k] = " + result);

        sc.close();
    }
}

   
*/

```

## Output:


<img width="435" height="89" alt="514428739-4eacad87-879a-439c-8de7-a72bb850f9c1" src="https://github.com/user-attachments/assets/37b9b1d0-0088-4984-a29c-6a4b13bee701" />


## Result:
The program successfully computes the longest length of the nested set s[k] for the given permutation array.


# Flattening a Nested List Using an Iterator
## DATE: 04-09-2025
## AIM:
To design and implement a class NestedIterator that flattens a nested list of integers such that all integers can be accessed sequentially using an iterator interface (next() and hasNext()).
## Algorithm
1.Start the program.

2.Define an interface-like class NestedInteger that can represent either a single integer or a nested list.

3.Use a stack or recursion to flatten all integers from the nested list into a single list.

4.Store the flattened list and maintain an index to track the current element.

5.Implement next() to return the next integer and hasNext() to check if more integers exist.

6.Test the iterator with a sample nested list.

7.Stop the program.
## Program:
```
/*
Program to find Flattening a Nested List Using an Iterator
Developed by: SUBBIAH S
RegisterNumber: 212223220111

import java.util.*;

interface NestedInteger {
    boolean isInteger();
    Integer getInteger();
    List<NestedInteger> getList();
}

class NI implements NestedInteger {
    private Integer value;
    private List<NestedInteger> list;

    NI(Integer value) {
        this.value = value;
        this.list = null;
    }

    NI(List<NestedInteger> list) {
        this.list = list;
        this.value = null;
    }

    public boolean isInteger() {
        return value != null;
    }

    public Integer getInteger() {
        return value;
    }

    public List<NestedInteger> getList() {
        return list;
    }
}

class NestedIterator implements Iterator<Integer> {
    private List<Integer> flattenedList = new ArrayList<>();
    private int index = 0;

    public NestedIterator(List<NestedInteger> nestedList) {
        flatten(nestedList);
    }

    private void flatten(List<NestedInteger> nestedList) {
        for (NestedInteger ni : nestedList) {
            if (ni.isInteger()) {
                flattenedList.add(ni.getInteger());
            } else {
                flatten(ni.getList());
            }
        }
    }

    public Integer next() {
        return flattenedList.get(index++);
    }

    public boolean hasNext() {
        return index < flattenedList.size();
    }
}

public class FlattenNestedList {
    public static void main(String[] args) {
        List<NestedInteger> nestedList = new ArrayList<>();
        nestedList.add(new NI(1));
        List<NestedInteger> innerList = new ArrayList<>();
        innerList.add(new NI(2));
        innerList.add(new NI(3));
        nestedList.add(new NI(innerList));
        nestedList.add(new NI(4));

        NestedIterator i = new NestedIterator(nestedList);
        System.out.print("Flattened list: ");
        while (i.hasNext()) {
            System.out.print(i.next() + " ");
        }
    }
} 
*/
```

## Output:

<img width="594" height="90" alt="514429842-2ed02c84-5ea3-4a30-bd22-198ca361f5b2" src="https://github.com/user-attachments/assets/d1664638-b3c3-4f2a-99dd-eef7663175c4" />



## Result:
The NestedIterator class successfully flattens a nested list of integers into a single list and provides sequential access using standard iterator methods.

## Result:
Thus, the C program to perfom right rotation on linked list is implemented successfully.
