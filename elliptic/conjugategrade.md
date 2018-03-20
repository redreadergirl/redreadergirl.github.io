## CONJUGATE GRADIENT METHOD

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to a linear system of equations using Conjugate Gradient Method

**Input:**

	Matrix A = matrix composed of constants of linear system of equations
  	Matrix f = column matrix composed of the answers of the linear system of equations
	
**Output:** The function will output the solution to the linear system of equations as a Matrix.

**Usage/Example:**

  	conjugateGradient(Matrix A, Matrix f)
  	Matrix A = {{2, 4, -2}, {4, 9, -3}, {-2, -3, 7}};
  	Matrix f = {{3}, {7}, {5}};

Output from the lines above:

	{4.75, -0.75, 1.75}
    
**Implementation/Code:** The following is the code for conjugateGradient()

    Matrix conjugateGradient(Matrix A, Matrix f) {
	    int n = A.getRow();
	    Matrix u(n, 1, 0);
	    Matrix r = f - (A * u);
	    Matrix p = r;
	    Matrix w(n, 1, 0);
	    Matrix uTemp = u;
	    Matrix rTemp = r;
	    double alpha;
	    double beta;
	    double tol = .0001;
	    int maxiter = 750;
	    int iter = 0;
	    double error = tol * 10;
	    while (iter < maxiter) {
		    w = A * p;
		    Matrix rTr = r.transpose() * r;
		    Matrix pTw = p.transpose() * w;
		    alpha = rTr.getVecUnit(0, 0) / pTw.getVecUnit(0, 0);
		    uTemp = u + (p * alpha);
		    rTemp = r - (w * alpha);
		    if (tnorm(r.getVector()) < tol) {
			    return u;
		    }
		    Matrix rtTrt = rTemp.transpose() * rTemp;
		    beta = rtTrt.getVecUnit(0, 0) / rTr.getVecUnit(0, 0);
		    p = (p * beta) + rTemp;
		    u = uTemp;
		    r = rTemp;
	    }
	    return u;
    }
