# Singly_Linked_Lists_Data_Structure




> ## Node class creation: :wink:

``` js
class Node{
    constructor(val){
        this.val = val;
        this.next = null;
    }
}
```

> ## class method creation for Singly_Linked_List: :wink:
// push(), pop(), shift(), unshift(), set(), insert(), remove(), reverse(), print() implementation

``` js
class SinglyLinkedList{
    constructor(){
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
    push(val){
        var newNode = new Node(val);
        if(!this.head){
            this.head = newNode;
            this.tail = this.head;
        } else {
            this.tail.next = newNode;
            this.tail = newNode;
        }
        this.length++;
        return this;
    }

    pop(){
        if(!this.head) return undefined;
        var current = this.head;
        var newTail = current;
        while(current.next){
            newTail = current;
            current = current.next;
        }
        this.tail = newTail;
        this.tail.next = null;
        this.length--;
        if(this.length === 0){
            this.head = null;
            this.tail = null;
        }
        return current;
    }

    shift(){
        if(!this.head) return undefined;
        var currentHead = this.head;
        this.head = currentHead.next;
        this.length--;
        if(this.length === 0){
            this.tail = null;
        }
        return currentHead;
    }

    unshift(val){
        var newNode = new Node(val);
        if(!this.head) {
            this.head = newNode;
            this.tail = this.head;
        } else {
            newNode.next = this.head;
            this.head = newNode;
        }
        this.length++;
        return this;
    }

    get(index){
        if(index < 0 || index >= this.length) return null;
        var counter = 0;
        var current = this.head;
        while(counter !== index){
            current = current.next;
            counter++;
        }
        return current;
    }

    set(index, val){
        var foundNode = this.get(index);
        if(foundNode){
            foundNode.val = val;
            return true;
        }
        return false;
    }

    insert(index, val){
        if(index < 0 || index > this.length) return false;
        if(index === this.length) return !!this.push(val);
        if(index === 0) return !!this.unshift(val);
        
        var newNode = new Node(val);
        var prev = this.get(index - 1);
        var temp = prev.next;
        prev.next = newNode;
        newNode.next = temp;
        this.length++;
        return true;
    }

    remove(index){
        if(index < 0 || index >= this.length) return undefined;
        if(index === 0) return this.shift();
        if(index === this.length - 1) return this.pop();
        var previousNode = this.get(index - 1);
        var removed = previousNode.next;
        previousNode.next = removed.next;
        this.length--;
        return removed;
    }

    reverse(){
      var node = this.head;
      this.head = this.tail;
      this.tail = node;
      var next;
      var prev = null;
      for(var i = 0; i < this.length; i++){
        next = node.next;
        node.next = prev;
        prev = node;
        node = next;
      }
      return this;
    }

    print(){
        var arr = [];
        var current = this.head
        while(current){
            arr.push(current.val)
            current = current.next
        }
        console.log(arr);
    }
}

```

> ## Running the code and results: :laughing:
``` js
var list = new SinglyLinkedList()
console.log(list.head, list.tail, list.length)
// null null 0
list.push("HELLO")
console.log(list.head, list.tail, list.length)
// Node { val: 'HELLO', next: null } Node { val: 'HELLO', next: null } 1
list.push("GOODBYE")
list.push("See You Later!")
console.log(list.head, list.tail, list.length)
// Node {
//   val: 'HELLO',
//   next: Node {
//     val: 'GOODBYE',
//     next: Node { val: 'See You Later!', next: null }
//   }
// } Node { val: 'See You Later!', next: null }
list.pop()
console.log(list.head, list.tail, list.length)
// Node { val: 'HELLO', next: Node { val: 'GOODBYE', next: null } } Node { val: 'GOODBYE', next: null } 2
list.push("one more hello!")
list.shift()
console.log(list.head, list.tail, list.length)
// Node {
//   val: 'GOODBYE',
//   next: Node { val: 'one more hello!', next: null }
// } Node { val: 'one more hello!', next: null } 2
list.pop()
list.pop()
console.log(list.head, list.tail, list.length)
// null null 0
list.unshift('unshifted')
console.log(list.head, list.tail, list.length)
// Node { val: 'unshifted', next: null } Node { val: 'unshifted', next: null } 1
list.push('hi')
list.push('again!')
console.log(list.head, list.tail, list.length)
// Node {
//   val: 'unshifted',
//   next: Node { val: 'hi', next: Node { val: 'again!', next: null } }
// } Node { val: 'again!', next: null } 3

console.log(list.get(100))
// null
console.log(list.get(1))
// Node { val: 'hi', next: Node { val: 'again!', next: null } }

list.set(1,'hiHI!!!')
console.log(list.get(1))
// Node { val: 'hiHI!!!', next: Node { val: 'again!', next: null } }
list.insert(1,'after index 1?')
console.log(list.get(0))
// Node {
//   val: 'unshifted',
//   next: Node {
//     val: 'after index 1?',
//     next: Node { val: 'hiHI!!!', next: [Node] }
//   }
// }
console.log(list.get(1))
// Node {
//   val: 'after index 1?',
//   next: Node { val: 'hiHI!!!', next: Node { val: 'again!', next: null } }
// }
console.log(list.get(2))
// Node { val: 'hiHI!!!', next: Node { val: 'again!', next: null } }
console.log(list.get(3))
// Node { val: 'again!', next: null }
console.log(list.head, list.tail, list.length)
// Node {
//   val: 'unshifted',
//   next: Node {
//     val: 'after index 1?',
//     next: Node { val: 'hiHI!!!', next: [Node] }
//   }
// } Node { val: 'again!', next: null } 4
list.remove(1)
console.log(list.head, list.tail, list.length)
// Node {
//   val: 'unshifted',
//   next: Node { val: 'hiHI!!!', next: Node { val: 'again!', next: null } }
// } Node { val: 'again!', next: null } 3
```

![singly_linked_lists_0](https://github.com/NoriKaneshige/Singly_Linked_Lists_Data_Structure/blob/master/singly_linked_lists_0.png)
![singly_linked_lists_push](https://github.com/NoriKaneshige/Singly_Linked_Lists_Data_Structure/blob/master/singly_linked_lists_push.png)

![singly_linked_lists_pop](https://github.com/NoriKaneshige/Singly_Linked_Lists_Data_Structure/blob/master/singly_linked_lists_pop.png)
![singly_linked_lists_shift](https://github.com/NoriKaneshige/Singly_Linked_Lists_Data_Structure/blob/master/singly_linked_lists_shift.png)
![singly_linked_lists_unshift](https://github.com/NoriKaneshige/Singly_Linked_Lists_Data_Structure/blob/master/singly_linked_lists_unshift.png)
![singly_linked_lists_get](https://github.com/NoriKaneshige/Singly_Linked_Lists_Data_Structure/blob/master/singly_linked_lists_get.png)
![singly_linked_lists_set](https://github.com/NoriKaneshige/Singly_Linked_Lists_Data_Structure/blob/master/singly_linked_lists_set.png)
![singly_linked_lists_insert](https://github.com/NoriKaneshige/Singly_Linked_Lists_Data_Structure/blob/master/singly_linked_lists_insert.png)
![singly_linked_lists_remove](https://github.com/NoriKaneshige/Singly_Linked_Lists_Data_Structure/blob/master/singly_linked_lists_remove.png)
![singly_linked_lists_reverse_1](https://github.com/NoriKaneshige/Singly_Linked_Lists_Data_Structure/blob/master/singly_linked_lists_reverse_1.png)
![singly_linked_lists_reverse_2](https://github.com/NoriKaneshige/Singly_Linked_Lists_Data_Structure/blob/master/singly_linked_lists_reverse_2.png)
![singly_linked_lists_BogO](https://github.com/NoriKaneshige/Singly_Linked_Lists_Data_Structure/blob/master/singly_linked_lists_BogO.png)
