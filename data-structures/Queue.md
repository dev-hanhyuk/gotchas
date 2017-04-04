# Queue
The Queue ADT is a container for multiple ordered elements.

## Methods
* enqueue
* dequeue
* size

## JavaScript Implementation
```javascript

function Queue() {
  this.data = [];
  this.head = this.tail = 0;
}

Queue.prototype.enqueue = function(val) {
  this.data[this.tail] = val;
  this.tail++;
}

Queue.prototype.dequeue = function() {
  if (!this.size()) return;
  let value = this.data[this.head++];

  if (this.head > 99) {
    this.data = this.data.slice(this.head);
    this.tail = this.tail - this.head;
    this.head = 0;
  }
  return value;
}

Queue.prototype.size = function() {
  return this.tail - this.head;
}

```