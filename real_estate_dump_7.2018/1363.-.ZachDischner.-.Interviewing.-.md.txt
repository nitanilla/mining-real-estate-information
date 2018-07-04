Interview Questions
===========================================
I am an Aerospace Engineer by training/education, but I predomenantly write software day-in and day-out. I've interviewed quite a bit for a variety of positions; I wear many hats and generally am up for anything new and different. However this means I'm an expert in nothing, and a poor interviewee besides, so I get lots of practice going through the technical interviewing process!

Here's a compiled list of questions and exercis that I can remember, mostly the interesting stuff. Have at it. 

# Telephone
* *What is Integral Hold control?*
* *Describe how the Linux OS communicates with a USB device*
* *How does the Linux scheduler work?*
* *What is a functor? (C++)*
* *Tell me how you would design a (C/C++) process that communicates with two sensors, where you can request information from the two independantly and the two states of each are are used for a combined calculation.* Device responsiveness is often slow and has variable response time, while the process needs to run its calculation based on those two states at a repeatable and higher cadence.
* *How would you implement an `Ordered Dictionary` in Python (under the hood)?*
* *Does your Attitude Determination algo have a problem if it is using a star tracker and a horizon sensor and the star tracker goes offline?*
* *Name some attitude determination devices and discuss pros/cons of each*
* *How does a star tracker work?*
* *What is gimball lock?*
* *How does a CCD work? How is that different from a CMOS detector?*
* (Python) *Why is `list.pop(0)` slower than `list.pop()`?*
* (Python) *Would you expect a `NamedTuple`, a `Class`, or a `Dictionary` to be the fastest simple storage container and why?*
* (Python) *Describe two usages of `yeild`*
* *Why might you want to avoid passing a list as a keyword argument to a Python function?* 
* *How do you test your software?*
* *What is a good test?*
* *What is REST? What are the standard HTTP protocols?*
* *Describe the weakness of each P, I and D in PID control*
* *What is the stack and heap in C?*
* *What does `static` mean in the C language?*
* *What is a weakness of a macro in C/C++ versus typical functions?*
* *What is the integral of velocity?*
* *If you have a single unsigned byte, and right shift 4, what is the result?*
* *What is a pointer and what is it used for?*
* *What is a transfer function (context of controls)?*

# Behavorial
`#define TMATW "tell me about a time when"`

* *TMATW you failed*
    * *Tell me about another time* 
* *Walk me through a tough bug you encountered*
* *TMATW you disagreed with a superior*
* *TMATW you had a conflict with a coworker (senior and junior)*
* *TMATW you went above and beyond the call of duty*
* *Do you like working in teams or solo better?*
* *Describe your favorite manager, least favorite*
* *How do you feel?*
* *Describe when you had to deal with ambiguity*
* *What was the last thing you stayed up late working on?*
* *Tell me about your side projects*

# Whiteboard
* You are given an **Unrolled Linked List** data structure where each node contains a Python structure with a preallocated list. The goal is to utilize this structure so that it behaves just like a standard Python list:
<p><a href="https://commons.wikimedia.org/wiki/File:Unrolled_linked_lists_(1-8).PNG#/media/File:Unrolled_linked_lists_(1-8).PNG"><img src="https://upload.wikimedia.org/wikipedia/commons/1/16/Unrolled_linked_lists_%281-8%29.PNG" alt="Unrolled linked lists (1-8).PNG"></a><br>By <a href="//commons.wikimedia.org/w/index.php?title=User:Shigeru23&amp;action=edit&amp;redlink=1" class="new" title="User:Shigeru23 (page does not exist)">Shigeru23</a> - Made by uploader (ref:<a rel="nofollow" class="external autonumber" href="http://blogs.msdn.com/b/devdev/archive/2005/08/22/454887.aspx">[1]</a>), <a href="http://creativecommons.org/licenses/by-sa/3.0" title="Creative Commons Attribution-Share Alike 3.0">CC BY-SA 3.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=15016787">Link</a></p>

    * *Write a function to access the `ii`th element*
    * *Write a function to insert a value `value` into the `ii`th position*
    
    ```python
    ## pseudostructure for the nodes 
    class Node():
        MAXLEN  # Maximum (and allocated) size of the data array 
        next    # Next Node object 
        datalen # Length of data array in this linked list
        data    # Preallocated list of values
    
    def get(root,ii):
        #complete me
    
    def insert(root,ii,value):
        #complete me
    ``` 
* Design a ticket sales service - AKA ticketmaster

* **Word Transform** You are given a word, and want to transform it into a word (of equal length). You may only change one letter at a time, and each newly formed word must be a valid word in a provided dictionary `dict['word']= True, dict['zord'] = None`. *Determine the sequence of the fewest number of transformations required to transform word1 into word2*
    
    ```Ex:
    Bat --> Dog
    Bat -> Bag -> Bog -> Dog
    def wordTransform(source,dest):
        pass
    
    # Hint : Sounds like a shortest path problem...
    ```

* **Testbed** *Design a system to test/validate firmware for GPS devices such that when a developer makes new commits, the end result is a report containing test completion marks, and performance metrics* (Come up with performance metrics, hardware/software infrastructure, networking, automation framework, etc)

* **Space Shuttle** Suppose you are standing on the space shuttle outer hull in its circular orbit, and you throw a baseball directly behind the shuttle (opposite of its velocity direction). *What does the ball appear to do from your perspective*?  (make drawing)

* **Inertia Tracking** We have a spreadsheet full of parts with their individual masses and moments of inertia given. Parts can be assembled with and within other parts to create components, components can be assembled with components, etc. We want to model the parts and assembled systems. *Architect your software solution for how you would represent, access, change, and model the physical systems using this information* (Don't forget about the Transport Therom!)
 
* **Inclination Change** You are delivering a spacecraft from a LEO circular orbit to a GEO circular orbit. *If you wanted to also include an inclination change, where/when would you want to perform that maneuver? Draw it out*

* **BFS/DFS** *Implement a Breadth First Search algorithm* (I've done this two or three times, sometimes the prompt is obfuscated by a word-problem, but knowing how to do this is pretty standard)

* **Orbital Elements** *Draw the 6 Keplarian orbital elements and give their description*

* **Apoge DV** (Polar orbit drawn) *If you apply an instantanious cross-track delta-V right as the spacecraft crosses its peroapsis, what orbital elements change and describe/draw those changes* 

* **Pendulum EOM** *Derive the Equations of Motion for a pendulumn with mass `m` at the end of a massless rigid rod of length `l`, starting at initial angle wrt the downward direction of `theta`*

* **Pizza Shop** A mom and pop pizza shop has been getting complaints about their deliveries taking too long. They do everything via paper slips and vocal communication. 
    * *As a data scientist asked to help out, describe what you would do to find where and if their delivery problem lies?* (~1week assignment)
    * Now they want to spend some money on modernizing their service and system. *Whiteboard the architecture for the system you would build them* (mobile/desktop, data model/normalization ideas, UI, hardware in the shop, be realistic and prudent with what you'd specify)

* **Scrabble** *How would you build a scrabble app?* (systems design)

* **Talent** *Design a tool to collect and report votes for an episode of ____ got talent. How does this scale to hundreds of millions of users?* (systems design)

* **Messy Data** Drawn example of messy, noisy time-series data with many missing pieces, and a large step indicating a state change. *Discuss how you would handle analyzing data like this and deal with missing data points?* The state change means that data before/after the change should be treated and analyzed differently. *How would you detect the state change in this dataset? How would this effect the pipeline used to analyze these datasets?*
  
* **Spring and Wall** A spring with spring constant `k` has a mass `m` on it. It is released some distance `d`from equilibrium. A perfectly elastic wall is placed some distance `d2` where `d2`< `d` opposite the equilibrium point. *What is the change in the period of this system with the wall versus without the wall in place* (Shoudl draw a picture)

* **Posfix Processor (python)** *Write a function to interpret a posfix operation (posed as a string) and provide the answer back to the user*. Additionally, assume that there might be special operators that define a variable number of arguments, the details of which are known to you as you write your interpreter.

    ```python
    def eval_posfix(posfix):
        pass
    
    ## Accommodate special functions
    def middle3(a,b,c):
        return b
    
    assert eval_posfix("3 4 +")==7, "Should be '3+4' == 7"
    assert eval_posfix("5 5 2 * -")== -5, "Should be '5-(5*2)' == -5"
    assert eval_posfix("-1 3 + 10 9 10 11 middle3 * -")==102, "Should be '(-1+3) - 10*middle3(9,10,11)'".
    ```
    
* **Smart Memoize (python)** You have a data pipeline that you find to be too slow, specifically it is the evaluation of one function millions of times that is the bottleneck. The function has been pretty heavily optimized, so take it as is.
    * *Discuss some things you would do in order to speed up the pipeline in this scenario*
    * Caching is a good idea. *Make a decorator that will **memoize** (cache) previous evaluations of this function. Discuss limitations and problems here* 
    * Now you find that memory consumption is an issue. *Reimplement a smarter momoizer that doesn't just eat memory forever* (LIFO buffer is what I did)
    * *Modify to make sure that you're still caching and keeping most recent calls without recalculating* (Reordering the buffer)
    
* **Files Summarizer** *Print file contents for all files of a given name under a given `directory`.* Note that this is a large system, where other processes may be reading from/writing to files at any time. Additionally, files and folders may be deleted at any time too. Use of basic modules is okay
    
    ```python
    '''directory
    |\
    | A
    | |\
    | | B
    | | |
    | | foo.rtf
    | | test.py
    | |
    | foo.txt
    | bar.txt
    foo.txt
    something.md
    ...
    '''
    
    def summarize(filename, directory):
        pass
    ```
     
* **Tower Breakers Final Battle** https://www.hackerrank.com/challenges/tower-breakers-the-final-battle-1 Dope. 

* **Math Quiz** Administer a math test such that the user inputs a base number, an arithmatic sign, and the maximum number of separate problems to pose to the test taker. You should continue re-testing the kids if they do not get a problem right twice in a row (not sequentially). 

    ```python
    def submit_question(question_to_ask:->str) -> int:
        # assume provided functionality
        return student_guess
        
    def administer(basenum:->int, sign:->str, maxquestions:->int):
        # fill me in, adminsiter `maxquestions` to the user asking 
        # math questions involving `sign` and `basenum`. Make sure to
        # keep asking as long as the user hasn't gotten two answers
        # in a row right
    ```


# Paired/Online Programming
* **Array Merge** Given two *sorted* arrays `A` and `B`, each has `N` elements in it. `A` is of size `2*N`, with the second half filled with `None` values. *Write a function to merge `B` into `A` in place, keeping results sorted*. You may **not** use other data structures (lists, sets, dicts) for temporary storage, but can use temporary variables if you wish.
    
    ```python
    A = [1,2,5,9,None,None,None,None]
    B = [2,3,4,10]
    
    def merge_arrays(A,B):
        ## complete Me
        return
    
    assert A == [1,2,2,3,4,5,9,10]
    
    # Hint: Merge from the back to the front to do this in place, without allocating additional memory
    ```
    
* **Is Subset?** Given two integer arrays A and B of any size. *Write code for a function FindExactMatch() to determine if B is contained (exact pattern match) in A*.  An exact pattern match is all the same value in the same sequence without any other values in between; literally a one for one match) Return the array index where the match is found or -1 if not found. 
    
    ```
    # Example1    A: 0,1,2,4,1,2,3    B: 4,1     Returns  3  (index of where match begins, assuming zero based indices) 
    # Example2    A: 0,1,2,4,3,1,3    B: 4,1     Returns -1  (no match found) 
    
    def FindExactMatch(A,B):
        pass # fill me in
    ```
    * *What if we wanted the match to be able to circle back from the end to the beginning of the array?*

* **Build Order** *Write a program that takes as inputs a list of build dependencies: (`[(child,parent),...]`), and outputs a valid build order such that all parents of a child are built before the child program*. Omit circular dependencies. Each child has one parent, and many children can share a parent. **Ive seen this asked more than any other problem!**
    * *How do you deal with circular dependancies?*

    ```python
    """"""
     Build order is downwards
     A depends on B and C, B depends on E, etc
        A       X       Foo
       /|       |\
      B C       Y Z
      | |
      | D
      \ |\
        E G
    """
    ## Build only once
    dependencies = [("A","C"),("A","B"),("B","E"),("C","D"),("D","E"),("D","G"),("X","Y"),("X","Z"),("Foo",None)]
    
    def build(dependencies):
        pass
    
    # Valid: ['E', 'G', 'D', 'C', 'B', 'A', 'Y', 'Z', 'X', 'Foo'] (not topological sort)
    
    # Hint: build helper classes if you want. Can implement topological sort or just make sure that whatever is built has no unbuilt parents. 
    ``` 

* **Longest chain** Find the longest substring in a string with only 2 varying characters
    
    ```
    # Example:   aaabbbbcccdddddd ==> cccddddd
    def longest_chain(string):
        pass
    ```
* **Permutation Indices** (Adapted from FB interview, my buddy saw this IRL. Neat problem) Background, you have an `N-Dimensional` matrix. Given a list of matrix dimensions, *write a function to return labels for every possible cell within the matrix* like `x_m_n_o_p`:

    ```python
    assert nd_lables([3]) == ["x_0", "x_1", "x_2"]
    assert nd_lables([2,2,2]) == ['x_0_0_0', 'x_0_0_1', 'x_0_1_0','x_0_1_1', 'x_1_0_0', 'x_1_0_1', 'x_1_1_0', 'x_1_1_1']
    def nd_labels(dims):
        pass
    
    
    ## This was too fun not to include. 
    def nd_labels(dims:list)->list:
    labels = ["x"]
    ## Add each dimension's range to the labels list
    for dim in dims:
        ## Update each existing (growing) label with this dimension's index range
        for ix in range(len(labels)):
            ## Choose the first one to modify
            base = labels.pop(0)
            ## Modify label by adding each new dimension's range to it
            for dim_ix in range(dim):
                labels.append(f"{base}_{dim_ix}")
    return labels
    ```

* **Word Verifier** Given a dictionary of valid words, and a mapping of numbers to a list of characters, identify which possible combination in a string of said numbers yields valid words. What is the runtime complexity?

```python 
"""mapping:
0 : []
1 : ['a','b','c']
2 : ['d','e','f','g']...
"""
# "121" -> "ada","aea","afa" ... which ones are valid words?
def validWord(numberstr):
    pass
```
* **Build Order** *Write a program that takes as inputs a list of build dependencies: (`[(child,parent),...]`), and outputs a valid build order such that all parents of a child are built before the child program*. Omit circular dependencies. Each child has one parent, and many children can share a parent. **THIS ONE COMES UP A LOT** Learn TopoSort or just figure out a smart way to do it with basic graph construct (dictionary of lists mapping connections). 
* **Linked List Cycle** *Return the starting node of a cycle within a linked list*
    * Can you do this in constant space?
        * Hint: Slow and Fast pointer. Find where they meet. Then find the size (k) of the cycle (hold one still and count movements of the other). Then start two pointers from beginning of LL, one at the start, the one at (k). March until they meet. 

    ```
                 ______
                 |     |
                 \/    |
        1 -> 2 -> 3 -> 4

    Return the node corresponding to node 3. 
    ```
* **Duplicate Linked List Removal** Given a sorted singly linked list, remove all duplicate elements
    
    ```python
    """
    Given 1->1->2, return 1->2.
    Given 1->1->2->3->3, return 1->2->3
    """
    #(trivial)
    def deleteDuplicates(A):
        head = A
        while A:
            while A.next and A.val == A.next.val:
                A.next = A.next.next
            A = A.next
        return head
    ```
* **Dict Compare** *Write a function that takes two dictionaries and returns `True` if the dictionaries are equivalent and `False` if they are not* (up to you to define what *equal* diuctionaries mean...)
    
    ```python
    def compare_dicts(dict1, dict2):
        ## Complete me
    ```
* **Tree Comparison** You're given two trees, each with just a few nodes. (pic?). Build the trees and:
    * *Write me a function that will tell me if two trees are identical, reading each from left to right* (AKA preorder traversal). 
    * *Now, tell me how what you implemented would work if you had a trillion nodes in each tree?* Maybe you're smart and don't need to do the third one
    * *Reimplement your function such that it is effective for massive tree comparisons*
    
* **Random from random**: You're given a function `rand5()` that, when called, yields a random number 0-4. Each number has a 1/5 chance of being produced.  *Write a function `rand7` that yields a random number in the range 0-6 with equal chance of each number being produced which **only** calls `rand5`*

    ```python
    rand5() # ==> Yields one of {0,1,2,3,4} with 1/5 chance of each
    
    def rand7(): # ==> Yields one of {0,1,2,3,4,5,6} with 1/7 chance of each
        ## Complete Me
    ```
* **Analysis**: (Give you a spreadsheet of X,Y,Z coordinates in separate columns). 
    *   *Tell me things about this data* (bring me a rock in the interview: Red flag for me)  
    *   *Calculate the ______ (Radius of circle that encompasses center 50% of X and Y coordinates)* 

# Take Home Exercises
* **Massage Parlor - 2 hour hard limit** This was a doozie. 
    
>   ==Your Mission==
>    Your task is to simulate a day-in-the-life of a massage parlour in operation.
>
>    ==Rules==
>    The Massage Parlor is open for 10 hours, from 8am to 6pm. You don't want your program to take that long to run, so you'll need to somehow simulate real time.
>
>    When the parlour opens, there are 4 maseusses who start their shift:
>    Andrew, Brad, Camile, and Demetri.
>
>    On average, a new customer enters once every ten minutes. Their arrivals are random. Customers are named successively starting at Customer-1. The parlour can only hold 12 total customers; if a customer arrives when the parlour is full, they leave impatiently.
>
>    Otherwise, the client waits for a Maseusse. A Maseusse can only massage one person's back at a time, and takes between 20 and 40 minutes to do so. After a Maseusse is done with a customer, the customer leaves satisfied.
>
>    A customer will wait up to 30 minutes for a free Maseusse; if time's up and none can be found, the customer leaves unfulfilled.
>
>    maseusses work 5 hour shifts, so the first shift of maseusses is allowed to go home at 1pm. They end their shift as soon as they can, unless they busy with a client. In that case, they wait until they finish that client, and then end their shift.
>
>    At 1pm, the second shift of maseusses starts: Erin, Fran, Greg, and Hercules. They also work a 5 hour shift, and can go home after 6pm. Like the morning shift, if they're busy with a customer, they need to finish up before leaving.
>
>    A customer who enters after 6pm is turned away, and leaves cursing himself.
>
>    When all the maseusses and customers have gone home, the parlour closes. If there are any customers left waiting for a Maseusse, they are kicked out, and leave furious.
>
>    ==Output==
>    Your program should print the below events in chronological order.  [Time] is maseusse parlour-time in the format HH:MM, not real time.
>
>    [Time] Maseusse Parlor [opened/closed]
>    [Time] [Maseusse] [started/ended] shift
>    [Time] [Customer] entered
>    [Time] [Customer] left [impatiently/satisfied/unfulfilled/cursing himself/furious]
>    [Time] [Maseusse] [started/ended] massaging [Customer]'s back
>
>    ==Guidelines==
>    Use your choice of language. Use only standard libraries. Use whatever resources you'd like, apart from asking about the question itself online.


## Nearby Neighbors 
*(git@github.com:ZachDischner/SectorSearch.git)*

* Given a square space, 128km x 128km, and N=10,000 birds occupying the space, * *compute how many birds in this 2d space are too close to each other*. 
    - Birds positions will be provided as an Nx2 array of [x,y] coordinates (in meters).
    - Birds must maintain a horizontal separation of radius 0.5km from other birds. 
    - If a bird is within 0.5km of another bird, both are "in conflict".
    - Have count_conflicts return the total number of birds that are in a conflicted state. Not the total number of conflicts).
    - **NOTE** the O(N<sup>2</sup>) solution takes just a few lines of code and 10 minutes time to code up. **Do better**
    - ZD: They didn't like my solution (I did though). Try to do this algorithmically vs programmatically. I'm thinking a not-too-fancy sorting algorithm with X/Y/angle to group locations in nearby space by nature of order of array.
        
    ```python
    NUM_DRONES = 10000
    AIRSPACE_SIZE = 128000  # Meters.
    CONFLICT_RADIUS = 500  # Meters.

    def count_conflicts()
        ## Complete me
        
    def gen_coord():
        return int(random.random() * AIRSPACE_SIZE)

    positions = [[gen_coord(), gen_coord()] for i in range(NUM_DRONES)]
    conflicts = count_conflicts(positions, CONFLICT_RADIUS)
    print("Drones in conflict: {}".format(conflicts))
    ```

* **Gram Schmidt** *Write a recursive implementation of the Gram Schmidt algorithm for finding an orthonormal basis for a vector space* https://en.wikipedia.org/wiki/Gram%E2%80%93Schmidt_process
    
    ```python
    def gramSchmidt(vectors):
    ## Complete me
        return basis
    ```
* **FizzBuzz** (git@github.com:ZachDischner/FizzBuzz.git) Modification of the classic here. *Write a program that generates `N` fibonacci numbers, and encodes the output as per the following rules:*
    - "Buzz" when F(n) is divisible by 3.
    - "Fizz" when F(n) is divisible by 5.
    - "FizzBuzz" when F(n) is divisible by 15.
    - "BuzzFizz" when F(n) is prime.
    - the value F(n) otherwise. 

## Python Concepts
* **Function Wrapping Decorator** *Implement a decorator `compose(\*funcs)` which accepts an arbitrary number of functions as arguments. Each of those functions takes a single argument, and returns a single value. The compose() decorator should evaluate them in left-to-right order, with the decorated function being the left-most function that is evaluated. For example, composing 3 functions will look like*:

    ```python
    #     @compose(func1, func2, func3)
    #     def func0(param):
    #         return val
    
    #     func0(arg)  #=> func3(func2(func1(func0(arg))))
    def compose(__):
        ## complete me
    ```
    
* **Words Generator from File**
*Implement `words()` such that it accepts a path to a file containing a sequence of ASCII characters of total length <= 1TB, and returns an iterable over each subsequence of contiguous English letters within that file:
    
    ```python
    #     for word in words(file_path):
    #         # word is a subsequence of contiguous English letters
    
    def words(file_path):
        ## Complete me
    ```
    
* **Capitalize Decorator**
*Implement `capitalized()` such that:*

    ```python
    #     @capitalized
    #     def string_returning_function():
    #         return "foo"
    
    def capitalized(func):
        ## Complete me
    ```
    
* **General**
*Implement the 3 functions belows so the code executes and produces the expected output*
    
    ```python.
    # Do not include any other imports.
    # Do not use any Python built-in functions like.
    # Is guarenteed to execute to completion.
    
    import time
    import random
    
    ## YOUR CODE ONLY BELOW HERE
    # 1. Implement this function
    def enum(iterator):
        pass
    
    # 2. Implement this function (a generator)
    def stream_objects():
        pass
    
    # 3. Implement this function
    def timetaken(func):
        pass
    ## YOUR CODE ONLY ABOVE HERE
    
    
    ## DO NOT MODIFY ANYTHING BELOW HERE
    class Object():
        def __init__(self):
            self.complete = random.random() < 0.2
    
        def is_complete(self):
            return self.complete
    
    @timetaken
    def run():
        for index, current in enum(stream_objects()):
            if current.is_complete():
                return index
    
    print 'Expected output:'
    print "Run function took # seconds."
    print 'Final object was at index #.'
    
    print 'Actual output:'
    final_index = run()
    print 'Final object was at index {}'.format(final_index)
    ```
## **Coffee Shop Scheduler** 
**(github.com:ZachDischner/BaristaScheduler.git)**

> The challenge here is to write a program that determines in what order to make a series of coffeeshop drinks. The drinks are ordered at various times during the day and take various amounts of time to make. The data formats, input data, and expected output data are detailed below, and we expect your program to match the provided output.
> 
> ### Description
> Welcome to _Fin's Cafe Shoppe_. The baristas are trying to figure out the best way to serve drinks to customers, and they need your help!
> There are exactly 2 baristas, with ID numbers `[1, 2]`. A barista can make at most 1 drink at a time. For example, if a barista starts making a `3-minute tea` at `time=5`, she will deliver the drink at `time=8` and can start making a new drink at `time=8`.
> 
> The work day starts at `time=0` and ends at `time=100`.
> 
> There are three types of drinks, each of which takes a different amount of time to make and yields a different profit.
>
```
[
	{ "type": "tea",      "brew_time": 3, "profit": 2 },
	{ "type": "latte",    "brew_time": 4, "profit": 3 },
	{ "type": "affogato", "brew_time": 7, "profit": 5 }
]
```
>
### Example Input / Output of your Program
> 
> Below is **example input data** of orders made in a given day, ordered by `order_time`. See file `input.json` for a full list.
>
```
[
	{ "order_id": 1, "order_time": 0, "type": "affogato" },
	{ "order_id": 2, "order_time": 1, "type": "tea" },
	{ "order_id": 3, "order_time": 2, "type": "latte" },
	{ "order_id": 4, "order_time": 2, "type": "tea" }
]
```
>
> Below is **example output data**. See file `output_fifo.json` for the expected output given `input.json`. The output of your solutions should include drinks that each barista makes and the time that the barista starts making the drink. It must be valid json - an array of objects with the following format:
> 
```
[
	{ "order_id": 1, "start_time": 0, "barista_id": 1 },
	{ "order_id": 2, "start_time": 1, "barista_id": 2 },
	{ "order_id": 3, "start_time": 4, "barista_id": 2 },
	{ "order_id": 4, "start_time": 7, "barista_id": 1 }
]
```

* **IP Parser** (github.com:ZachDischner/BaristaScheduler.git)
> **Requirements:**
> Create a program that will read a given set of IPs, perform Geo IP and RDAP lookups, and accept a query to filter results.

> **Objectives:**
>   This exercise is designed to test your ability to:
    Take abstract requirements and run with them
    Write isolated decoupled modules with strict input/output interfaces
    Create a query language and algorithm for filtering
    Reading, parsing, and extracting IP addresses from unstructured text in an efficient manner
    Once you are done, please post your code on Github named something like: https://github.com/*profileID*/python_challenge
> 
> **Technical:**
>    Each component (GeoIP/RDAP/Filter/Parsing) should be as decoupled from the others as possible while still being easy to use.
    The main function should parse a text file containing 5000 IP addresses spread throughout random text.
    The filter component should provide a custom query language allowing the user to easily filter results based on
    Do not use 3rd party packages that provide complete solutions for GeoIP queries, RDAP queries, or filtering. Libraries simplifying HTTP requests, data manipulation, etc. are acceptable.
    Bonus points for simple, clever, and performant solutions, and any extras like unit tests, docs, multiple output formats, result caching, web UI, cli, etc. Be creative.
>    
> **File structure**
> 
> 5000 IP addresses interspersed in a text file like:
> 
> ```
> Lorem ipsum dolor sit amet, 244.36.171.60 adipiscing elit. Pellentesque finibus massa vitae augue 81.44.150.240, vitae faucibus quam pellentesque. Aenean condimentum risus at justo suscipit bibendum. Curabitur consequat tempus bibendum. Vestibulum bibendum sagittis odio, in fermentum velit auctor eget. Etiam mollis aliquet semper. Sed id turpis ac nulla congue rhoncus. 40.82.106.5 facilisis sem augue, sit amet consequat lacus pellentesque sed. Fusce non posuere ligula. Praesent nec lorem nisl. Integer suscipit efficitur nibh consectetur malesuada.
> 
Aliquam porta ullamcorper lorem, non 216.235.211.155 erat scelerisque eget. 116.101.14.224 finibus eu leo vitae 34.142.6.33. Fusce eu arcu eu metus dignissim hendrerit a in eros. Aenean elementum, mi id interdum hendrerit, odio erat dapibus nisl, sit amet feugiat purus massa ut eros. Duis lacus velit, facilisis ut dignissim vel, tempus id turpis. Vivamus laoreet sollicitudin metus vitae consequat. Praesent sapien massa, fringilla tempus finibus et, dapibus sit amet risus. Fusce in rhoncus tellus.
> 
Praesent in tincidunt 33.33.53.155. In in vehicula est, nec finibus urna. Nulla 186.167.42.67 arcu, bibendum quis erat in, viverra sodales erat. Vestibulum non scelerisque nibh, a viverra quam. Proin vitae odio ac leo dignissim mollis auctor ac libero. Cras sollicitudin lobortis risus eget aliquet. Morbi mattis id felis sed molestie. Praesent semper tellus a est ornare vulputate. Suspendisse rhoncus neque purus, non ornare sem pellentesque maximus.
> 
236.220.190.72
208.128.240.230
123.42.170.221
> 
224.171.234.30
3.173.155.119
40.43.195.14
232.125.33.216
> 
31.57.136.230
222.5.172.196
33.238.19.104
142.254.194.243
124.86.226.223
> 
Etiam quis 13.211.237.22 eros. Donec massa nunc, 4.44.97.176 vel ligula ut, dapibus 203.35.56.248 eros. Pellentesque malesuada nisi 24.197.112.182, a malesuada mi feugiat vitae. Nulla vitae ante at odio imperdiet varius 107.73.246.73 in justo. Sed nisi leo, venenatis vitae lorem et, porta eleifend arcu. Fusce ornare tempor lacinia. Vestibulum at diam eu libero lobortis pulvinar a non ex. 108.65.14.158 a neque ullamcorper, lacinia odio in, mattis est. Integer rhoncus neque sit amet lorem pulvinar, at pretium libero venenatis. Aenean tristique semper hendrerit. Praesent molestie mauris sed justo bibendum facilisis. Proin lorem magna, rutrum vel finibus eget, eleifend vel dui. 72.240.178.112 Donec fringilla nisi et erat iaculis rhoncus sed a nibh. Mauris semper 59.219.223.23 vel interdum vulputate. Mauris ut rhoncus nunc. Cras nec lectus eget lectus pretium tincidunt. Pellentesque magna ex, maximus sed imperdiet nec, molestie in sem. Ut efficitur 61.66.194.204 et porta mollis. Donec eu ex in purus tincidunt suscipit. 159.129.75.124 interdum velit velit, quis aliquam ante malesuada aliquet. Nunc ante enim, lobortis nec aliquet nec, vulputate vitae 227.73.226.94. Vivamus dapibus imperdiet augue, nec sagittis tellus lobortis vitae. Quisque ligula elit, 99.174.36.137 vitae justo vitae, porttitor malesuada 23.5.102.194.
> 
41.107.216.31
136.17.123.206
54.153.173.116
184.159.117.150
221.88.104.235
14.187.35.51
...
```

## PlutoVacationRentals API

> Taking the Test
> ---------------
> 
> You have five hours to implement your solution. The test will be administered through email. At the
beginning of the test, the test proctor will send you the problem description via email. Your
solutions will be submitted back to the proctor via email.
> 
> The test will involve implementing a database-backed service and the proctor will run your service
against a validation suite to ensure it meets all requirements.
> 
> Even though you should not use the proctor as a test engineer, you may provide early submissions. If your
submission fails some of the tests and if there is time remaining, the proctor will attempt to give you
feedback so that you can fix your program and resubmit.
> 
> It's highly recommended to make at least one submission very early in the test (once you have figured out
the basic structure of your application, how to install any needed dependencies and how to boot your
application) so the proctor can verify your submission starts up without errors at _____. Doing this early
on in the testing process will help get you quick feedback towards the end.
> 
> Getting Your Environment Ready
> ------------------------------
> 
You'll need a computer to work on and email access. You'll also need to set up Vagrant
(http://www.vagrantup.com/) and VirtualBox (https://www.virtualbox.org/), both of which are free. A
sample Vagrantfile is included here for you to test your setup.
> 
Please make sure you can bring up that machine with `vagrant up` well before the start of the test.
You'll see "Ready for launch!" once the basic setup works.
> 
To save time, we also suggest installing any tools (databases you're familiar with, your favorite
Python, Javascript or Go packages,...) ahead of time so you don't loose time during the test.
> 
Please be sure to update the `bootstrap.sh` script and to make it install any dependencies you have.
We will `vagrant up` your machine from a machine connected to the internet and expect a full functioning
service without manual intervention from the proctor's side.
>
> PROMPT
> ----------------------
> Your startup "PlutoVRBO" is competing to build a vacation rental system for the new Pluto colony. You heard your competitor "LyftPluto" is going to launch tomorrow!
Competition is fierce and getting your product out first is the only way you'll
succeed. You've already contracted out the front-end work so the only remaining piece
is the back-end API server. A fully functioning solution needs to be deployed today
for your company to survive!
> 
People who have traveled back to Earth will use this service to rent out their
Pluto real estate to fellow Pluto colonizers.
> You can use Python, JavaScript or Go to implement the API server, talking to the backing data store of your choice. You may use any libraries that aid in
handling generic HTTP requests, but may not use any libraries that add further
"API" features.
>
Examples allowed here are: Node.js Express, Python Flask.
Examples forbidden here are: Node.js LoopBack, Python Flask-RESTful.
>
Configure the Vagrant box to install all the dependencies and start your
service by modifying the supplied `bootstrap.sh` script. Internally your API server
should listen on port 9090, which we forward out of the Vagrant box.
>
When we get your submission, we will run `vagrant up` and then point our test harness to
http://localhost:9090/ to validate your solution.
>
The data store must be local to the vagrant box (no remote / Internet data storage).
>
Good luck!
>
API Specification
=================
>
There are a few endpoints you need to support. All of these produce and consume
JSON. JSON is expected out of every response from the API. We expect about 100k
listings in the system so we'll load test to a little beyond that.
>
Listings Endpoint
-----------------
>
The `/api/listings` endpoint is for querying, creating, and deleting listings.
>
**GET** - Get Listings
>
> Queries all of the listings in the system. A few query arguments are supported:
> 
 * `?active=1` returns only listings that have not expired
 * `?length=<length>&page=<page>` return paginated listings, starting at
   `<page>`; use page size of `<length>` listings
>
If no arguments are supplied then this should return all the listings. Listings
should always be returned in id order.
>
```
[
    {
        "id" : <id>,
        "user" : "<listing owner, username>",
        "title" : "<title, up to 140 characters>",
        "description" : "<description, up to 1024 characters>",
        "expiration" : "<expiration date as yyyy-MM-ddThh:mm:ss>",
        "location" :
        {
            "x" : <x coordinate, floating point, meters>,
            "y" : <y coordinate, floating point, meters>
        }
    },
    ...
]
```
>
**POST** - Create New Listing
>
Adds a new listing to the system. The POST will contain a listing with the
following format:
>
```
{
    "user" : "<listing owner, username>",
    "title" : "<title, up to 140 characters>",
    "description" : "<description, up to 1024 characters>",
    "expiration" : "<expiration date as yyyy-MM-ddThh:mm:ss>",
    "location" :
    {
        "x" : <x coordinate, floating point, meters>,
        "y" : <y coordinate, floating point, meters>
    }
}
```
>
Upon success, the newly-created id should be returned (it's also OK to return
the whole listing with the id field as part of it):
>
```
{
    "id" : <id>
}
```
>
**DELETE** - Delete All Listings
> 
This will be used to flush the database for testing.
>
Single Listing Endpoint
-----------------------
>
The `/api/listings/<id>` endpoint is for viewing and updating individual
listings. They produce and consume the same JSON listing format as the endpoint
above.
>
**GET** - Get Single Listing
>
**PUT** - Replace Single Listing
>
**DELETE** - Delete Single Listing
>
Extra Credit
============
>
If you have extra time, you may want to try one or more of these extra credit
features.
>
Location Search
---------------
>
The Pluto settlement will initially be pretty small so a simple Cartesian grid
can be used for addresses, assuming all real estate lies in a plane. Implement
a new query argument for the /api/listings endpoint,
`?x=<x>&y=<y>&radius=<radius>` that returns listings within a circle of
`<radius>` from location `(<x>, <y>)`.
> 
Comments Endpoint
-----------------
> 
The `/api/listings/<id>/comments` endpoint allows users to provide feedback
about listings.
> 
**POST** - Create New Comment
>
Adds a new comment to a listing. The POST will contain a comment with the
following format:
>
```
{
    "user" : "<commenter, username>",
    "comment" : "<comment, up to 140 characters>"
}
```
>
Upon success, the newly-created id should be returned (it's also OK to return
the whole comment with the id field as part of it):
>
```
{
    "id" : <id>
}
```
>
**GET** - Get Comments
>
Query for all of the comments for the given listing. Comments should always be
returned in id order.
>
```
[
    {
        "id", <id>,
        "user" : "<commenter, username>",
        "comment" : "<comment, up to 140 characters>"
    },
    ...
]
```

## WordCloud Generator
*(git@github.com:ZachDischner/WordCloud.git)*
>Your program word cloud program should be written in Java, C#, or C++ aned be able to take both a line of text and a path to a text file to generate a word cloud.  The parser in your inner libraries should try not to include words useless to word clouds (like articles [a, an, the], or minor words like "it", "us", "them"); this is just notional since this is a programming example just show the principle of the filtering. As an output your program, and therefore the inner libraries, need to support the ability to return the word cloud sorted by counts with a min/max threshold option and it needs to be able to return the word cloud alphabetically with the ability to choose the starting characters.  For example, one run may ask for all words that occur more than 10 times but less than 20, and another may ask for the top ten words.  Another run may ask for all words alphabetically that start with the phrase "sa".  Have a driver program as well as unit tests that stimulate the library and the code with reasonable test cases. 

