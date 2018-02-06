## JACOBI ITERATION

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to an elliptic ODE using Jacobi Iteration.

**Input:**

	int n = size of mesh
  All other input is initiated in [initede()](initede.md)
	
**Output:** The function will output the solution to the function at each point int the mesh

**Usage/Example:**

	jacobi(int n)
  n = 4;
  f = "x";
  a = 1;
  b = 2;
  ua = 1;
  ub = 2;

Output from the lines above:

	{1.11652, 1.31186, 1.6009}
    
**Implementation/Code:** The following is the code for jacobi()

  Matrix jacobi(int n) {
	  initEDE(n);

	  Matrix D(n - 1, n - 1, 0);
	  Matrix R = T;
	  Matrix b(n - 1, 1, 0);
	  for (int i = 0; i < n - 1; i++) {
		  D.setVecUnit(i, i, 1 / T.getVecUnit(i, i));
		  R.setVecUnit(i, i, 0);
		  b.setVecUnit(i, 0, rhs[i]);
	  }

	  int iterations = pow(n, 2) * log(n);

	  Matrix x(n - 1, 1, 0);
	  Matrix temp(n - 1, 1, 0);
	  while (iterations-- > 0) {
		  temp = D * (b - (R * x));
		  x = temp;
	  }

	  return x;
  }
