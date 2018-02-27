## POWER METHOD ITERATION

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the largest eigenvalue of a matrix using the power method iteration.

**Input:**

	Matrix A: matrix
	
**Output:** The function will output the largest eigenvalue as a double

**Usage/Example:**

	powerIteration(A)
  	Matrix A = { {1, 1/2, 1/3}, {1/2, 1/3, 1/4}, {1/3, 1/4, 1/5} }

Output from the lines above:

  	1.40831
	
**Implementation/Code:** The following is the code for powerIteration()

	  double powerIteration(Matrix A) {
		Matrix v(A.getCol(), 1, 1);
	  	double tol = .001;
	  	int maxiter = 50;
	  	double error = 10 * tol;
	  	v.normalize(tnorm(v.getVector()));
	  	double lambdaMax = 0.0;
		  int iter = 0;
		  while (error > tol && iter < maxiter) {
			  iter++;
			  Matrix u = A * v;
			  Matrix y = u;
			  u.normalize(tnorm(u.getVector()));
			  Matrix lambda = u.transpose() * y;
			  error = abs(lambda.getVecUnit(0, 0) - lambdaMax);
			  lambdaMax = lambda.getVecUnit(0, 0);
			  v = u;
		  }
		  return lambdaMax;
  	}
  
Matrix class:
 [Matrix](../append/matrix.md)
