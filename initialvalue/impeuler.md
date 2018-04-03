## IMPLICIT EULER METHOD

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to an initial value problem using the implicit euler method.

**Input:**

	double u0 = initial u value;
	double t0 = initial t value;
	double time = time you want to solve for;
  
  	The user will provide a function to solve f(u, t) and f'(u,t)
  
**Output:** The function will output the value of u evaluated at time as a double

**Usage/Example:**

	implicitEulers(double u0, double t0, double time)
  	u0 = .1
  	t0 = 0
  	time = 1
  	f(u, t) = -u

Output from the lines above:

	0.0361
    
**Implementation/Code:** The following is the code for implicitEulers()

    double evalF(double t, double y) {
	    return -1 * y;
    }

    double findFPrime(double u) {
	    return -1;
    }

    double implicitEulers(double u0, double t0, double time) {
	    double k = .0125;
	    double u = u0;
	    double t = t0;
	    while (t < time) {
		    double fPrime = findFPrime(u);
		    double eval = evalF(t, u) / fPrime;
		    double y = evalF(t, eval) * k;
		    u += y;
		    t += k;
    	}
	    return u;
    }
