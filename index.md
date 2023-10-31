```
import static org.junit.Assert.*;
import org.junit.*;
public class ArrayTests {
  @Test
  public void testReverseInPlace2() {
    int[] input1 = { 3, 4, 5, 6 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 6, 5, 4, 3 }, input1);
  }
 }
```
```
import static org.junit.Assert.*;
import org.junit.*;
public class ArrayTests {
  @Test
  public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
  }
}
```
<img width="623" alt="image" src="https://github.com/joh048/cse15l-lab-report-3/assets/146862219/2e5c0d7e-d95e-4cb0-b52b-3457a7c300d1">

```
public class ArrayExamples {
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
}
```

```
public class ArrayExamples {
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[i];
    }
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
  }
}
```
<img width="219" alt="image" src="https://github.com/joh048/cse15l-lab-report-3/assets/146862219/3ae4f01d-ede4-468c-9b5f-2d8d54404ba6">

The problem that caused the bug was that since we were only using 1 array and replacing the element near the end with the elements in the beginning, we were losing the element values near the end. 
This causes an issue because, in order for the array to be reversed, you would need to know all the elements and their order so you can reverse the order. A fix to this is to create another array. 
This new Array would hold the original elements and their position while you replace the other array with its reversed order. Now when traversing through the array and replacing each element, 
you still have the values and order stored in another array which makes it possible to reverse.
