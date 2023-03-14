## CSE 15L Lab Report 5: Putting it All Together
---

## Lab 6

For this lab I decided to go back to Lab 6, primarily because I couldn't go to lab and properly do the task on my lonesome.
I went ahead and did the lab step-by-step because the implementation also shows up for the later skill demo.

## TestListExamples & ListExamples Implementation

First thing first, I took a look at the starter code available in [list-examples-grader repo]([https://man7.org/linux/man-pages/man1/grep.1.html](https://github.com/ucsd-cse15l-w23/list-examples-grader)) , and since one of the weekly quizzes on gradescope also needed this starter code, I had a head start on fixing the bugs in the repo.

The first task I set out to do was remove the `IsMoon` class in TestListExamples since that was irrelevant to the task, and then create some tests for what we're looking for. From the [Week 6 Lab Taks](https://ucsd-cse15l-w23.github.io/week/week6/#lab-tasks), we needed to find:

- A repository with a file called ListExamples.java
- In that file, a class called ListExamples
- In that class, two methods:

  -  `static List<String> filter(List<String> s, StringChecker sc)`
  -  `static List<String> merge(List<String> list1, List<String> list2)`

The initial `TestListExamples.java` already has implementation for `merge`, so now I needed to find a way to test for `filter`.  
To do this end, I looked at the description of `filter` which states:  
```
  // Returns a new list that has all the elements of the input list for which  
  // the StringChecker returns true, and not the elements that return false, in      
  // the same order they appeared in the input list;  
```

So following this statement, that means when "filtering" a list, the new list is simply the elements that are specified to be filtered, ignoring case.  
Now, taking a look at `TestListExamples`, there's already a `IsMoon` class that utilizes a `checkstring` method, so I'll go ahead and use that since I'm too  lazy to do my own tests right now, but maybe later.  
Now, for the `filter` test, using the `testMergeRightEnd` test as a basis, I made the following test `filterMoon` for the expected behavior of ListExamples.
I created a string List `testList` as the base, and  created another List `expected` for what the output array should be after being filtered. Afterwards I made a new List `filtered` using the `filter` method and cmparing the `filtered` list with what's expected as the test.
```
  @Test(timeout = 500)
  public void filterMoon(){
    List<String> testList = Arrays.asList("This", "moon", "should","moona","work");
    List<String> expected = Arrays.asList("moon");
    List<String> filtered = ListExamples.filter(testList, new IsMoon() );
    assertEquals(expected, filtered);
  }
```
Now that there's one test for all the expected methods in the `ListExamples` class, it's time to go back to `ListExamples` and create the `filter` and `merge` methods. Since the whole lab is mostly about grading students' submissions, I simply went ahead and copied the `ListExamples` class from [Corrected List Methods](https://github.com/ucsd-cse15l-f22/list-methods-corrected) to ensure that the tests I run are within expected behavior. I'll come back and do some more tests once I get the grading script working properly.

## grade.sh Implementation

Now that I got all the necessary parts finished, it's time to go back and get working on the workflow of the grading script, which is as follows:  

1. Clone the repository of the student submission to a well-known directory name (provided in starter code)
2. Check that the student code has the correct file submitted. If they didn’t, detect and give helpful feedback about it.
    - Useful tools here are if and -e/-f. You can use the exit command to quit a bash script early.
3. Somehow get the student code and your test .java file into the same directory
    - Useful tools here might be cp and maybe mkdir
4. Compile your tests and the student’s code from the appropriate directory with the appropriate classpath commands. If the compilation fails, detect and give helpful feedback about it.
   - Aside from the necessary javac, useful tools here are output redirection and error codes ($?) along with if
    - This might be a time where you need to turn off set -e. Why?
 5.Run the tests and report the grade based on the JUnit output.
   - Again output redirection will be useful, and also tools like grep could be helpful here

The first step was done for us already, I'll get started on the second step. Looking at the starter code for `grade.sh`, the cloned submission is made in a new directory `student-submission`, so an if statement for finding the java file should work, along with conditions for if its found and if it isnt found (with the found file outputting a message that its found, and an unfound file stating as such and giving a reccomendation). The implementation is as such:
```
if [[ -e student-submission/ListExamples.java ]]
then
    echo 'ListExamples.java found'
else
  echo 'ListExamples.java not found. Is the filetype named properly?'
  echo 'Score: 0/4'
  exit 1
fi
```
Now with step 2 done, step 3 says I have to get the student code and the test.java file into the same directory, so I use mkdir to make a new directory `grade-zone` where I'll copy the `ListExamples.java` file and the `TestListExamples.java` into it.
```
rm -r grade-zone
mkdir grade-zone

cp student-submission/ListExamples.java ./grade-zone
cp -r lib/ ./grade-zone
cp TestListExamples.java ./grade-zone
```

