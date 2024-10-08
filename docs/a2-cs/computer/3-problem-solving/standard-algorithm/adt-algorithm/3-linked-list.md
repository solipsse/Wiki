# linklist

```python exec='1' source='tabbed-left'
NULL = -1

class Node:
    def __init__(self):
        self.data = None
        self.ptr = None

class LinkedList:
    global NULL
    def __init__(self):
        self.startptr = NULL
        self.freeptr = 0
        self.list = [Node() for _ in range(8)] # can't use * 8 here because it will create 1 instance of node and duplicate them
        for i in range(7):
            self.list[i].ptr = i + 1
        self.list[7].ptr = NULL

    def insert(self, key):
        if self.freeptr == NULL:
            return -1
        nodeptr = self.freeptr
        self.list[nodeptr].data = key
        self.freeptr = self.list[self.freeptr].ptr

        prevptr = NULL
        thisptr = self.startptr
        while thisptr != NULL and key > self.list[thisptr].data:
            prevptr = thisptr
            thisptr = self.list[thisptr].ptr

        if prevptr == NULL:
            self.list[nodeptr].ptr = self.startptr
            self.startptr = nodeptr
            return 0

        self.list[nodeptr].ptr = thisptr
        self.list[prevptr].ptr = nodeptr
        return 0

    def find(self, key):
        thisptr = self.startptr
        while thisptr != NULL and self.list[thisptr].data != key:
            thisptr = self.list[thisptr].ptr
        return thisptr

    def delete(self, key):
        prevptr = NULL
        thisptr = self.startptr
        while thisptr != NULL and self.list[thisptr].data != key:
            prevptr = thisptr
            thisptr = self.list[thisptr].ptr

        if thisptr == NULL:
            return -1

        if thisptr == self.startptr:
            self.startptr  = self.list[self.startptr].ptr
        else:
            self.list[prevptr].ptr = self.list[thisptr].ptr

        self.list[thisptr].ptr = self.freeptr
        self.freeptr = thisptr
```