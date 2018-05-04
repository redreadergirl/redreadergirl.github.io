## WARMING AND BEAM

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to a hyperbolic equation using warming and beam
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

	beamWarming(0, 1, 10, 1, .001, 2)
  	f(x, 0) = x

Output from the lines above:

	{1, 1.11, 1.22, 1.33, 1.44, 1.55, 1.66, 1.77, 1.88, 2}
    
**Implementation/Code:** The following is the code for beamWarming()

    Matrix beamWarming(double x0, double xn, double n, double t, double deltaT, int a) {
	    double deltaX = (xn - x0) / (n - 1);
	    Matrix A(n);
	    int numberOfSteps = t / deltaT;
	    double center = 1 - ((3 * a * deltaT) / (2 * deltaX)) + (a * a * deltaT * deltaT) / (2 * deltaX * deltaX);
	    double left1 = ((2 * a * deltaT) / (deltaX)) - ((a * a * deltaT * deltaT) / (deltaX * deltaX));
	    double left2 = ((-1 * a * deltaT) / (2 * deltaX)) + ((a * a * deltaT * deltaT) / (2 * deltaX * deltaX));
	    for (int i = 0; i < n; i++) {
		    A.setVecUnit(i, i, center);
		    if (i != n - 1) {
			    A.setVecUnit(i + 1, i, left1);
			    if (i != n - 2) {
				    A.setVecUnit(i + 2, i, left2);
		    	}
		    }
	    }
	    A.setVecUnit(0, n - 1, left1);
	    A.setVecUnit(0, n - 2, left2);
	    A.setVecUnit(1, n - 1, left2);
	    Matrix U(n, 1, 0);
	    U = fillU(U, xn, deltaX);
	    for (int i = 0; i < numberOfSteps; i++) {
		    U = A * U;
	    }
	    return U;
    }
