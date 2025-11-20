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
Developed by: Vamsi Krishna G
RegisterNumber: 212223220120


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
