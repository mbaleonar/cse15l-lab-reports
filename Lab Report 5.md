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
Now with step 2 done, step 3 says I have to get the student code and the test.java file into the same directory, so I use mkdir to make a new directory `grade-zone` where I'll copy the `ListExamples.java` file and the `TestListExamples.java` into it. Then I changed the current working directory to grade-zone for the next parts.
```
rm -r grade-zone
mkdir grade-zone

cp student-submission/ListExamples.java ./grade-zone
cp -r lib/ ./grade-zone
cp TestListExamples.java ./grade-zone
cd grade-zone
```
Onto step 4, now I have to compile the code and `TestListExamples`, and also compensate for failed compilations. Since I'm running on Windows machine I'll have to make a seperate classpath at least temporarily, dubbed `WINPATH` (slightly altered since I'm accessing the `/lib` directory from one directory back.) So for local testing purposes I'll be using `$WINPATH` instead of `$CPATH`
```
WINPATH='".;..\lib\junit-4.13.2.jar;..\lib\hamcrest-core-1.3.jar"' 
```
Now, to find the compilation failures from all the java files, I created this line of code:
```
javac -cp $CPATH *.java 2> errors.txt
```
After doing some research, 2> outputs the standard error, which should also clean up the terminal from a bunch of error messages, and so I created an if statement for an unsuccessful compilation:
```
if [ $? = "0" ]
then
  java -cp $WINPATH org.junit.runner.JUnitCore TestListExamples > testoutput.txt
else
  LINES=$(wc -l errors.txt)
  ERRORNUM=$(head -n $LINES errors.txt | tail -1)
  ERROR1st=$(head -n 1 errors.txt | tail -1)
  echo ""
  echo "Failure to compile; Total of "$ERRORNUM
  echo "Potential error: " $ERROR1st
  exit 1
fi
```
Since I created the `errors.txt` file, I replaced the `$CPATH` with `$WINPATH` to populate the `errors.txt` file and see what showed up and this was what showed up:
```
TestListExamples.java:1: error: package org.junit does not exist
import static org.junit.Assert.*;
                       ^
TestListExamples.java:2: error: package org.junit does not exist
import org.junit.*;
^
TestListExamples.java:15: error: cannot find symbol
  @Test(timeout = 500)
   ^
  symbol:   class Test
  location: class TestListExamples
TestListExamples.java:24: error: cannot find symbol
  @Test(timeout = 500)
   ^
  symbol:   class Test
  location: class TestListExamples
TestListExamples.java:21: error: cannot find symbol
    assertEquals(expected, merged);
    ^
  symbol:   method assertEquals(List<String>,List<String>)
  location: class TestListExamples
TestListExamples.java:29: error: cannot find symbol
    assertEquals(expected, filtered);
    ^
  symbol:   method assertEquals(List<String>,List<String>)
  location: class TestListExamples
6 errors
```
I noticed that the last line of the .txt file mentioned the number of errors, and the first line mentions the type of error it had, so I created a value `LINES` that is the number of lines in the .txt files, which is then used in my `ERRORNUM` value which is a string of the last line of the code that mentions the number of errors, and then `ERROR1st` takes the first line. Then I echoed an error message for the number of errors and the potential errors, then exiting the shell.

With the compiling error check done, I went ahead to the meat of the issue with compilation and subsequent grading process. First, I went ahead and ran the grade script with [Buggy Code](https://github.com/ucsd-cse15l-f22/list-methods-lab3) and [Corrected Methods](https://github.com/ucsd-cse15l-f22/list-methods-corrected).
