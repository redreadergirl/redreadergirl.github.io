## INVERSE POWER METHOD

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the smallest eigenvalue of a matrix using the inverse power method.

**Input:**

	Matrix A: matrix
	
**Output:** The function will output the smallest eigenvalue as a double

**Usage/Example:**

	inverseIteration(A)
  	Matrix A = { {-2, 1, 0}, {1, -2, 1}, {0, 1, -2} }

Output from the lines above:

  	0.585794
	
**Implementation/Code:** The following is the code for inverseIteration()

	  double inverseIteration(Matrix A) {
	    Matrix v(A.getCol(), 1, 1);
	    v.normalize(tnorm(v.getVector()));
	    int maxiter = 750;
	    int iter = 0;
	    double tol = .001;
	    double error = tol * 10;
	    double lambdaMin = 0.0;

	    while (error > tol && iter < maxiter) {
		    iter++;
		    Matrix u = lufactorization(A, v);
		    Matrix y = u;
		    u.normalize(tnorm(u.getVector()));
		    Matrix lambda = u.transpose() * y;
		    error = abs(lambda.getVecUnit(0, 0) - lambdaMin);
		    lambdaMin = lambda.getVecUnit(0, 0);
		    v = u;
	    }

	    return 1 / lambdaMin;
  }
  
Matrix Class: [Matrix](../append/matrix.md)
