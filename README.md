import time
import os
import csv

class Queue:
    def __init__(self, max_size=10):
        self.queue = []
        self.max_size = max_size

    def enqueue(self, item):
        if len(self.queue) >= self.max_size:
            print("Queue is Full!")
            time.sleep(1)
            return
        print(f"\n▶ enqueue('{item}')")
        self.queue.append(item)
        self.print_queue()

    def dequeue(self):
        if self.isEmpty():
            print("Queue is Empty!")
            time.sleep(1)
            return None
        item = self.queue.pop(0)
        print(f"\n▶ dequeue() -> '{item}'")
        self.print_queue()
        return item

    def front(self):
        if self.isEmpty():
            print("Queue is Empty!")
            time.sleep(1)
            return None
        print(f"\n▶ front() -> '{self.queue[0]}'")
        time.sleep(1)
        return self.queue[0]

    def isEmpty(self):
        return len(self.queue) == 0

    def clear(self):
        print("\n▶ clear()")
        self.queue.clear()
        self.print_queue()

    def print_queue(self):
        os.system('cls' if os.name == 'nt' else 'clear')
        print("📦 현재 Queue 상태:\n")
        if self.isEmpty():
            print("[ empty ]")
        else:
            for item in self.queue:
                print(f"[ {item} ]")
        print("\n" + "-" * 30)
        time.sleep(1)


with open("data.csv", "w", newline="", encoding="utf-8") as f:
    writer = csv.writer(f)
    writer.writerow(["이름","학번","메뉴1","메뉴2","메뉴3"])
    writer.writerow(["팀원1","20231234","초코맛 바스크치케이크","카푸치노","디카페인 아메리카노"])
    writer.writerow(["팀원2","20231235","카페라떼","티라미수","아이스초코"])
    writer.writerow(["팀원3","20231236","아메리카노","마카롱","녹차라떼"])


q = Queue(10)

print("🎬 CSV 파일에서 데이터 불러오는 중...\n")
time.sleep(1)

with open("data.csv", "r", encoding="utf-8") as f:
    reader = csv.reader(f)
    next(reader)

    for row in reader:
        name = row[0]
        menus = row[2:5]

        print(f"\n👤 {name}의 메뉴 추가 중...")
        time.sleep(1)

        for menu in menus:
            q.enqueue(menu)

q.front()
q.dequeue()

q.enqueue("카페라떼")
q.enqueue("티라미수")

print("\n▶ isEmpty() ->", q.isEmpty())
time.sleep(1)

q.clear()

print("\n▶ isEmpty() ->", q.isEmpty())
