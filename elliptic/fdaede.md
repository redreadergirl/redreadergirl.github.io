## FINITE DIFFERENCE APPROXIMATION WITH COEFFICIENT FUNCTION

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the finite difference approximation of an elliptic ODE where k(x) is a coefficient function

**Input:**

	int n = size of mesh
	
**Output:** The function will output finite difference approximation at each point in the mesh

**Usage/Example:**

	fdaede(int n)
	n = 4;
	f = x;
	a = 1;
	b = 2;
	ua = 1;
	ub = 2;

Output from the lines above:

	k(x) generated: {10, 27, 30}
	{0.0626198, 0.0330521, 0.0463838}
    
**Implementation/Code:** The following is the code for fdaede()

	Matrix fdaede(int n) {
		initEDE(n);

		Matrix K(n - 1, 1, 0);
		Matrix b(n - 1, 1, 0);
		for (int i = 0; i < n - 1; i++) {
			int random = (rand() % (50 - 10 + 1)) + 10;
			K.setVecUnit(i, 0, random);
			b.setVecUnit(i, 0, rhs[i]);
		}

		for (int i = 0; i < n - 2; i++) {
			T.setVecUnit(i, i, T.getVecUnit(i, i) * K.getVecUnit(i, 0));
			T.setVecUnit(i, i+1, T.getVecUnit(i, i+1) * K.getVecUnit(i, 0));
			T.setVecUnit(i+1, i, T.getVecUnit(i+1, i) * K.getVecUnit(i, 0));
		}
		T.setVecUnit(n - 2, n - 2, T.getVecUnit(n - 2, n - 2) * K.getVecUnit(n - 2, 0));

		Matrix ans = lufactorization(T, b);

		return ans;
	}
