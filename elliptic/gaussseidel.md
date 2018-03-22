## GAUSS-SEIDEL

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to a linear system of equations using Guass-Seidel

**Input:**

	Matrix A = matrix composed of constants of linear system of equations
  	Matrix b = column matrix composed of the answers of the linear system of equations
	
**Output:** The function will output the solution to the linear system of equations as a Matrix.

**Usage/Example:**

  	gaussSeidel(Matrix A, Matrix b)
  	Matrix A = { {2, 4, -2}, {4, 9, -3}, {-2, -3, 7} };
  	Matrix b = { {3}, {7}, {5} };

Output from the lines above:

	{4.74904, -0.749567, 1.7499}
    
**Implementation/Code:** The following is the code for gaussSeidel()

	Matrix gaussSeidel(Matrix A, Matrix b) {
	  int n = A.getRow();
	  Matrix x(n, 1, 1);
	  Matrix D(n, n, 0);
	  Matrix L(n, n, 0);
	  for (int i = 0; i < n; i++) {
		  for (int j = 0; j < n; j++) {
			  if (i > j) {
				  L.setVecUnit(i, j, A.getVecUnit(i, j));
			  }
			  else {
				  D.setVecUnit(i, j, A.getVecUnit(i, j));
			  }
		  }
	  }
	  double tol = .0001;
	  double error = 10 * tol;
	  int maxiter = 750;
	  int iter = 0;
	  Matrix c(n, 1, 0);
	  while (error > tol && iter < maxiter) {
		  Matrix temp(n, 1, 0);
		  iter++;
		  c = b - (L * x);
		  for (int i = n - 1; i >= 0; i--) {
			  double left = c.getVecUnit(i, 0);
			  for (int j = i; j < n; j++) {
				  left -= (D.getVecUnit(i, j) * temp.getVecUnit(j, 0));
			  }
			  temp.setVecUnit(i, 0, (left / A.getVecUnit(i, i)));
		  }
		  Matrix errorMat = temp - x;
		  error = tnorm(errorMat.getVector());
		  x = temp;
	  }
	  return x;
  	}
