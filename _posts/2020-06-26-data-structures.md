---
title: Data Structures
author: Teo
layout: post
---
<header> <h2> What are data structures? </h2> </header>
<p> Data structure are specialized formats for organizing, processing, retrieving and storing data. While there are several basic and advanced structure types,
any data structure is efficient in some operations and inefficient in others. Therefore, the goal is to understand them in order to pick the most optimal data structure
for the problem at hand.</p>
<p> Commonly used Data Structures are the following (listed from the easiest to wrap your head around to the hardest in my opinion): 

<div class="6u$ 12u$(small)">
			<ol>
				<li>Arrays</li>
				<li>Linked Lists</li>
				<li>Stacks</li>
				<li>Queues</li>
				<li>Trees</li>
        <li>Graphs</li>
        <li>Hash Tables</li>
			</ol>
		</div>

<hr/>

<br>
<h2> Arrays </h2>
<p> An array is the simplest and most widely used data structure. Other data structures like stacks and queues are derived from arrays. Here’s an image of a simple array of size 10, containing elements [10, 20, 30, 40, 50, 60, 70, 80, 90 and 100].

<p><span class="image left"><img src="{{ 'assets/images/arr.png' | relative_url }}" alt="" /></span> Each data element is assigned a positive numerical value called the Index, which corresponds to the position of that item in the array. The majority of languages define the starting index of the array as 0. </p>
<p><span class="image right"><img src="{{ 'assets/images/rsz_dimensionalarr.png' | relative_url }}" alt="" /></span>  

<div class="6u$ 12u$(small)">
		<h3> Types of Arrays </h3>
			<ul>
				<li> One-dimensional arrays (as shown above)</li>
				<li>  Multi-dimensional arrays (arrays within arrays)</li>
			</ul>
		</div>
  </p>

<div class="6u$ 12u$(small)">
	<h3> Basic Operations on Arrays </h3>
			<ul>
				<li> <b>Insert</b> — Inserts an element at a given index</li>
				<li> <b> Get </b>— Returns the element at a given index </li>
				 <li> <b>Delete</b> — Deletes an element at a given index </li>
				  <li><b> Size </b>— Gets the total number of elements in an array </li>
			</ul>
		</div>

<h3> Array Processing Examples in Java </h3>
{% highlight java linenos %}String[] dogs = {"terries", "pugs", "bulldogs", "samoyeds"};
int[] = {1, 2, 3, 4};
// Accesing an element of the array
System.out.println(dogs[1]); // Outputs pugs
// Change an element of the array
dogs[1] = "beagles";
System.out.println(dogs[1]); // Now outputs beagles
// Size of array
System.out.println(dogs.length); // Outputs 4
}{% endhighlight %}

{% highlight java linenos %}
// Function to insert an element in arr at given index 
public static int[] insertElement(int[] arr, int index, int element) {
    int[] result = new int[arr.length];
    for(int i = 0; i < index; i++)
        result[i] = a[i];
    newarr[index] = element;
    for(int i = index + 1; i < arr.length; i++)
        result[i] = a[i - 1];
    return newarr;
}{% endhighlight %}
<hr/>

<br>
<h2> Linked Lists</h2>
<p> A linked list is another important linear data structure which might look similar to arrays at first but differs in memory allocation, internal structure and how basic operations of insertion and deletion are carried out. </p>


<p><span class="image right"><img src="{{ 'assets/images/linkedlist.png' | relative_url }}" alt="" /></span> A linked list is like a chain of nodes, where each node contains information like data and a pointer to the succeeding node in the chain. There’s a head pointer, which points to the first element of the linked list, and if the list is empty then it simply points to null or nothing.

Linked lists are used to implement file systems, hash tables, and adjacency lists. 

Here’s a visual representation of the internal structure of a linked list: </p>


<div class="6u$ 12u$(small)">
		<h3> Types of Linked Lists </h3>
			<ul>
				<li> Singly Linked List (Unidirectional)</li>
				<li>  Doubly Linked List (Bi-directional)</li>
			</ul>
		</div>
		
<div class="6u$ 12u$(small)">
	<h3> Basic Operations on Linked Lists </h3>
			<ul>
				<li> <b> InsertAtEnd </b> — Inserts a given element at the end of the linked list </li>
				<li> <b> InsertAtHead </b> — Inserts a given element at the start/head of the linked list </li>
				<li> <b> Delete </b> — Deletes a given element from the linked list </li>
				<li> <b> DeleteAtHead </b> — Deletes the first element of the linked list </li>
				<li> <b> Search </b> — Returns the given element from a linked list </li>
				<li> <b> isEmpty </b> — Returns true if the linked list is empty</li>
			</ul>
		</div>		    

<h3> Linkled List implementation in Java </h3>
{% highlight java linenos %}
import java.io.*; 
public class LinkedList { 
    Node head; // head of list 
    // Linked list Node. This inner class is made static so that main() can access it 
    static class Node { 
        int data; 
        Node next; 
        Node(int d) // Constructor 
        { 
            data = d; 
            next = null; 
        } 
    } 
    // **************INSERTION************** 
    // Method to insert a new node at end
    public static LinkedList insertAtEnd(LinkedList list, int data) 
    { 
        // Create a new node with given data 
        Node new_node = new Node(data); 
        new_node.next = null; 
        // If the Linked List is empty, then make the new node as head 
        if (list.head == null) { 
            list.head = new_node; 
        } 
        else {// Else traverse till the last node and insert the new_node there 
            Node last = list.head; 
            while (last.next != null) { 
                last = last.next; 
            } 
            last.next = new_node; // Insert the new_node at last node 
        } 
        return list; 
    } 
    // **************TRAVERSAL************** 
    // Method to print the LinkedList. 
    public static void printList(LinkedList list) { 
        Node currNode = list.head; 
        System.out.print("\nLinkedList: "); 
        // Traverse through the LinkedList 
        while (currNode != null) { 
            // Print the data at current node 
            System.out.print(currNode.data + " "); 
            // Go to next node 
            currNode = currNode.next; 
        } 
        System.out.println("\n"); 
    } 
    // **************DELETION BY KEY************** 
    // Method to delete a node in the LinkedList by KEY 
    public static LinkedList deleteByKey(LinkedList list, int key) { 
        // Store head node 
        Node currNode = list.head, prev = null; 
        // CASE 1: If head node itself holds the key to be deleted 
        if (currNode != null && currNode.data == key) { 
            list.head = currNode.next; // Changed head 
            System.out.println(key + " found and deleted"); 
            // Return the updated List 
            return list; 
        } 
        // CASE 2: If the key is somewhere other than at head   
        // Search for the key to be deleted,  keep track of the previous node as it is needed to change currNode.next 
        while (currNode != null && currNode.data != key) { 
            // If currNode does not hold key continue to next node 
            prev = currNode; 
            currNode = currNode.next; 
        } 
        // If the key was present, it should be at currNode 
        // Therefore the currNode shall not be null 
        if (currNode != null) { 
            // Since the key is at currNode 
            // Unlink currNode from linked list 
            prev.next = currNode.next; 
            // Display the message 
            System.out.println(key + " found and deleted"); 
        } 
        // CASE 3: The key is not present 
        // If key was not present in linked list currNode should be null 
        if (currNode == null) { 
            System.out.println(key + " not found"); 
        } 
        return list; 
    } 
    // **************DELETION AT A POSITION************** 
    // Method to delete a node in the LinkedList by POSITION 
    public static LinkedList deleteAtPosition(LinkedList list, int index) { 
        Node currNode = list.head, prev = null; // Store head node 
        // CASE 1: If index is 0, then head node itself is to be deleted 
        if (index == 0 && currNode != null) { 
            list.head = currNode.next; // Changed head 
            System.out.println(index + " position element deleted"); 
            return list; 
        } 
        // CASE 2: If the index is greater than 0 but less than the size of LinkedList 
        int counter = 0; 
        // Count for the index to be deleted, keep track of the previous node as it is needed to change currNode.next 
        while (currNode != null) { 
            if (counter == index) { 
                // Since the currNode is the required position. Unlink currNode from linked list 
                prev.next = currNode.next; 
                System.out.println(index + " position element deleted"); 
                break; 
            } 
            else { 
                // If current position is not the index, continue to next node 
                prev = currNode; 
                currNode = currNode.next; 
                counter++; 
            } 
        }    
        // CASE 3: The index is greater than the size of the LinkedList 
        // If the position element was found, it should be at currNode, Therefore the currNode shall not be null 
        if (currNode == null) { 
            System.out.println(index + " position element not found"); 
        } 
        return list; 
    }{% endhighlight %}

<h3> Bonus: Arrays vs Linked Lists </h3>
<p> 🧠 In the <b> array </b> the elements belong to indexes, i.e., if you want to get into the fourth element you have to write the variable name with its index or location within the square bracket. In a <b> linked list </b> though, you have to start from the head and work your way through until you get to the fourth element. As a result, accessing an element in an array is fast, while linked list takes linear time, so it is quite a bit slower. 
	<br>
🧠 Operations like insertion and deletion in  <b> array </b> consume a lot of time. On the other hand, the performance of these operations in <b> linked lists </b> is fast.
<br>
🧠<b> Arrays </b> are of fixed size. In contrast,<b> linked lists </b> are dynamic and flexible and can expand and contract its size.
<br>	
🧠 In an  <b> array </b>, memory is assigned during compile time while in a <b> linked list </b>it is allocated during execution or runtime. 
<br>	
🧠 Elements are stored consecutively in  <b> arrays </b> whereas they are stored randomly in <b> linked lists </b>.</p>
<hr/>
<br>



<h2>Stacks </h2>
<p><span class="image right"><img src="{{ 'assets/images/stack.png' | relative_url }}" alt="" /></span> We are all familiar with the Undo option, present in almost every application. Ever wondered how it works? The idea: you store the previous states of your work (which are limited to a specific number) in the memory in such an order that the last one appears first. This can’t be done just by using arrays. That is where Stacks come in. Here’s a visual representation of a stack and it's operations: <div class="6u$ 12u$(small)">
	<h3> Basic Operations of Stacks </h3>
			<ul>
				<li> <b> Push </b> — Inserts an element at the top </li>
				<li> <b> Pop </b> — Returns the top element after removing from the stack </li>
				<li> <b> isEmpty </b> — Returns true if the stack is emptyt </li>
				<li> <b> Top </b> — Returns the top element without removing from the stack </li>
			</ul>
		</div>	 </p>

      
<p><span class="image left"><img src="{{ 'assets/images/pancake.png' | relative_url }}" alt="" /></span> A real-life example of Stack could be a number of pancakes stacked on top of each other. In order to get the extra syrupy pancake that’s somewhere in the middle, you will need to remove (or alternatively, eat) all the pancakes placed on top of it. This is how the LIFO (Last In First Out) method works. </p>
<br>
<br>
		
<h3> Stack implementation in Java </h3>	
{% highlight java linenos %}
public class Stack<Item> implements Iterable<Item> {
    private Node<Item> first;     // top of stack
    private int n;                // size of the stack
    // helper linked list class
    private static class Node<Item> {
        private Item item;
        private Node<Item> next;
    }
    // Initializes an empty stack.
    public Stack() {
        first = null;
        n = 0;
    }
    public boolean isEmpty() {
        return first == null;
    }
    // Returns the number of items in this stack.
    public int size() {
        return n;
    }
    // Adds the item to this stack.
    public void push(Item item) {
        Node<Item> oldfirst = first;
        first = new Node<Item>();
        first.item = item;
        first.next = oldfirst;
        n++;
    }
    // Removes and returns the item most recently added to this stack.
    public Item pop() {
        if (isEmpty()) throw new NoSuchElementException("Stack underflow");
        Item item = first.item;        // save item to return
        first = first.next;            // delete first node
        n--;
        return item;                   // return the saved item
    }
    // Returns (but does not remove) the item most recently added to this stack.
    public Item top() {
        if (isEmpty()) throw new NoSuchElementException("Stack underflow");
        return first.item;
    }
     // Returns a string representation of this stack.
    public String toString() {
        StringBuilder s = new StringBuilder();
        for (Item item : this) {
            s.append(item);
            s.append(' ');
        }
        return s.toString();
    }
    // Returns an iterator to this stack that iterates through the items in LIFO order.
    public Iterator<Item> iterator() {
        return new LinkedIterator(first);
    }
    // an iterator, doesn't implement remove() since it's optional
    private class LinkedIterator implements Iterator<Item> {
        private Node<Item> current;
        public LinkedIterator(Node<Item> first) {
            current = first;
        }
        public boolean hasNext() {
            return current != null;
        }
        public void remove() {
            throw new UnsupportedOperationException();
        }
        public Item next() {
            if (!hasNext()) throw new NoSuchElementException();
            Item item = current.item;
            current = current.next; 
            return item;
        }
    }
}
{% endhighlight %}
<hr/>
<br>


<h2>Queues </h2>
<p><span class="image right"><img src="{{ 'assets/images/q.png' | relative_url }}" alt="" /></span> Similar to Stack, Queue is another linear data structure that stores elementa in a sequential manner. The only significant difference between Stack and Queue is that instead of using the LIFO method, Queue implements the FIFO method, which is short for First in First Out.  </p>
<p> A perfect real-life example of Queue: a line of people waiting at a ticket booth. If a new person comes, they will join the line from the end, not from the start — and the person standing at the front will be the first to get the ticket and hence leave the line. </p>
<p> </p>

<div class="6u$ 12u$(small)">
	<h3> Basic Operations of Queues </h3>
			<ul>
				<li> <b> Enqueue </b> — Inserts an element at the end of the queue </li>
				<li> <b> Dequeue </b> — Removes an element from the start of the queue </li>
				<li> <b> isEmpty </b> — Returns true if the queue is empty </li>
				<li> <b> Top </b> — Returns the first element of the queue </li>
			</ul>
		</div>	

<h3> Queue implementation in Java </h3>	
{% highlight java linenos %}
public class Queue<Item> implements Iterable<Item> {
    private Node<Item> first;    // beginning of queue
    private Node<Item> last;     // end of queue
    private int n;               // number of elements on queue
    // helper linked list class
    private static class Node<Item> {
        private Item item;
        private Node<Item> next;
    }
    // Initializes an empty queue.
    public Queue() {
        first = null;
        last  = null;
        n = 0;
    }
    // Returns true if this queue is empty.
    public boolean isEmpty() {
        return first == null;
    }
    // Returns the number of items in this queue.
    public int size() {
        return n;
    }
    // Returns the item least recently added to this queue.
    public Item peek() {
        if (isEmpty()) throw new NoSuchElementException("Queue underflow");
        return first.item;
    }
    // Adds the item to this queue.
    public void enqueue(Item item) {
        Node<Item> oldlast = last;
        last = new Node<Item>();
        last.item = item;
        last.next = null;
        if (isEmpty()) first = last;
        else           oldlast.next = last;
        n++;
    }
    // Removes and returns the item on this queue that was least recently added.
    public Item dequeue() {
        if (isEmpty()) throw new NoSuchElementException("Queue underflow");
        Item item = first.item;
        first = first.next;
        n--;
        if (isEmpty()) last = null;   // to avoid loitering
        return item;
    }
    // Returns a string representation of this queue.
    public String toString() {
        StringBuilder s = new StringBuilder();
        for (Item item : this) {
            s.append(item);
            s.append(' ');
        }
        return s.toString();
    } 
    // Returns an iterator that iterates over the items in this queue in FIFO order.
    public Iterator<Item> iterator()  {
        return new LinkedIterator(first);  
    }
    // an iterator, doesn't implement remove() 
    private class LinkedIterator implements Iterator<Item> {
        private Node<Item> current;
        public LinkedIterator(Node<Item> first) {
            current = first;
        }
        public boolean hasNext() { 
		return current != null;                     
	}
        public void remove() { 
		throw new UnsupportedOperationException();  
	}
        public Item next() {
            if (!hasNext()) throw new NoSuchElementException();
            Item item = current.item;
            current = current.next; 
            return item;
        }
    }
}
{% endhighlight %}
<hr/>
<br>

<h2> Binary Search Trees</h2>
<h3> Tree walks in Java </h3>	
{% highlight java linenos %}

// java program for different tree traversals
class Node {
    int key;
    Node left, right;

    public Node(int item)    {
        key = item;
        left = right = null;
    }
}

class BinaryTreeWalk {
    // root of Binary Tree
    Node root;

    BinaryTreeWalk() {
        root = null;
    }

    // given a binary tree, print its nodes according to the "bottom-up" postorder traversal. */
    void printPostorder(Node node) {
        if (node == null)
            return;

        // first recur on left subtree
        printPostorder(node.left);

        // then recur on right subtree
        printPostorder(node.right);

        // now deal with the node
        System.out.print(node.key + " ");
    }

    // given a binary tree, print its nodes in inorder
    void printInorder(Node node) {
        if (node == null)
            return;

        // first recur on left child
        printInorder(node.left);

        // then print the data of node
        System.out.print(node.key + " ");

        // now recur on right child
        printInorder(node.right);
    }

    // given a binary tree, print its nodes in preorder
    void printPreorder(Node node) {
        if (node == null)
            return;

        // first print data of node
        System.out.print(node.key + " ");

        // then recur on left sutree
        printPreorder(node.left);

        // now recur on right subtree
        printPreorder(node.right);
    }

    // Wrappers over above recursive functions
    void printPostorder() {
        printPostorder(root);
    }

    void printInorder() {
        printInorder(root);
    }

    void printPreorder() {
        printPreorder(root);
    }

    public static void main(String[] args) {
        BinaryTreeWalk tree = new BinaryTreeWalk();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);

        System.out.println("Preorder traversal of binary tree is ");
        tree.printPreorder();

        System.out.println("\nInorder traversal of binary tree is ");
        tree.printInorder();

        System.out.println("\nPostorder traversal of binary tree is ");
        tree.printPostorder();
    }
}
{% endhighlight %}
<hr/>
<br>


<h2> Hash Tables</h2>
<h3> Collisions resolved by chaining in Java </h3>	
{% highlight java linenos %}
// Java program to demonstrate implementation of our own hash table with chaining for collision detection
import java.util.ArrayList;

// A node of chains
class HashNode<K, V> {
    K key;
    V value;

    // Reference to next node
    HashNode<K, V> next;

    // Constructor
    public HashNode(K key, V value) {
        this.key = key;
        this.value = value;
    }
}

// Class to represent entire hash table
class ChainingHash<K, V> {
    // bucketArray is used to store array of chains
    private ArrayList<HashNode<K, V>> bucketArray;

    // Current capacity of array list
    private int numBuckets;

    // Current size of array list
    private int size;

    // Constructor (Initializes capacity, size and empty chains.
    public ChainingHash() {
        bucketArray = new ArrayList<>();
        numBuckets = 10;
        size = 0;

        // Create empty chains
        for (int i = 0; i < numBuckets; i++)
            bucketArray.add(null);
    }

    public int size() {
        return size;
    }

    public boolean isEmpty() {
        return size() == 0;
    }

    // This implements hash function to find index for a key
    private int getBucketIndex(K key) {
        int hashCode = key.hashCode();
        int index = hashCode % numBuckets;
        return index;
    }

    // Method to remove a given key
    public V remove(K key) {
        // Apply hash function to find index for given key
        int bucketIndex = getBucketIndex(key);

        // Get head of chain
        HashNode<K, V> head = bucketArray.get(bucketIndex);

        // Search for key in its chain
        HashNode<K, V> prev = null;
        while (head != null) {
            // If Key found
            if (head.key.equals(key))
                break;

            // Else keep moving in chain
            prev = head;
            head = head.next;
        }

        // If key was not there
        if (head == null)
            return null;

        // Reduce size
        size--;

        // Remove key
        if (prev != null)
            prev.next = head.next;
        else
            bucketArray.set(bucketIndex, head.next);

        return head.value;
    }

    // Returns value for a key
    public V get(K key) {
        // Find head of chain for given key
        int bucketIndex = getBucketIndex(key);
        HashNode<K, V> head = bucketArray.get(bucketIndex);

        // Search key in chain
        while (head != null) {
            if (head.key.equals(key))
                return head.value;
            head = head.next;
        }

        // If key not found
        return null;
    }

    // Adds a key value pair to hash
    public void add(K key, V value) {
        // Find head of chain for given key
        int bucketIndex = getBucketIndex(key);
        HashNode<K, V> head = bucketArray.get(bucketIndex);

        // Check if key is already present
        while (head != null) {
            if (head.key.equals(key))
            {
                head.value = value;
                return;
            }
            head = head.next;
        }

        // Insert key in chain
        size++;
        head = bucketArray.get(bucketIndex);
        HashNode<K, V> newNode = new HashNode<K, V>(key, value);
        newNode.next = head;
        bucketArray.set(bucketIndex, newNode);

        // If load factor goes beyond threshold, then double hash table size
        if ((1.0*size)/numBuckets >= 0.7) {
            ArrayList<HashNode<K, V>> temp = bucketArray;
            bucketArray = new ArrayList<>();
            numBuckets = 2 * numBuckets;
            size = 0;
            for (int i = 0; i < numBuckets; i++)
                bucketArray.add(null);

            for (HashNode<K, V> headNode : temp) {
                while (headNode != null) {
                    add(headNode.key, headNode.value);
                    headNode = headNode.next;
                }
            }
        }
    }

    // Driver method to test Map class
    public static void main(String[] args) {
        ChainingHash<String, Integer>map = new ChainingHash<>();
        map.add("this",1 );
        map.add("coder",2 );
        map.add("this",4 );
        map.add("hi",5 );
        System.out.println(map.size());
        System.out.println(map.remove("this"));
        System.out.println(map.remove("this"));
        System.out.println(map.size());
        System.out.println(map.isEmpty());
    }
}
{% endhighlight %}
<hr/>
<br>

<h3> Open-addressing implementation in Java </h3>	
{% highlight java linenos %} public class OpenAddressingHash {
    // properties of hash table
    private int max = 20;
    private HashTableNode[] vector = new HashTableNode[max];

    // element of hash table.
    class HashTableNode {
        public int key;

        HashTableNode(int key) {
            this.key = key;
        }
    }

    // constructor
    OpenAddressingHash() {
        for (int i = 0; i < max; i++) {
            this.vector[i] = null;
        }
    }

    // add element to hash table
    public void insert(int key, int i) {
        int hashcode = this.hashFunction(key, i);

        if ((i > 0) && (hashcode == this.hashFunction(key, 0))) {
            System.out.println("It's not possible to add the key " + key + " in hash table.");
            return;
        }

        if (this.vector[hashcode] != null) {
            this.insert(key, i + 1);
        }

        else {
            this.vector[hashcode] = new HashTableNode(key);
        }
    }

    // overloading of add() method. Simplifies the call of method.
    public void insert(int key) {
        this.insert(key, 0);
    }

    // search an element in hash table.
    public int search(int key, int i) {
        int hashcode = this.hashFunction(key, i);

        if ((i > 0) && (hashcode == this.hashFunction(key, 0))) {
            System.out.println("Key " + key + " not found in hash table. It was made " + i + " stepsizes.");
            return -99;
        }

        if ((this.vector[hashcode] != null) && (this.vector[hashcode].key == key)) {
            System.out.println("Key " + key + " found in hash table in " + (i + 1) + "-esim stepsize.");
            return hashcode;
        }

        return this.search(key, i + 1);
    }

    // overloading of search() method. Simplifies the call of method.
    public int search(int key) {
        return this.search(key, 0);
    }

    //Remove an element from the hash table.
    public void delete(int key) {

        int i = this.search(key);

        if (i != -99) {
            System.out.println("The key " + key + " was removed from hash table.");
            this.vector[i] = null;
        }
        else {
            System.out.println("The key " + key + " was not removed, because it does not exists in hash table.");
        }
    }

    // linear probing
    public int linearProbing(int key, int i) {
        return (key + i) % this.max;
    }

    // quadratic probing.
    public int quadraticProbing(int key, int i) {
        return (key + (i * i)) % this.max;
    }

    // double hashing.
    public int doubleHash(int key, int i) {
        return (this.doubleHash2(key) + i) % this.max;
    }

    // auxiliar hash function to Double hashing made by double() method.
    public int doubleHash2(int key) {
        return (1 + key) % (this.max - 1);
    }

    // hash function.
    public int hashFunction(int key, int i) {
        return this.linearProbing(key, i);
    }

    // toString method.
    public String toString() {
        String description = "Hash table: [ ";
        for (int i = 0; i < this.max; i++) {
            if (this.vector[i] == null) {
                description += "__  ";
            }
            else {
                description += String.format("%2d  ", this.vector[i].key);
            }
        }
        description += "]";
        return description;
    }
}
{% endhighlight %}
<hr/>
<br>


<h2> </h2>
<h3>  </h3>	
{% highlight java linenos %}
{% endhighlight %}
<hr/>
<br>


<p> </p>
<p> </p>
<p> </p>
<p> </p>

<h2> </h2>
<p> </p>

<h2> </h2>
<p> </p>

<h2> </h2>
<p> </p>

<h2> </h2>
<p> </p>

<h2> </h2>
<p> </p>

