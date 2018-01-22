## MACEPS

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the machine epsilon or the precision of any computer.

**Input:** There are no inputs needed in this case.

**Output:** This function returns a double of the percision of the computer.

**Usage/Example:**

      cout << maceps() << endl;
  
Output from the lines above:

      1.11022e-16

**Implementation/Code:** The following is the code for maceps()

      double maceps() {
          double num = 1.0;
          while (num + 1.0 != 1.0) {
              num /= 2;
          }
          return num;
       }
