## LOGISTIC EQUATION

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will calculate the value of the solution of the logistic equation at an arbitrary point.

**Input:** 

      p0 = initial condition at P(0)
      a = alpha
      b = beta
      t = time

**Output:** The function will output a double solution of the function at time t.

**Usage/Example:**

        logistic(a, b, p0, t);
        a = 1, b = 2, p0 = 3, t = 4
       
Output from the lines above:

        0.50775
  
**Implementation/Code:** The following is the code for logistic()

        double logistic(double a, double b, double p0, double t) {
	            double exponent = exp(-1 * a * t);
	            double p = a / ((((a / p0) - b) * exponent) + b);
	            return p;
        }
