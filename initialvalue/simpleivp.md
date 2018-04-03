## ANALYTIC SOLUTION TO SIMPLE IVP

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the analytic solution to the simple initial value problem u'= λu

**Input:**

	double alpha = u(0)
	double lambda = λ
	double t = time you want to solve for;
  
**Output:** The function will output the value u evaluated at time t as a double

**Usage/Example:**

    simpleIVP(double alpha, double lambda, double t)
    alpha = 0.1
    lambda = -1
    t = 1

Output from the lines above:

	0.0368
    
**Implementation/Code:** The following is the code for simpleIVP()

    double simpleIVP(double alpha, double lambda, double t) {
	    double etl = 1;
	    double x = t * lambda;
	    double fact = 1;
	    for (int i = 1; i < 10; i++) {
		    fact *= i;
		    etl += pow(x, i) / fact;
	    }
	    return alpha * etl;
    }
