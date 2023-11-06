# **Lab Report 3** #
## Part 1 :
**Failure-Inducing Code:**
```
  @Test
  public void testReverseInPlace3() {
    int[] input1 = {7,8,9,10};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{10,9,8,7}, input1);
  }
```
*Symptom:* 

![Image](Image23.png)

**Code That's Not Inducing a Failure:**
```
  @Test
  public void testReverseInPlace() {
    int[] input1 = { 8 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 8 }, input1);
  }
```

*Symptom:*

![Image](Image24.png)


Before the Code Fix:

```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

After Debugging: 

```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[i]; //set the temporary value to i value's original number
      arr[i] = arr[arr.length - i - 1]; //that i value is moved backwards
      arr[arr.length - i - 1] = temp; //the replacing value's place is then swapped with the replacing value
    }
  }
```

*How did this work?*  

To properly create a for loop that would correctly reverse the contents inside our ArrayList, we would have first to create a for loop that would only go up to half of the total length. When we do reverse the values inside the ArrayList, we only need to reverse half of them as it effectively is just swapping opposing values so that it becomes reversed. The original code would essentially replace the values incorrectly. The fix provides a temporary variable that holds onto the original value while the index value gets replaced, so the replacing value is then swapped in for the temporary value. Consequently, this eventually outputs a reversed ArrayList of values.   

-----
## Part 2 :  **The command `grep`**

**1. Case-Insensitive Search `-i`**

```
$ grep -i "cohort" technical/biomed/1468-6708-3-1.txt
        years of being healthy, in a cohort of older adults for
          visit. Two cohorts were followed, one with 7 years of
          persons in the second African American cohort, who have
          and for 70 persons in the first cohort who did not have
          were unbiased for the African American cohort. In the
```

The `i` command in this case is searching for the inputted string no matter its case, which makes it case-insensitive. Even if the word "cohort" was capitalized or had a contraction, it is still outputted. 

  
```
(Simplified)
$ grep -ri "Propagation" ./technical/
./technical/biomed/1471-2091-2-13.txt:        for the location, propagation and distribution of inteins
./technical/biomed/1471-2105-3-14.txt:        propagation caused by transfer of information from
./technical/biomed/1471-2105-4-13.txt:        On the other hand, backpropagation neural networks are a
./technical/biomed/1471-2105-4-13.txt:        A second major advantage of backpropagation networks
./technical/biomed/1471-2105-4-13.txt:          propagation neural networks could do better using the
./technical/biomed/1471-2105-4-13.txt:        propagation networks trained with a learning coefficient of
./technical/biomed/1471-2105-4-28.txt:          Back propagation NN (BPNN)
...
```
The `-ri` command in this case is searching for the "propagation" string throughout the entire technical folder directory, no matter the case. 

The `-i` command is extremely useful for searching for any instances in which a word or string is used in a file without the worry of the characters not matching exactly how it is inside the text file. 

Source: https://linuxize.com/post/how-to-use-grep-command-to-search-files-in-linux/ 

---

**2. Invert Matching `-v`**

```
(Simplified)
$ grep -v "the" technical/biomed/1468-6708-3-1.txt

        Introduction
        Older adults are frequently counseled to lose weight,
        associated with increased mortality in those over age 65.
        Six large controlled population-based studies of
        between body mass index (BMI) and mortality, controlling
        for relevant covariates [ 1 2 3 4 5 6 ] . All studies found
        excess risk for persons with very low BMI, but that persons
        with moderately high BMI had little or no extra risk except
        in certain small subsets. A review of 13 studies of older
        adults drew similar conclusions [ 7 ].
        ...
```
The `-v` command prints any line that does not include the inputted string. As shown here, it is printing every line that does not include the "the" string as it extends to every line, an extensive list of lines of text that would take over half of the page if it was pasted. 

```
(Simplified)
$ grep -rv " " ./technical/
./technical/911report/chapter-1.txt:
./technical/911report/chapter-1.txt:
...
```
The `-rv` prints every line in the folder that does not include a space. This is recursively going through any file that has no space in the "technical" directory.  

`-v` is useful for searching text in files that specifically do not pertain to a certain keyword or topic. The command could reduce the time to search for a more specific topic by excluding lines of text that talk about it. 

Source: https://www.howtogeek.com/devops/how-to-use-negative-matching-with-grep-in-linux-print-lines-that-dont-match/

---

**3. After Context `-A`**

```
$ grep -A 2 "four men" technical/911report/chapter-1.txt
    The four men passed through the security checkpoint, owned by United Airlines and operated under contract by Argenbright Security. Like the checkpoints in Boston, it lacked closed-circuit television surveillance so there is no documentary evidence to indicate when the hijackers passed through the checkpoint, what alarms may have been triggered, or what security procedures were administered. The FAA interviewed the screeners later; none recalled anything unusual or suspicious.

    The four men boarded the plane between 7:39 and 7:48. All four had seats in the first-class cabin; their plane had no business-class section. Jarrah was in seat 1B, closest to the cockpit; Nami was in 3C, Ghamdi in 3D, and Haznawi in 6B.

    The 19 men were aboard four transcontinental flights.
```
The `-A` searches for the inputted string along with the desired amount of lines of context afterward. In this case, each case that the string "four men" appeared along with two lines for context. 
```
$ grep -A 2 "U.S. airspace" technical/911report/chapter-1.txt
    On 9/11, the defense of U.S. airspace depended on close interaction between two federal agencies: the FAA and the North American Aerospace Defense Command (NORAD). The most recent hijacking that involved U.S. air traffic controllers, FAA management, and military coordination had occurred in 1993.90 In order to understand how the two agencies interacted eight years later, we will review their missions, command and control structures, and working relationship on the morning of 9/11.

    FAA Mission and Structure. As of September 11, 2001, the FAA was mandated by law to regulate the safety and security of civil aviation. From an air traffic controller's perspective, that meant maintaining a safe distance between airborne aircraft.
--
    The defense of U.S. airspace on 9/11 was not conducted in accord with preexisting training and protocols. It was improvised by civilians who had never handled a hijacked aircraft that attempted to disappear, and by a military unprepared for the transformation of commercial aircraft into weapons of mass destruction. As it turned out, the NEADS air defenders had nine minutes' notice on the first hijacked plane, no advance notice on the second, no advance notice on the third, and no advance notice on the fourth.

    We do not believe that the true picture of that morning reflects discredit on the operational personnel at NEADS or FAA facilities. NEADS commanders and officers actively sought out information, and made the best judgments they could on the basis of what they knew. Individual FAA controllers, facility managers, and Command Center managers thought outside the box in recommending a nationwide alert, in ground-stopping local traffic, and, ultimately, in deciding to land all aircraft and executing that unprecedented order flawlessly.
```
The `-A` command searches for each instance of "U.S. airspace" in the file while also providing each instance with two lines of context afterward. 

The `-A` command is useful in terms that it is able to look for any specific keywords that the user wants while also providing some context of what they are looking up. It allows the user to search for any specific topic with the added context so that it makes more sense as usable information. 

Source: https://www.hashbangcode.com/article/grep-context#:~:text=Grep%20has%20a%20couple%20of%20built%20in%20flags,group%20separator%20%28--%29%20between%20contiguous%20groups%20of%20matches. 

---
**4. Names of Matching Files `-l`**

```
(Simplified)
$ grep -l "cohort" ./technical/biomed/*
./technical/biomed/1468-6708-3-1.txt
./technical/biomed/1468-6708-3-3.txt
./technical/biomed/1468-6708-3-7.txt
./technical/biomed/1471-2121-2-21.txt
./technical/biomed/1471-213X-3-7.txt
./technical/biomed/1471-2156-2-12.txt
./technical/biomed/1471-2156-2-17.txt
./technical/biomed/1471-2172-3-10.txt
./technical/biomed/1471-2199-2-2.txt
./technical/biomed/1471-2261-3-5.txt
./technical/biomed/1471-2288-1-9.txt
./technical/biomed/1471-2288-2-10.txt
...
```
The `-l` command searches for anything that contains the inputted string in a directory. In this case, it is looking for any file with the "cohort" string and printing the name of it. 

```
$ grep -l  "Cardiovascular" ./technical/biomed/*
./technical/biomed/1468-6708-3-1.txt
./technical/biomed/1471-2164-3-32.txt
./technical/biomed/1471-2350-2-11.txt
./technical/biomed/1471-2350-4-4.txt
./technical/biomed/1471-2474-2-3.txt
./technical/biomed/1472-6793-2-1.txt
./technical/biomed/1472-6947-2-7.txt
./technical/biomed/cc303.txt
```
The `-l` command searches for anything that contains the "Cardiovascular" string in the biomed directory. 

The `-l` command is useful as it is able to search for files with information that is useful or that pertains to the user's desired search topic. It cuts down on all the files that are not useful or related to what the user wants. 

Source: https://phoenixnap.com/kb/grep-command-linux-unix-examples 
