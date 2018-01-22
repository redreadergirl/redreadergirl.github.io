## ABSOLUTE ERROR

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the absolute error of an approximation.

**Input:** 
        
        x = approximation
        xbar = exact solution

**Output:** The function will output a double of the absolute error

**Usage/Example:**

        abserr(double x, double xbar)
        x = 1, xbar = 1.00001
       
Output from the lines above:

        1e-05
  
**Implementation/Code:** The following is the code for abserr()

        double abserr(double x, double xbar) {
	        double error = x - xbar;
	        if (error < 0) {
		        error *= -1;
	        }
	        return error;
        }
