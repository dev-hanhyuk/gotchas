# Binary Search Tree
It is a Search tree if all nodes respect an order: all values less than a given node value are in its left subtree, and all values greater or equal to a given node value are stored in its right subtree. For every node you jump, you are on average throwing away half of the remaining nodes in your search. This means that for a (balanced) tree of n nodes, you will find the minimum in an average of log2(n) moves. Log2(n) grows very very slowly with respect to n. In the worst case, a "degenerate" tree is just a linked list.


## Methods
* insert
* contains
* size
* depthFirstForEach
* breadthFirstForEach


## Traversal
A classic problem for trees is how to traverse them — i.e., visit and process every node. There are four flavors of tree traversal:

* Breadth-first: start at level 0, then go through all nodes at level 1, then all nodes at level 2, etc. This is meaningful when tree level actually has some meaning; for example, a hierarchical org chart. It is less useful for a BST, where levels don't usually have intrinsic meaning.

* Depth-first: go down paths to certain stopping points before moving on to the next branch. Three types:
  * pre-order: process the current node value, then go down the left branch, then the right branch. This processes parents before leaves, so can be used to copy a tree.
  * in-order: process all the left children (lesser values), then this node's value, then the right children (greater values). This is the most useful for a BST as it respects the intrinsic ordering of the tree; values are processed from smallest to greatest.
  * post-order: process all the left children, then right children, then this node's value. This processes leaves before parents, so can be used in languages with explicit memory management to delete nodes in a safe way.


## JavaScript Implementation

```javascript

function BST(val) {
  this.value = val;
  this.size = 1;
}

BST.prototype.insert = function(val) {
  this.size ++;
  let direction = val < this.value ? 'left' : 'right';
  if (!this[direction]) this[direction] = new BST(val);
  else this[direction].insert(val);
}

BST.prototype.contains = function(val) {
  if (this.value == val) return true;
  let direction = val < this.value ? 'left' : 'right';
  if (this[direction]) this[direction].contains(val);
  else return false;
}

BST.prototype.size = function() {
  return this.size;
}

BST.prototype.depthFirstForEach = function(iterator, order) {
  if (order === 'pre-order') iterator(this.value);
  if (this.left) this.left.depthFirstForEach(iterator, order);
  if (!order || order === 'in-order') iterator(this.value);
  if (this.right) this.right.depthFirstForEach(iterator, order);
  if (order === 'post-order') iterator(this.value);
}

BST.prototype.breadthFirstForEach = function(iterator) {
  var queue = [ this ];
  var tree;
  while (queue.length) {
    tree = this.shift();
    iterator(tree.value);
    if (tree.left) queue.push(tree.left);
    if (tree.right) queue.push(tree.right);
  }
}

```