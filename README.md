import time

class Queue:
    def __init__(self, max_size=10):
        self.queue = []
        self.max_size = max_size

    def enqueue(self, item):
        if len(self.queue) >= self.max_size:
            print("Queue is Full!")
            return
        self.queue.append(item)
        print(f"enqueue('{item}')")
        self.print_queue()

    def dequeue(self):
        if self.isEmpty():
            print("Queue is Empty!")
            return None
        item = self.queue.pop(0)
        print(f"dequeue() -> '{item}'")
        self.print_queue()
        return item

    def front(self):
        if self.isEmpty():
            print("Queue is Empty!")
            return None
        print(f"front() -> '{self.queue[0]}'")
        return self.queue[0]

    def isEmpty(self):
        return len(self.queue) == 0

    def clear(self):
        self.queue.clear()
        print("clear()")
        self.print_queue()

    def print_queue(self):
        print("현재 Queue 상태:")
        if self.isEmpty():
            print("[ empty ]")
        else:
            for item in self.queue:
                print(f"[ {item} ]")
        print("-" * 30)
        time.sleep(1)

