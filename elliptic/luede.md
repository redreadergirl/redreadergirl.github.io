## LU FACTORIZATION SOLUTION OF ELLIPTIC ODE

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solutioin of an elliptic ODE using LU Factorization

**Input:**

	int n = size of mesh
  [initiate with initede()](initede.md)
	
**Output:** The function will output the solution to the ODE at each mesh point.

**Usage/Example:**

	luede(int n);
  n = 4;
  f = x;
  a = 1;
  b = 2;
  ua = 1;
  ub = 2;

Output from the lines above:

	{ -0.484375, -1.89063, -3.20313}
    
**Implementation/Code:** The following is the code for luede()

  Matrix luede(int n) {
	  initEDE(n);
	  Matrix x(n - 1, 1, 0);
	  for (int i = 0; i < n - 1; i++) {
		  x.setVecUnit(i, 0, rhs[i]);
	  }
	  return lufactorization(T, x);
  }
  
**Link to lufactorization:**
  [lufactorization()](../append/lufactorization.md)
