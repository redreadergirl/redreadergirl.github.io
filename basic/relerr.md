## RELATIVE ERROR

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the relative error of an approximation.

**Input:** 
        
        x = approximation
        xbar = exact solution

**Output:** The function will output a double of the relative error.

**Usage/Example:**

        relerr(double x, double xbar)
        x = 1, xbar = 1.00001
       
Output from the lines above:

        9.9999e-06
  
**Implementation/Code:** The following is the code for relerr()

        double relerr(double x, double xbar) {
	        double error = (x - xbar) / xbar;
	        if (error < 0) {
		        error *= -1;
	        }
	        return error;
        }
