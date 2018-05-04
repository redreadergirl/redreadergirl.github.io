## EXPLICIT EULERS METHOD

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to the heat equation using the explicit eulers method.

**Input:**

	double k = change in t
  double h =  change in x
  int n = size of mesh
  vector<double> f = initial values of x's
  int finalt = time you are solving for
  int alpha = coefficient in front of uxx
  
**Output:** The function will output a column vector as a Matrix of solutions at time finalt

**Usage/Example:**

	explicitEulers(.001, .1, 11, {0, .1, .2, .3, .4, .5, .6, .7, .8, .9, 1}, 10, 1)

Output from the lines above:

	{1.53e-26, 2.17e-26, 2.7e-26, 3.07e-26, 3.26e-26, 3.26e-26, 3.07e-26, 2.73-26, 2.18e-26, 1.53e-26, 7.86e-27}
    
**Implementation/Code:** The following is the code for explicitEulerParab()

	  Matrix explicitEulerParab(double k, double h, int n, vector<double> f, int finalt, int alpha) {
	   int numOfSteps = finalt / k;
	    Matrix A(n);
	    double step = (alpha * k) / (h * h);
	    for (int i = 0; i < n; i++) {
		    A.setVecUnit(i, i, (1 - (2 * step)));
		    if (i != n - 1) {
			    A.setVecUnit(i, i + 1, step);
			    A.setVecUnit(i + 1, i, step);
		    }
	    }
	    A.setVecUnit(0, n - 1, step);
	    Matrix U(f);
	    for (int i = 0; i < numOfSteps; i++) {
		    U = A * U;
	    }
	    return U;
    }
