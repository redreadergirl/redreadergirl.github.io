## UPWINDING

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to a hyperbolic equation using upwinding
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

	upwinding(0, 1, 10, 1, .001, 2)
  	f(x, 0) = x

Output from the lines above:

	{.491, .497, .504, .510, .512, .509, .502, .495, .489, .487}
    
**Implementation/Code:** The following is the code for upwinding()

    Matrix upwinding(double x0, double xn, double n, double t, double deltaT, int a) {
	    double deltaX = (xn - x0) / (n - 1);
	    Matrix A(n);
	    int numberOfSteps = t / deltaT;
	    double step = (a * deltaT) / deltaX;
    	for (int i = 0; i < n; i++) {
    		A.setVecUnit(i, i, (A.getVecUnit(i, i) - step));
	    	if (i != n - 1) {
		    	A.setVecUnit(i + 1, i, step);
		    }
	    }
	    A.setVecUnit(0, n - 1, step);
	    Matrix U(n, 1, 0);
	    U = fillU(U, x0, deltaX);
	    for (int i = 0; i < numberOfSteps; i++) {
		    U = A * U;
    	}
	    return U;
    }
