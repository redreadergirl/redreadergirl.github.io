## LAX-WENDROFF

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to a hyperbolic equation using lax-wendroff
**Input:**

	double x0 = beginning of mesh at time zero
  	double xn = end of mesh at time zero
  	double n = size of mesh
  	double t = final time you are solving for
  	double deltaT = change it t
  	int a = coefficient in front of ux
  
  	function must be provided for f(x, 0)
  
**Output:** The function will output a column vector as a Matrix of solutions at time t

**Usage/Example:**

	laxWendroff(0, 1, 10, 1, .001, 2)
  	f(x, 0) = x

Output from the lines above:

	{8.87, 12.22, 7.89, 11.63, 4.63, 10.98, .888, 10.92, -2.36, 11.06}
    
**Implementation/Code:** The following is the code for laxWendroff()

    Matrix laxWendroff(double x0, double xn, double n, double t, double deltaT, int a) {
	    double deltaX = (xn - x0) / (n - 1);
	    Matrix A(n);
	    int numberOfSteps = t / deltaT;
	    double center = 1 - (-1 * a * a * deltaT * deltaT) / (deltaX * deltaX);
	    double left = ((a * deltaT) / (2 * deltaX)) + ((a * a * deltaT * deltaT) / (2 * deltaX * deltaX));
	    double right = ((-1 * a * deltaT) / (2 * deltaX)) + ((a * a * deltaT * deltaT) / (2 * deltaX * deltaX));
	    for (int i = 0; i < n; i++) {
	    	A.setVecUnit(i, i, center);
		    if (i != n - 1) {
		    	A.setVecUnit(i, i + 1, right);
			    A.setVecUnit(i + 1, i, left);
	    	}
    	}
    	A.setVecUnit(0, n - 1, left);
	    Matrix U(n, 1, 0);
    	U = fillU(U, xn, deltaX);
	    for (int i = 0; i < numberOfSteps; i++) {
		    U = A * U;
    	}
	    return U;
    }
