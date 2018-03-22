## JACOBI ITERATION

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to an elliptic ODE using Jacobi Iteration.

**Input:**

	Matrix A = Matrix formed from ODE;
	vector<double> c = right hand side of equation
	
**Output:** The function will output the solution to the function at each point int the mesh

**Usage/Example:**

	jacobi(Matrix A, vector<double> c)
	Matrix A = {{-2, 1, 0}, {1, -2, 1}, {0, 1, -2}}
	vector<double> c = {1.25, 1.5, 1.75}

Output from the lines above:

	{1.11652, 1.31186, 1.6009}
    
**Implementation/Code:** The following is the code for jacobi()

	Matrix jacobi(Matrix A, vector<double> c) {
		int n = A.getCol();

		Matrix D(n - 1, n - 1, 0);
		Matrix R = T;
		Matrix b(n - 1, 1, 0);
		for (int i = 0; i < n - 1; i++) {
			D.setVecUnit(i, i, 1 / A.getVecUnit(i, i));
			R.setVecUnit(i, i, 0);
			b.setVecUnit(i, 0, c[i]);
		}
		double tol = .0001;
		double error = 10 * tol;
		int maxiter = 750;
		int iter = 0;
		Matrix x(n - 1, 1, 0);
		Matrix temp(n - 1, 1, 0);
		while (error > tol && iter < maxiter) {
			iter++;
			temp = D * (b - (R * x));
			Matrix errorMat = temp - x;
			error = tnorm(errorMat.getVector());
			x = temp;
		}
		return x;
	}
