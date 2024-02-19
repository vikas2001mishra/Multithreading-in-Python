# Multithreading-in-Python


# Multi Threding:
             #Multi Tasking - Execution of several tasks simultaneously
                    #1. Process based multi tasksing
                    #2. Thread based multi tasking
            #1. Process based multi tasking Each task is seperate independent process
            #2. Thread based multi tasksing - 10000 - 5000 not dependent on rest of 5000

# Advantage - Reduces the time and increase the performance

# Python provides inbuilt mult threading
# threading - module

# Thread:
    #1. Flow of execution
    #2. For every thread there is some jobs available
    #Single threaded program - Only one thread
    #Multiple thred - multiple flows


# Our 1st Program:

import threading
print('current executing thred:',threading.current_thread().getName())



# from threading import current_thread, Thread

# There are 3 ways to create multiple threads
       #1. Creating a thread without using any class
       #2. Creating a thread by extending thread class
       #3. Creating a thread without extending thread class


# For Example:

import threading
import time
def func(seconds):
    print(f'sleep for {seconds} seconds')
    time.sleep(seconds)
func(4)
func(2)
func(1)



# creating a thread without any class


from threading import *
def display():
    print('Display:',current_thread().getName())
t1 = Thread(target=display)
t2 = Thread(target=display)
t1.start()
t2.start()
print("This code executed by thred:",current_thread().getName())




# create a thred class extending thread class:


from threading import *
class MyThread(Thread):
    def run(self):
        for i in range(10):
            print('child thred')
t = MyThread()
t.start()
for i in range(10):
    print('main thred')





# create a thred class without extending thread class:

class Test:
    def display(self):
        for i in range(10):
            print('Child thred', current_thread().getName())
obj = Test()
t = Thread(target=obj.display())
t.start()
for i in range(10):
    print('main thread',current_thread().getName())



# .


from threading import *
print(current_thread().getName())
current_thread().setName('Sagar')
print(current_thread().getName())
print(current_thread().name)



# .


from threading import *
import time
def Display():
    print(current_thread().name,'Started')
    time.sleep(4)
    print(current_thread().name,'Ended')
print('How many active threads are there:',active_count())
t1 = Thread(target=Display(),name = 'child thread1')
t2 = Thread(target=Display(),name = 'child thread1')
t3 = Thread(target=Display(),name = 'child thread1')
t1.start()
t2.start()
t3.start()
print('How many active threads are there:',active_count())
time.sleep(10)
print('How many active threads are there:',active_count())



# .


from threading import  *
import time
def display():
    for i in range(10):
        print('A thread')
        time.sleep(2)
t = Thread(target=display())
t.start()
for i in range(10):
    print('B thread')




# join() method



from threading import  *
import time
def display():
    for i in range(10):
        print('A thread')
        time.sleep(2)
t = Thread(target=display())
t.start()
t.join()
for i in range(10):
    print('B thread')




# without sleep (parellel)


without sleep (parellel)

from threading import  *
import time
def display():
    for i in range(10):
        print('A thread')
t = Thread(target=display())
t.start()
t.join()
for i in range(10):
    print('B thread')





# Daemon Thread


from threading import *
print(current_thread().getName())
print(current_thread().isDaemon())
current_thread().setDaemon(True)


# .


from threading import *
def job():
    print("Child thread")
t = Thread(target=job())
print(t.daemon)
t.setDaemon(True)
print(t.daemon)


# .

from threading import *
import time
def job():
    for i in range(10):
        print("A Thred")
        time.sleep(2)
t = Thread(target=job())
t.start()
time.sleep(4)
print("End of Main Thread")




# .

from threading import *
import time
def job():
    for i in range(10):
        print("A Thred")
        time.sleep(2)
t = Thread(target=job())
t.start()
time.sleep(4)
print("End of Main Thread")




# Synchronization

# Lock
# RLock = Reentrance
# Semaphore



# Lock


from threading import *
import time
def greeting(name):
    for i in range(5):
        print("Good Morning ",end='')
        time.sleep(2)
        print(name)
t1 = Thread(target=greeting,args= ('Aman',))
t2 = Thread(target=greeting,args= ('Ajay',))
t1.start()
t2.start()


# .

from threading import *
import time
l = Lock()
def greeting(name):
    l.acquire()
    for i in range(5):
        print('Good Morning ',end='')
        time.sleep(1)
        print(name)
    l.release()
t1 = Thread(target=greeting,args=('Ram',))
t2 = Thread(target=greeting,args=('Shyam',))
t3 = Thread(target=greeting,args=('Rohan',))
t4 = Thread(target=greeting,args=('Pritam',))
t5 = Thread(target=greeting,args=('Sagar',))
t1.start()
t2.start()
t3.start()
t4.start()
t5.start()



# .

from threading import *
l = Lock()
print('Main thread acquire the lock')
l.acquire()
print('Main thread release the lock')
l.release()




# RLock


from threading import *
l = Lock()
print('Main thread trying to acquire the lock...')
l.acquire()
print('Main thread trying to release the lock...')
l.release()



# .

from  threading import *
import time
l = RLock()
def factorial(n):
    l.acquire()
    if n==0:
        result = 1
    else:
        result = n*factorial(n-1)
    l.release()
    return result
def results(n):
    print('the factorial of',n,'is:',factorial(n))
t1 = Thread(target=results,args= (5,))
t2 = Thread(target=results,args= (6,))
t1.start()
t2.start()




# Semaphore


from threading import *
import time
s = Semaphore()
def greeting(name):
    s.acquire()
    for i in range(4):
        print('Good Evening:',end='')
        time.sleep(2)
        print(name)
    s.release()
t1 = Thread(target=greeting,args=('Rahul',))
t2 = Thread(target=greeting,args=('Rohit',))
t3 = Thread(target=greeting,args=('Mahesh',))
t4 = Thread(target=greeting,args=('Laxmi',))
t1.start()
t2.start()
t3.start()
t4.start()





# InterThread Communication

# Event
# Condition
# Queue

# Event..
  #Set() - Interal flag values True - Green Signal
  #clear() - false - Red Signal
  #isSet() - Event is Set or not
  #wait() - Thread can wait until event get set




from threading import *
import time
e = Event()
def Consumer():
    print('consumer waiting for creation of the bread')
    e.wait()
    print('consumer purchased the bread and consuming it')

def Producer():
    time.sleep(2)
    print('producer producing the bread')
    print('producer giving the information by setting the event')
    e.set()
t1 = Thread(target=Consumer)
t2 = Thread(target=Producer)
t1.start()
t2.start()






# .

from threading import *
import time
e = Event()
def TrafficPolice():
    while True:
        time.sleep(5)
        print('Traffic Police giving Green Signal')
        e.set()
        time.sleep(5)
        print('Traffic Police giving Red Signal')
        e.clear()

def Driver():
    num = 0
    while True:
        print('Driver waiting for the green signal')
        e.wait()
        print('Traffic signal is Green Vehicle can move')
        while e.isSet():
            num = num+1
            print('Vehicle number:',num,'Crossing the signal')
            time.sleep(2)
        print('Traffic signal is Red Drivers have to wait')

t1 = Thread(target=TrafficPolice)
t2 = Thread(target=Driver)
t1.start()
t2.start()





# Condition:
         #Condition based Communication
         #Condition Object is always associated with Rlock
         #acquire
         #Release

# Methods:
        #acquire
        #release
        #wait
        #c.notifyALL()





from threading import *
def Consumer(c):
    c.acquire()
    print('Consumer waiting for updation')
    c.wait()
    print('Consumer got the notification and consuming the item')
    c.release()

def Producer(c):
    c.acquire()
    print('Producer producing the item')
    print('Producer giving the notification')
    c.notify()
    c.release()

c = Condition()
t1 = Thread(target=Consumer,args=(c,))
t2 = Thread(target=Producer,args=(c,))
t1.start()
t2.start()




# .

from threading import *
import time
import random
items = []
def Producer(c):
    while True:
        c.acquire()
        item = random.randint(1,100)
        print('Producer producing the item',item)
        items.append(item)
        print('Producer giving the information')
        c.notify()
        c.release()
        time.sleep(5)

def Consumer(c):
    while True:
        c.acquire()
        print('Consumer waiting for updation....')
        c.wait()
        print('Consumer Consuming the item:',items.pop())
        c.release()
        time.sleep(5)
c = Condition()
t1 = Thread(target=Producer,args=(c,))
t2 = Thread(target=Consumer,args=(c,))
t1.start()
t2.start()






# Interthread comm by using queue
      #Queue enternally has condition object
      #that condition has lock object

# Queue - not have to worry about Lock,sync,and notification
# q.put() - waiting concept - if queue is full put will call wait automatically



from threading import *
import random
import time
import queue
def Producer(q):
    while True:
        item = random.randint(1,100)
        print('Producer producing trhe item',item)
        q.put(item)
        print('Producer giving the notification')
        time.sleep(5)
def Consumer(q):
    while True:
        print('Consumer waiting for the updation')
        print('Consumer consuming item',q.get())
        time.sleep(5)

q = queue.Queue()
t1 = Thread(target=Producer,args=(q,))
t2 = Thread(target=Consumer,args=(q,))
t1.start()
t2.start()






# Python supports 3 types of Queue
        # FIFO
        # LIFO
        # Priority Queue


# FIFO

import queue
q = queue.Queue()
q.put(10)
q.put(9)
q.put(12)
q.put(98)
q.put(7)
while not q.empty():
    print(q.get(),end=' ')



# LIFO

import queue
q = queue.LifoQueue()
q.put(10)
q.put(9)
q.put(12)
q.put(98)
q.put(7)
while not q.empty():
    print(q.get(),end=' ')








# Priority Queue

import queue
q = queue.PriorityQueue()
q.put(5, 'Ram')
q.put(3, 'Shyam')
q.put(1, 'Mohan')
q.put(4, 'Ghanshyam')
q.put(2, 'Sumit')
while not q.empty():
    print(q.get(),end=' '



# .


import queue
q = queue.PriorityQueue()
q.put((5, 'Ram'))
q.put((3, 'Shyam'))
q.put((1, 'Mohan'))
q.put((4, 'Ghanshyam'))
q.put((2, 'Sumit'))
while not q.empty():
    print(q.get(),end=' ')



# .


import queue
q = queue.PriorityQueue()
q.put((5, 'Ram'))
q.put((3, 'Shyam'))
q.put((1, 'Mohan'))
q.put((4, 'Ghanshyam'))
q.put((2, 'Sumit'))
while not q.empty():
    print(q.get()[1],end=' ')














