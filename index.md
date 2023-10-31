# Lab Report 3
## Part I
## Failure-inducing input
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
## Input not failure-inducing
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
## Symptom

<img width="623" alt="image" src="https://github.com/joh048/cse15l-lab-report-3/assets/146862219/2e5c0d7e-d95e-4cb0-b52b-3457a7c300d1">

## Code with bug
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
## Fixed Code
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

## Part II
## -r option for grep: 
The -r option for grep stands for --recursive. Basically the option recursively reads all option under directories. 
```
$ grep -r "OLD TERRORISM" technical/
technical/911report/chapter-3.txt:            FROM THE OLD TERRORISM TO THE NEW: THE FIRST WORLD TRADE CENTER
```
In this example we are recursively looking under the technical directory and the directories under the technical directory to find any files that have the phrase "OLD TERRORISM".
```
$ grep -r "Resonance" technical/
technical/biomed/ar615.txt:        The delayed Gadolinium-Enhanced Magnetic Resonance
technical/plos/journal.pbio.0020150.txt:        Magnetic Resonance Imaging Research Center at Columbia University, fMRI represents a
```
In this example we are recursively looking under technical directory and the directories under the technical directory to find any files that have the phrase "Resonance".

## -l option for grep:
The -l option for grep stands for --files-with-matches. This option essentially prints only the name of each input file. Supresses the normal output.
```
$ grep -l "By next summer, more" technical/plos/*.txt
technical/plos/journal.pbio.0020053.txt
```
In this example we search for the phrase "By next summer, more" in technical/plos to find that this file path technical/plos/journal.pbio.0020053.txt contains the phrase.
```
$ grep -l "Daniel Hungerford" technical/government/Alcohol_Problems/*.txt
technical/government/Alcohol_Problems/DraftRecom-PDF.txt
technical/government/Alcohol_Problems/Session3-PDF.txt
technical/government/Alcohol_Problems/Session4-PDF.txt
```
In this example we search for the phrase "Daniel Hungerford" in technical/government/Alcohol_Problems to find that 3 of these file paths include the name.

## -c option for grep
The -c option for grep stands for --count. This option suppresses the normal output like -l but also outputs the number of matching lines for each file.
```
$ grep -c "injured" technical/911report/*.txt
technical/911report/chapter-1.txt:1
technical/911report/chapter-10.txt:1
technical/911report/chapter-11.txt:0
technical/911report/chapter-12.txt:0
technical/911report/chapter-13.1.txt:0
technical/911report/chapter-13.2.txt:0
technical/911report/chapter-13.3.txt:2
technical/911report/chapter-13.4.txt:1
technical/911report/chapter-13.5.txt:1
technical/911report/chapter-2.txt:1
technical/911report/chapter-3.txt:1
technical/911report/chapter-5.txt:0
technical/911report/chapter-6.txt:0
technical/911report/chapter-7.txt:0
technical/911report/chapter-8.txt:0
technical/911report/chapter-9.txt:21
technical/911report/preface.txt:0
```
In this example it shows that when searching for the keyword "injured" in technical/911report these files paths include the word along with their number of matching lines. technical/911report/chapter-2.txt has 1 matching line.
```
$ grep -c "alcohol" technical/government/Alcohol_Problems/*.txt
technical/government/Alcohol_Problems/DraftRecom-PDF.txt:53
technical/government/Alcohol_Problems/Session2-PDF.txt:97
technical/government/Alcohol_Problems/Session3-PDF.txt:168
technical/government/Alcohol_Problems/Session4-PDF.txt:164
```
In this example it shows that when searching for the keyword "alcohol" in technical/government/Alcohol_Problems these files paths include the word along with their number of matching 
 lines.technical/government/Alcohol_Problems/Session3-PDF.txt had 168 matching lines

## -n option for grep
The -n option for grep stands for --line-number. This option outputs the line number with the file path.
```
$ grep -n "Resonance" technical/plos/*.txt
technical/plos/journal.pbio.0020150.txt:42:        Magnetic Resonance Imaging Research Center at Columbia University, fMRI represents a
```
In this example we can see that line 42 of technical/plos/journal.pbio.0020150.txt contains the word "Resonance".
```
$ grep -n "underground" technical/911report/*.txt
technical/911report/chapter-1.txt:592:    It resumed at 9:37 as an air threat conference call,* which lasted more than eight hours. The President, Vice President, Secretary of Defense, Vice Chairman of the Joint Chiefs of Staff, and Deputy National Security Advisor Stephen Hadley all participated in this teleconference at various times, as did military personnel from the White House underground shelter and the President's military aide on Air Force One.
technical/911report/chapter-1.txt:624:    American 77 began turning south, away from the White House, at 9:34. It continued heading south for roughly a minute, before turning west and beginning to circle back. This news prompted the Secret Service to order the immediate evacuation of the Vice President just before 9:36. Agents propelled him out of his chair and told him he had to get to the bunker. The Vice President entered the underground tunnel leading to the shelter at 9:37.
technical/911report/chapter-3.txt:17:                parked a truck bomb with a timing device on Level B-2 of the underground garage,
technical/911report/chapter-9.txt:19:                acres of land. The buildings were connected by an underground mall (the concourse).
technical/911report/chapter-9.txt:1230:                post on the west side of West Street took shelter in the underground parking garage
technical/911report/chapter-9.txt:1655:                or perhaps directed through the underground concourse. Despite the initial advice
```
In this example we can see that all the line numbers that follow the file path are outputted since they contain the keyword "underground".

## Work Cited Source
![grep manual](https://linuxcommand.org/lc3_man_pages/grep1.html)
