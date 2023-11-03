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

*How did this work?:*  

In order to properly create a for loop that would correctly reverse the contents inside our ArrayList, we would have to first create a for loop that would only go up to half of the total length. When we do 

-----
## Part 2 :  **The command `grep`**





