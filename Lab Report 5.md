## CSE 15L Lab Report 5
---

## Lab 6

For this lab I decided to go back to Lab 6, primarily because I couldn't go to lab and properly do the task on my lonesome.
I went ahead and did the lab step-by-step because the implementation also shows up for the later skill demo.

## TestListExamples Implementation

First thing first, I took a look at the starter code available in [list-examples-grader repo]([https://man7.org/linux/man-pages/man1/grep.1.html](https://github.com/ucsd-cse15l-w23/list-examples-grader), and since one of the weekly quizzes on gradescope also needed this starter code, I had a head start on fixing the bugs in the repo.

The first task I set out to do was remove the `IsMoon` class in TestListExamples since that was irrelevant to the task, and then create some tests for what we're looking for. From the [Week 6 Lab Taks](https://ucsd-cse15l-w23.github.io/week/week6/#lab-tasks), we needed to find:

- A repository with a file called ListExamples.java
- In that file, a class called ListExamples
- In that class, two methods:

  -  `static List<String> filter(List<String> s, StringChecker sc)`
  -  `static List<String> merge(List<String> list1, List<String> list2)`

The initial `TestListExamples.java` already has implementation for `merge`, so now I needed to find a way to test for `filter`.  
To do this end, I looked at the description of `filter` which states:  

`  // Returns a new list that has all the elements of the input list for which  `  
`  // the StringChecker returns true, and not the elements that return false, in  `    
`  // the same order they appeared in the input list;  `  

So following this statement, that means when "filtering" a list, the new list is simply the elements that are specified to be filtered.  
Now, taking a look at `TestListExamples`, there's already a `IsMoon` class that utilizes a `checkstring` method, but there isn't a StringChecker interface, so I decided to slap that above the `IsMoon` class:

`  interface StringChecker {  `
`    boolean checkString(String s);  ` 
`}  `

