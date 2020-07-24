# [Design Circular Deque](https://leetcode-cn.com/problems/design-circular-deque/)

## Description

设计实现双端队列。
你的实现需要支持以下操作：

* MyCircularDeque(k)：构造函数,双端队列的大小为k。
* insertFront()：将一个元素添加到双端队列头部。 如果操作成功返回 true。
* insertLast()：将一个元素添加到双端队列尾部。如果操作成功返回 true。
* deleteFront()：从双端队列头部删除一个元素。 如果操作成功返回 true。
* deleteLast()：从双端队列尾部删除一个元素。如果操作成功返回 true。
* getFront()：从双端队列头部获得一个元素。如果双端队列为空，返回 -1。
* getRear()：获得双端队列的最后一个元素。 如果双端队列为空，返回 -1。
* isEmpty()：检查双端队列是否为空。
* isFull()：检查双端队列是否满了。

### Example:

````
MyCircularDeque circularDeque = new MycircularDeque(3); // 设置容量大小为3
circularDeque.insertLast(1);			        // 返回 true
circularDeque.insertLast(2);			        // 返回 true
circularDeque.insertFront(3);			        // 返回 true
circularDeque.insertFront(4);			        // 已经满了，返回 false
circularDeque.getRear();  				// 返回 2
circularDeque.isFull();				        // 返回 true
circularDeque.deleteLast();			        // 返回 true
circularDeque.insertFront(4);			        // 返回 true
circularDeque.getFront();				// 返回 4
````

## 思路 :whale:

循环队列。注意区分空队列、满队列，队列有一个值时情况。

## 代码
```` Go
type MyCircularDeque struct {
    arr      []int
	head    int // 往前走 -1
	tail     int // 往后走 +1
	capacity int
}


/** Initialize your data structure here. Set the size of the deque to be k. */
func Constructor(k int) MyCircularDeque {
    capacity := k + 1
	return MyCircularDeque{
		arr:      make([]int, capacity),
		capacity: capacity,
	}
}


/** Adds an item at the front of Deque. Return true if the operation is successful. */
func (this *MyCircularDeque) InsertFront(value int) bool {
    if this.IsFull() {
        return false
    }
    this.head = (this.head-1+this.capacity)%this.capacity
    this.arr[this.head] = value
    return true
}


/** Adds an item at the rear of Deque. Return true if the operation is successful. */
func (this *MyCircularDeque) InsertLast(value int) bool {
    if this.IsFull() {
        return false
    }
    this.arr[this.tail] = value
    this.tail = (this.tail+1)%this.capacity
    return true
}


/** Deletes an item from the front of Deque. Return true if the operation is successful. */
func (this *MyCircularDeque) DeleteFront() bool {
    if this.IsEmpty() {
        return false
    }
    this.head = (this.head+1)%this.capacity
    return true
}


/** Deletes an item from the rear of Deque. Return true if the operation is successful. */
func (this *MyCircularDeque) DeleteLast() bool {
    if this.IsEmpty() {
        return false
    }
    this.tail = (this.tail-1+this.capacity)%this.capacity
    return true
}


/** Get the front item from the deque. */
func (this *MyCircularDeque) GetFront() int {
    if this.IsEmpty() {
        return -1
    }
    return this.arr[this.head]
}


/** Get the last item from the deque. */
func (this *MyCircularDeque) GetRear() int {
        if this.IsEmpty() {
        return -1
    }
    return this.arr[(this.tail-1+this.capacity)%this.capacity]
}


/** Checks whether the circular deque is empty or not. */
func (this *MyCircularDeque) IsEmpty() bool {
    return this.head  == this.tail
}


/** Checks whether the circular deque is full or not. */
func (this *MyCircularDeque) IsFull() bool {
    return (this.tail+1) % this.capacity == this.head 
}


/**
 * Your MyCircularDeque object will be instantiated and called as such:
 * obj := Constructor(k);
 * param_1 := obj.InsertFront(value);
 * param_2 := obj.InsertLast(value);
 * param_3 := obj.DeleteFront();
 * param_4 := obj.DeleteLast();
 * param_5 := obj.GetFront();
 * param_6 := obj.GetRear();
 * param_7 := obj.IsEmpty();
 * param_8 := obj.IsFull();
 */
````

