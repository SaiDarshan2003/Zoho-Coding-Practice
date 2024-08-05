# Zoho-Coding-Practice

## Challenge 1:

Find the longest palindrome sub-string in a string in Java.
```
public class LongestPalindromeSubstring {
    public static void main(String[] args) {
        String s = "babad";
        System.out.println("Longest Palindromic Substring: " + longestPalindrome(s));
    }

    public static String longestPalindrome(String s) {
        if (s == null || s.length() < 1) return "";
        
        int start = 0, end = 0;
        
        for (int i = 0; i < s.length(); i++) {
            int len1 = expandAroundCenter(s, i, i);    // Odd length palindromes
            int len2 = expandAroundCenter(s, i, i + 1); // Even length palindromes
            int len = Math.max(len1, len2);
            
            if (len > end - start) {
                start = i - (len - 1) / 2;
                end = i + len / 2;
            }
        }
        
        return s.substring(start, end + 1);
    }

    private static int expandAroundCenter(String s, int left, int right) {
        int L = left, R = right;
        
        while (L >= 0 && R < s.length() && s.charAt(L) == s.charAt(R)) {
            L--;
            R++;
        }
        
        return R - L - 1;
    }
}

```

## Challenge 2:

Write a program to get the output:
Eg. 1: input: a1b10
Output abbbbbbbbb
Eg. 2 input b3c6d15
output bbbccccccddddddddddddddd
The number varies from 1 to 99.
```
public class StringExpander {
    public static void main(String[] args) {
        String input1 = "a1b10";
        String input2 = "b3c6d15";
        
        System.out.println("Output for input \"" + input1 + "\": " + expandString(input1));
        System.out.println("Output for input \"" + input2 + "\": " + expandString(input2));
    }

    public static String expandString(String input) {
        StringBuilder result = new StringBuilder();
        int length = input.length();
        int i = 0;
        
        while (i < length) {
            char ch = input.charAt(i);
            i++;
            int number = 0;
            
            // Read the number part
            while (i < length && Character.isDigit(input.charAt(i))) {
                number = number * 10 + (input.charAt(i) - '0');
                i++;
            }
            
            // Append the character 'number' times to the result
            for (int j = 0; j < number; j++) {
                result.append(ch);
            }
        }
        
        return result.toString();
    }
}

```

## Challenge 3:

Find Duplicates in Array? Display its frequency.
```
import java.util.HashMap;
import java.util.Map;

public class FindDuplicates {
    public static void main(String[] args) {
        int[] array = {4, 5, 6, 7, 8, 4, 5, 6, 4, 6, 6};
        findAndDisplayDuplicates(array);
    }

    public static void findAndDisplayDuplicates(int[] array) {
        HashMap<Integer, Integer> frequencyMap = new HashMap<>();
        
        // Count frequencies
        for (int num : array) {
            frequencyMap.put(num, frequencyMap.getOrDefault(num, 0) + 1);
        }
        
        // Display duplicates and their frequencies
        System.out.println("Duplicate elements and their frequencies:");
        for (Map.Entry<Integer, Integer> entry : frequencyMap.entrySet()) {
            if (entry.getValue() > 1) {
                System.out.println("Element: " + entry.getKey() + ", Frequency: " + entry.getValue());
            }
        }
    }
}

```

## Challenge 4:

Write a program to print the following output for the given input. You can assume the string is of odd length.
Input: 12345

```
public class PrintPattern {
    public static void main(String[] args) {
        String input = "12345";
        printPattern(input);
    }

    public static void printPattern(String input) {
        int length = input.length();
        int middleIndex = length / 2;
        
        // Print the upper part of the pattern
        for (int i = 0; i <= middleIndex; i++) {
            for (int j = 0; j < i; j++) {
                System.out.print(" ");
            }
            System.out.println(input.charAt(i));
        }
        
        // Print the lower part of the pattern
        for (int i = middleIndex + 1; i < length; i++) {
            for (int j = middleIndex; j < i; j++) {
                System.out.print(" ");
            }
            System.out.println(input.charAt(i));
        }
    }
}

```

## Challenge 5:

Given two sorted arrays, merge them such that the elements are not repeated
Eg 1: Input:Array 1: 2,4,5,6,7,9,10,13
        Array 2: 2,3,4,5,6,7,8,9,11,15
       Output array: 2,3,4,5,6,7,8,9,10,11,13,15
```
import java.util.ArrayList;
import java.util.List;

public class MergeSortedArrays {
    public static void main(String[] args) {
        int[] array1 = {2, 4, 5, 6, 7, 9, 10, 13};
        int[] array2 = {2, 3, 4, 5, 6, 7, 8, 9, 11, 15};
        
        int[] mergedArray = mergeArrays(array1, array2);
        
        System.out.print("Merged array: ");
        for (int num : mergedArray) {
            System.out.print(num + " ");
        }
    }

    public static int[] mergeArrays(int[] array1, int[] array2) {
        List<Integer> resultList = new ArrayList<>();
        int i = 0, j = 0;
        
        while (i < array1.length && j < array2.length) {
            if (array1[i] < array2[j]) {
                if (resultList.isEmpty() || resultList.get(resultList.size() - 1) != array1[i]) {
                    resultList.add(array1[i]);
                }
                i++;
            } else if (array1[i] > array2[j]) {
                if (resultList.isEmpty() || resultList.get(resultList.size() - 1) != array2[j]) {
                    resultList.add(array2[j]);
                }
                j++;
            } else {
                if (resultList.isEmpty() || resultList.get(resultList.size() - 1) != array1[i]) {
                    resultList.add(array1[i]);
                }
                i++;
                j++;
            }
        }
        
        while (i < array1.length) {
            if (resultList.isEmpty() || resultList.get(resultList.size() - 1) != array1[i]) {
                resultList.add(array1[i]);
            }
            i++;
        }
        
        while (j < array2.length) {
            if (resultList.isEmpty() || resultList.get(resultList.size() - 1) != array2[j]) {
                resultList.add(array2[j]);
            }
            j++;
        }
        
        int[] mergedArray = new int[resultList.size()];
        for (int k = 0; k < resultList.size(); k++) {
            mergedArray[k] = resultList.get(k);
        }
        
        return mergedArray;
    }
}

```

## Challenge 6:

Using Recursion reverse the string such as Eg 1: Input: one two three
      Output: three two one
Eg 2: Input: I love india
      Output: india love I

```
public class ReverseWords {
    public static void main(String[] args) {
        String input1 = "one two three";
        String input2 = "I love india";
        
        System.out.println("Reversed: " + reverseWords(input1));
        System.out.println("Reversed: " + reverseWords(input2));
    }

    public static String reverseWords(String str) {
        String[] words = str.split(" ");
        return reverseWordsHelper(words, 0);
    }

    private static String reverseWordsHelper(String[] words, int index) {
        if (index == words.length - 1) {
            return words[index];
        }
        return reverseWordsHelper(words, index + 1) + " " + words[index];
    }
}

```

## Challenge 7:

Find if a String2 is substring of String1. If it is, return the index of the first occurrence. else return -1.
```
public class SubstringFinder {
    public static void main(String[] args) {
        String str1 = "test123string";
        String str2 = "123";
        System.out.println("Output: " + findSubstringIndex(str1, str2));
        
        str1 = "testing12";
        str2 = "1234";
        System.out.println("Output: " + findSubstringIndex(str1, str2));
    }

    public static int findSubstringIndex(String str1, String str2) {
        return str1.indexOf(str2);
    }
}

```

## Challenge 8:

Write a program to sort the elements in odd positions in descending order & even position elements in ascen order
```
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class SortOddEvenPositions {
    public static void main(String[] args) {
        int[] input1 = {13, 2, 4, 15, 12, 10, 5};
        int[] input2 = {1, 2, 3, 4, 5, 6, 7, 8, 9};
        
        System.out.print("Output for input1: ");
        sortOddEvenPositions(input1);
        
        System.out.print("Output for input2: ");
        sortOddEvenPositions(input2);
    }

    public static void sortOddEvenPositions(int[] arr) {
        List<Integer> oddPositions = new ArrayList<>();
        List<Integer> evenPositions = new ArrayList<>();
        
        // Separate elements into odd and even position lists
        for (int i = 0; i < arr.length; i++) {
            if (i % 2 == 0) {
                oddPositions.add(arr[i]);
            } else {
                evenPositions.add(arr[i]);
            }
        }
        
        // Sort odd positions in descending order
        Collections.sort(oddPositions, Collections.reverseOrder());
        // Sort even positions in ascending order
        Collections.sort(evenPositions);
        
        // Merge sorted elements back into the original array
        int oddIndex = 0;
        int evenIndex = 0;
        for (int i = 0; i < arr.length; i++) {
            if (i % 2 == 0) {
                arr[i] = oddPositions.get(oddIndex++);
            } else {
                arr[i] = evenPositions.get(evenIndex++);
            }
        }
        
        // Print the sorted array
        for (int num : arr) {
            System.out.print(num + " ");
        }
        System.out.println();
    }
}

```

## Challenge 9:

Design a Call taxi booking application
```
import java.util.ArrayList;
import java.util.List;

class Taxi {
    private int taxiId;
    private String currentLocation;
    private int totalEarnings;
    private List<Booking> bookings;

    public Taxi(int taxiId) {
        this.taxiId = taxiId;
        this.currentLocation = "A";
        this.totalEarnings = 0;
        this.bookings = new ArrayList<>();
    }

    public int getTaxiId() {
        return taxiId;
    }

    public String getCurrentLocation() {
        return currentLocation;
    }

    public void setCurrentLocation(String currentLocation) {
        this.currentLocation = currentLocation;
    }

    public int getTotalEarnings() {
        return totalEarnings;
    }

    public void addEarnings(int amount) {
        this.totalEarnings += amount;
    }

    public List<Booking> getBookings() {
        return bookings;
    }

    public void addBooking(Booking booking) {
        this.bookings.add(booking);
    }
}
class Booking {
    private int bookingId;
    private int customerId;
    private String from;
    private String to;
    private int pickupTime;
    private int dropTime;
    private int amount;

    public Booking(int bookingId, int customerId, String from, String to, int pickupTime, int dropTime, int amount) {
        this.bookingId = bookingId;
        this.customerId = customerId;
        this.from = from;
        this.to = to;
        this.pickupTime = pickupTime;
        this.dropTime = dropTime;
        this.amount = amount;
    }

    public int getBookingId() {
        return bookingId;
    }

    public int getCustomerId() {
        return customerId;
    }

    public String getFrom() {
        return from;
    }

    public String getTo() {
        return to;
    }

    public int getPickupTime() {
        return pickupTime;
    }

    public int getDropTime() {
        return dropTime;
    }

    public int getAmount() {
        return amount;
    }
}
import java.util.ArrayList;
import java.util.List;

class TaxiBookingSystem {
    private List<Taxi> taxis;
    private int bookingIdCounter;

    public TaxiBookingSystem(int numberOfTaxis) {
        taxis = new ArrayList<>();
        for (int i = 1; i <= numberOfTaxis; i++) {
            taxis.add(new Taxi(i));
        }
        bookingIdCounter = 1;
    }

    public void bookTaxi(int customerId, String from, String to, int pickupTime) {
        Taxi assignedTaxi = null;
        int minDistance = Integer.MAX_VALUE;

        for (Taxi taxi : taxis) {
            int distance = getDistance(taxi.getCurrentLocation(), from);
            if (distance < minDistance || (distance == minDistance && taxi.getTotalEarnings() < (assignedTaxi != null ? assignedTaxi.getTotalEarnings() : Integer.MAX_VALUE))) {
                if (isTaxiFree(taxi, pickupTime, from)) {
                    minDistance = distance;
                    assignedTaxi = taxi;
                }
            }
        }

        if (assignedTaxi != null) {
            int dropTime = pickupTime + getTravelTime(from, to);
            int amount = calculateFare(from, to);
            Booking booking = new Booking(bookingIdCounter++, customerId, from, to, pickupTime, dropTime, amount);
            assignedTaxi.addBooking(booking);
            assignedTaxi.addEarnings(amount);
            assignedTaxi.setCurrentLocation(to);
            System.out.println("Taxi can be allotted.");
            System.out.println("Taxi-" + assignedTaxi.getTaxiId() + " is allotted");
        } else {
            System.out.println("No Taxi can be allotted.");
        }
    }

    public void displayTaxiDetails() {
        for (Taxi taxi : taxis) {
            System.out.println("Taxi-" + taxi.getTaxiId() + " Total Earnings: Rs. " + taxi.getTotalEarnings());
            for (Booking booking : taxi.getBookings()) {
                System.out.println(booking.getBookingId() + " " + booking.getCustomerId() + " " + booking.getFrom() + " " + booking.getTo() + " " + booking.getPickupTime() + " " + booking.getDropTime() + " " + booking.getAmount());
            }
        }
    }

    private int getDistance(String from, String to) {
        return Math.abs(from.charAt(0) - to.charAt(0)) * 15;
    }

    private int getTravelTime(String from, String to) {
        return getDistance(from, to) / 15 * 1; // Since 15 kms takes 60 mins
    }

    private int calculateFare(String from, String to) {
        int distance = getDistance(from, to);
        if (distance <= 5) {
            return 100;
        } else {
            return 100 + (distance - 5) * 10;
        }
    }

    private boolean isTaxiFree(Taxi taxi, int pickupTime, String pickupPoint) {
        for (Booking booking : taxi.getBookings()) {
            if (booking.getDropTime() > pickupTime) {
                return false;
            }
        }
        return true;
    }
}
public class Main {
    public static void main(String[] args) {
        TaxiBookingSystem system = new TaxiBookingSystem(4);

        system.bookTaxi(1, "A", "B", 9);
        system.bookTaxi(2, "B", "D", 9);
        system.bookTaxi(3, "B", "C", 12);

        system.displayTaxiDetails();
    }
}

```

## Challenge 10:

Find the minimum number of times required to represent a number as sum of squares.
```
public class MinimumSquares {
    public static void main(String[] args) {
        int input = 12;
        int result = minNumberOfSquares(input);
        System.out.println("Min: " + result);
    }

    public static int minNumberOfSquares(int n) {
        // Array to store the minimum number of squares for each number up to n
        int[] dp = new int[n + 1];
        
        // Initialize dp array with a large value
        for (int i = 1; i <= n; i++) {
            dp[i] = Integer.MAX_VALUE;
        }
        
        // Base case
        dp[0] = 0;
        
        // Fill dp array
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j * j <= i; j++) {
                dp[i] = Math.min(dp[i], dp[i - j * j] + 1);
            }
        }
        
        return dp[n];
    }
}

```
