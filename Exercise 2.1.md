
## Exercise 2.1

The value of variable 'result' at end of program depends on whether the array 'nums' that is passed to 'avg' method is empty or not empty.

In case 1, where array 'nums' contains elements [1, 2]:

- Array 'nums' in initialized with values of '{1, 2}
- 'avg' method is called with this array.
- In the method, array is checked for being either null or having length of 0. Since nums is not null and length is not 0, the if statement evaluates to false.
- Next, for loop iterates over 'nums' elements and sums them up. Result is 1 + 2 = 3.
- Average is then calculated as 3 / 2 = 1.5
- The method 'avg' returns '1.5', this is assigned to varaible 'result'.
- **At program's end, 'result'
 holds value '1.5'**

In case 2, where array 'nums' is empty:

- Array 'nums' is initialized as empty array {}
- Method 'avg' is called with this array.
- In the metod, array is checked for being null or having length of 0. Since nums is empty, the if statement evaluates to 'true'.
- 'EmptyArray' exception gets thrown.
- This exception is caught by catch block in 'main' method.
- The 'catch' block does not alter 'result' variable and 'result' was never initialized in first place. So, 'result' is still uninitialized.
- As local variable 'result' has been declared but not assigned a value before or within 'try' block, it's use causes Java compile error. **Therefore, the program will not compile.**
<br>
<br>
---
<br>
Modifying 'avg' method for non-negative numbers only, taking into account different ordinals:
<br>
<br>

```Java
import java.util.ArrayList;
import java.util.List;

class EmptyArray extends Exception {
    private static final long serialVersionUID = 1L;
}

class NegativeNumberException extends Exception {
    private static final long serialVersionUID = 1L;
    private final List<Integer> indices;
    private final List<Integer> values;

    public NegativeNumberException(List<Integer> indices, List<Integer> values) {
        this.indices = indices;
        this.values = values;
    }

    public List<Integer> getIndices() {
        return indices;
    }

    public List<Integer> getValues() {
        return values;
    }
}

public class Main {
    float avg(int[] nums) throws EmptyArray, NegativeNumberException {
        int sum = 0;

        if (nums == null || nums.length == 0)
            throw new EmptyArray();

        List<Integer> negativeIndices = new ArrayList<>();
        List<Integer> negativeValues = new ArrayList<>();

        for (int i = 0; i < nums.length; i++) {
            if (nums[i] < 0) {
                negativeIndices.add(i + 1);
                negativeValues.add(nums[i]);
            } else {
                sum += nums[i];
            }
        }

        if (!negativeIndices.isEmpty()) {
            throw new NegativeNumberException(negativeIndices, negativeValues);
        }

        return sum / (float) nums.length;
    }

    public static void main(String[] args) {
        Main instance = new Main();
        instance.run();
    }

    void run() {
        int[] nums = new int[] { -2, -4, -3, -10, 5, 8};
        Float result = null;

        try {
            result = avg(nums);
            System.out.println(result);
        } catch (EmptyArray e) {
            System.out.println("The array is empty.");
        } catch (NegativeNumberException e) {
            List<Integer> indices = e.getIndices();
            List<Integer> values = e.getValues();
            for (int i = 0; i < indices.size(); i++) {
                System.out.printf("The %s number %d in your array is invalid%n", getOrdinal(indices.get(i)), values.get(i));
            }
        }
    }

    String getOrdinal(int number) {
        if (number <= 0) {
            throw new IllegalArgumentException("Number must be positive");
        }
        int mod100 = number % 100;
        int mod10 = number % 10;
        if (mod100 - mod10 == 10) {
            return number + "th";
        }
        switch (mod10) {
            case 1: return number + "st";
            case 2: return number + "nd";
            case 3: return number + "rd";
            default: return number + "th";
        }
    }
}
```
---