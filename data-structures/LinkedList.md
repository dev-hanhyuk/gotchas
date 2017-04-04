# Linked List
Linked Lists are collections of nodes — wrapper structures which encapsulate a value and one or more pointers (references) to other nodes.

## Methods
* addToTail
* removeTail
* addToHead
* removeHead

## Traversal


## JavaScript Implementation
```javascript

function Node(val, prev, next) {
  this.value = val;
  this.previous = prev || null;
  this.next = next || null;
}

function LinkedList() {}

LinkedList.prototype.addToTail = function(val) {
  let newNode = new Node(val, this.tail);
  if (this.tail) this.tail.next = newNode;
  // if there is no previous tail == no previous item => CASE: this.head = this.tail
  else this.head = newNode;
  this.tail = newNode;
}

LinkedList.prototype.removeTail = function() {
  if (!this.tail) return;
  let oldTail = this.tail.value;
  this.tail = this.tail.previous;
  if (this.tail) this.tail.next = null;
  else this.head = null;
  return oldTail;
}

LinkedList.prototype.addToHead = function(val) {
  let newNode = new Node(val, null, this.head);
  if (this.head) this.head.previous = newNode;
  // if there is no previous head == no previous item => CASE: this.head = this.tail
  else this.tail = newNode;
  this.head = newNode;
}

LinkedList.prototype.removeHead = function() {
  if (!this.head) return;
  let oldHead = this.head.value;
  this.head = this.head.next;
  if (this.head) this.head.previous = null;
  else this.tail = null; // no item exists after removing the only one item
  return oldHead;
}

LinkedList.prototype.search = function(val) {
  var currentNode = this.head;
  while (currentNode) {
    if (currentNode.value == val) return currentNode.value;
    currentNode = currentNode.next;
  }
  return null;
}

```