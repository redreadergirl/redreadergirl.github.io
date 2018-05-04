## IMPLICIT EULERS METHOD

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to the heat equation using the implicit eulers method.

**Input:**

	double k = change in t
  double h =  change in x
  int n = size of mesh
  vector<double> f = initial values of x's
  int finalt = time you are solving for
  int alpha = coefficient in front of uxx
  
**Output:** The function will output a column vector as a Matrix of solutions at time finalt

**Usage/Example:**

	implicitEulerParab(.001, .1, 11, {0, .1, .2, .3, .4, .5, .6, .7, .8, .9, 1}, 10, 1)

Output from the lines above:

	{1.48e-323, 1.48e-323, 1.48e-323, 1.48e-323, 1.48e-323, 1.48e-323, 1.48e-323, 1.48e-323, 1.48e-323, 1.48e-323, 1.48e-323}
    
**Implementation/Code:** The following is the code for implicitEulerParab()

	    Matrix implicitEulerParab(double k, double h, int n, vector<double> f, int finalt, int alpha) {
	      int numOfSteps = finalt / k;
	      Matrix A(n);
	      double step = (alpha * k) / (h * h);
	      for (int i = 0; i < n; i++) {
		      A.setVecUnit(i, i, (1 + (2 * step)));
		      if (i != n - 1) {
			      A.setVecUnit(i, i + 1, -1 * step);
			      A.setVecUnit(i + 1, i, -1 * step);
	      	}
	      }
	      A.setVecUnit(0, n - 1, -1 * step);
	      Matrix U(f);
	      for (int i = 0; i < numOfSteps; i++) {
		      int r = U.getRow();
		      Matrix temp(n, 1, 0);
		      for (int i = r - 1; i >= 0; i--) {
			      double left = U.getVecUnit(i, 0);
			      for (int j = i; j < r; j++) {
				      left -= (A.getVecUnit(i, j) * temp.getVecUnit(j, 0));
		      	}
			      temp.setVecUnit(i, 0, (left / A.getVecUnit(i, i)));
	      	}
		      U = temp;
	      }
      	return U;
      }
