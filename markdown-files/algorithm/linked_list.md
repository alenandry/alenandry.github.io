# Linked List

## Implement with Javascript (ES6)

```js
class Node {
	// constructor
	constructor(element) {
		this.element = element;
		this.next = null
	}
}
// linkedlist class
class LinkedList {
	constructor() {
		this.head = null;
		this.size = 0;
	}

	// adds an element at the end
	// of list
	add(element) {
		// creates a new node
		var node = new Node(element);

		// to store current node
		var current;

		// if list is Empty add the
		// element and make it head
		if (this.head == null)
			this.head = node;
		else {
			current = this.head;

			// iterate to the end of the
			// list
			while (current.next) {
				current = current.next;
			}

			// add node
			current.next = node;
		}
		this.size++;
	}

	// insert element at the position index
	// of the list
	insertAt(element, index) {
		if (index < 0 || index > this.size)
			return console.log("Please enter a valid index.");
		else {
			// creates a new node
			var node = new Node(element);
			var curr, prev;

			curr = this.head;

			// add the element to the
			// first index
			if (index == 0) {
				node.next = this.head;
				this.head = node;
			} else {
				curr = this.head;
				var it = 0;

				// iterate over the list to find
				// the position to insert
				while (it < index) {
					it++;
					prev = curr;
					curr = curr.next;
				}

				// adding an element
				node.next = curr;
				prev.next = node;
			}
			this.size++;
		}
	}

	// removes an element from the
	// specified location
	removeFrom(index) {
		if (index < 0 || index >= this.size)
			return console.log("Please Enter a valid index");
		else {
			var curr, prev, it = 0;
			curr = this.head;
			prev = curr;

			// deleting first element
			if (index === 0) {
				this.head = curr.next;
			} else {
				// iterate over the list to the
				// position to removce an element
				while (it < index) {
					it++;
					prev = curr;
					curr = curr.next;
				}

				// remove the element
				prev.next = curr.next;
			}
			this.size--;

			// return the remove element
			return curr.element;
		}
	}

	// removes a given element from the
	// list
	removeElement(element) {
		var current = this.head;
		var prev = null;

		// iterate over the list
		while (current != null) {
			// comparing element with current
			// element if found then remove the
			// and return true
			if (current.element === element) {
				if (prev == null) {
					this.head = current.next;
				} else {
					prev.next = current.next;
				}
				this.size--;
				return current.element;
			}
			prev = current;
			current = current.next;
		}
		return -1;
	}


	// finds the index of element
	indexOf(element) {
		var count = 0;
		var current = this.head;

		// iterae over the list
		while (current != null) {
			// compare each element of the list
			// with given element
			if (current.element === element)
				return count;
			count++;
			current = current.next;
		}

		// not found
		return -1;
	}

	// checks the list for empty
	isEmpty() {
		return this.size == 0;
	}

	// gives the size of the list
	size_of_list() {
		console.log(this.size);
	}


	// prints the list items
	printList() {
		var curr = this.head;
		var str = "";
		while (curr) {
			str += curr.element + " ";
			curr = curr.next;
		}
		console.log(str);
	}

}

// creating an object for the
// Linkedlist class
var ll = new LinkedList();

// testing isEmpty on an empty list
// returns true
console.log(ll.isEmpty());

// adding element to the list
ll.add(10);

// prints 10
ll.printList();

// returns 1
console.log(ll.size_of_list());

// adding more elements to the list
ll.add(20);
ll.add(30);
ll.add(40);
ll.add(50);

// returns 10 20 30 40 50
ll.printList();

// prints 50 from the list
console.log("is element removed ?" + ll.removeElement(50));

// prints 10 20 30 40
ll.printList();

// returns 3
console.log("Index of 40 " + ll.indexOf(40));

// insert 60 at second position
// ll contains 10 20 60 30 40
ll.insertAt(60, 2);

ll.printList();

// returns false
console.log("is List Empty ? " + ll.isEmpty());

// remove 3rd element from the list
console.log(ll.removeFrom(3));

// prints 10 20 60 40
ll.printList();

```

## Implement with Javascript (ES5)

```js
function Node(data) {
  this.data = data;
  this.next = null;
}

function append(a,b) {
  if(!a)return b;
  a.next=append(a.next,b);
  return a;
}
```



## Implement with Python

```python
class Node(object):
    def __init__(self, data):
        self.data = data
        self.next = None

def push(head, data):
    return Node(data, head)
  
def build_one_two_three():
    return Node(1, Node(2, Node(3)))

def get_nth(node, index):
    v = -1
    n = node
    while n:
        v += 1
        if v == index:
            return n
        n = n.next
    raise ValueError     
    
def length(node):
    leng = 0
    while node:
        leng += 1
        node = node.next
    return leng
  
def count(node, data):
    c = 0
    while node:
        if node.data==data:
            c += 1
        node = node.next
    return c

def insert_nth(head, index, data):
  if index == 0: return Node(data, head)
  if head and index > 0:
    head.next = insert_nth(head.next, index - 1, data)
    return head
  raise ValueError

def append(listA, listB):
  return listB if not listA else Node(listA.data, append(listA.next, listB))    

def remove_duplicates(head):
    if head == None:
        return head
    current = head
    next = current.next
    while next:
        if current.data == next.data:
            current.next = current.next.next
            next = current.next
        else:
            current = next
            next = current.next
    return head

#sortedInsert(1 -> 2 -> 3 -> null, 4) === 1 -> 2 -> 3 -> 4 -> null)
#sortedInsert(1 -> 7 -> 8 -> null, 5) === 1 -> 5 -> 7 -> 8 -> null)
#sortedInsert(3 -> 5 -> 9 -> null, 7) === 3 -> 5 -> 7 -> 9 -> null)
def sorted_insert(head, data):
  if not head or data < head.data: return Node(data, head)
  else:
    head.next = sorted_insert(head.next, data)
    return head

#var list = 4 -> 2 -> 1 -> 3 -> 8 -> 9 -> null
#mergeSort(list) === 1 -> 2 -> 3 -> 4 -> 8 -> 9 -> null
def merge_sort(list):
    if not list or not list.next: return list
    front, back = Node(), Node()
    front_back_split(list, front, back)
    return sorted_merge(merge_sort(front), merge_sort(back))
```



## Implement with Java

```java
class Node {

  int data;
  Node next = null;
  
  Node(final int data) {
    this.data = data;
  }
  
  public static Node push(final Node head, final int data) {
    Node node = new Node(data);
    node.next = head;
    return node;    
  }
  
  public static Node buildOneTwoThree() {
    Node chained = null;
    chained = push(chained, 3);
    chained = push(chained, 2);
    chained = push(chained, 1);
    return chained;
  }
    
   public static int getNth(Node n, int index) throws Exception{
     if(index==0)return n.data; 
     else return getNth(n.next,index-1);
  }
    
   public Node(int data, Node next) {
    this.data = data;
    this.next = next;
  }

  public static Node append(Node listA, Node listB) {
    if ( listA == null ) {
      return listB;
    }
    Node tmp = listA;
    while ( tmp.next != null ) {
      tmp = tmp.next;
    }
    tmp.next = listB;
    return listA;
  }
    
  
}
```



## Implement with Rust

```rust

```



## Implement with C++

```c++
/* Node Definition*/
struct Node {
  Node * next;
  int data;
}


int Length(Node *head)
{
  int l = 0;
  while(head != NULL) {
    l++;
    head = head->next;
  }
  return l;
}

int Count(Node *head, int data)
{
  int c = 0;
  while(head != NULL){
    if(head->data == data) c++;
    head = head->next;
  }
  return c;
}
```

