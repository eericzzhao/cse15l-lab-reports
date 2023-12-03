# **Lab Report 5** #
## Code Not Running?!?!? Tests Failing, not compiling either ## 

Student 1:
1 hour ago in General

I'm having issues running the test script. I don't know why I'm getting these test errors, but whatever change I make to the ListExamplesTest.java file isn't fixing anything. Mainly, it's not even detecting my JUnit tests which I'm pretty sure I have setup in the bash file to correctly call on it. To run my files I bashed a test script file to compile all of the Java files with the jar file. Then I ran the tests through it by inputting the command while in the correct directory structure:


![Image](Image32.png)

What am I missing? Right now, I'm stuck on how to fix these errors. Thank you.

---

TA (Staff):

Hi, rather than looking at just the ListExamplesTests.java file, as it is only testing whether your code works properly or not, maybe it is in one of your other Java files. There might be a bug in how you assign your variables that could be causing errors for your tests to fail. You also want to make sure that when you call the merge method, is it actually using the `add` function in the manner in which you want it to be? I would also double-check how your test script file is calling the JUnit tests. Additionally, in its current state, it won't produce the output you want (unless hint...you're on a Mac operating system).

---

Student 1:

![Image](Image37.png)

OK thank you so much! I just realized I made a mistake on how the add method works.  Assigning a 0 first made any values added onto the ArrayList print out the list backward, not what I intended for it to do.  I also made two simple mistakes of not assigning the correct variables in their while loops, which was why my expected tests often did not match with what was being outputted. Finally, I also realized that the Junit tests weren't being called correctly because they needed to be a semi-colon (I'm on a Windows machine) and that the JUnit tests weren't being formatted correctly for it to be detected by Java. 

---

Step Four: 

The File & Directory Structure Needed:
![Image](Image36.png)

Contents of each file before fixing the bug:
![Image](Image33.png)
![Image](Image34.png)
![Image](Image35.png)

Full Command Line You Ran to Trigger the Bug:

``bash test.sh`` 

A Description of What to Edit to Fix the Bug:

Firstly, you would have to edit the ListExamples.java file. Starting from line 15, we would remove the `0, ` portion from the add method to remove a hidden bug that would result in our filter function working as intended. 

![image](Image38.png)

Scrolling down, line 39 and and line 44 need their variables changed to `index1` and `index2` respectively, this would fix the bug to return the correct list. 

![image](Image39.png)


Finally, you would place the `.jar` files in quotations. This would allow Java to properly detect the files and the JUnit tests. I also changed any instance in which a `:` was used with a `;` instead as I am on a Windows machine. 

![Image](Image40.png) 

---

## Part 2 -- Reflection

I felt that for the second half of the quarter, something that I learned before that I had not learned before would be using Vim. Learning how to edit code from the terminal is very interesting and something that I definitely need for future classes. Another one would be the `jdb` debugger. Although we only had a short introduction to it, Professor Politz taught me how to diagnose problems that allowed for step-by-step intervention in determining where the bug occurred. Finally, I thought that this class served as a decent introduction to `Git` as I most likely have to use Github extremely often in the future, and learning the functions for it is useful. I want to thank Professor Politz and all the TAs who made this class possible, especially for whoever is reading this final sentence of my Lab Report. 
