## FIVE POINT STENCIL USING CONJUGATE GRADIENT METHOD

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to ▲u = sin(x y) using a five point stencil and the conjugate gradient method

**Input:**

    double n = size of your five point stencil
	
**Output:** The function will output the solution as a vector of doubles.

**Usage/Example:**
 
  	fivePointStencil(3)

Output from the lines above:

	{-0.0778, -0.2996, 0.01504, -0.2996, -0.58404, -0.4085, 0.01504, -0.4085, -0.0815}
    
**Implementation/Code:** The following is the code for fivePointStencil()

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
    
    vector<double> inity(int n, double h) {
	    vector<double> answer(n * n, 0);
	    for (int i = 0; i < n; i++) {
		    for (int j = 0; j < n; j++) {
			    answer[i * n + j] += sin(((i + 1) * (j+1)) / (h * h));
		    }
	    }
	    return answer;
    }

    vector<double> fivePointStencil(double n) {
	    double h = 1 / (n + 1);
	    Matrix diag(n);
	    for (int i = 0; i < n - 1; i++) {
		    diag.setVecUnit(i, i, -4);
		    diag.setVecUnit(i, i + 1, 1);
	  	  diag.setVecUnit(i + 1, i, 1);
	    }
	    diag.setVecUnit(n - 1, n - 1, -4);
	    Matrix iMat(n);
	    Matrix zero(n, n, 0);
	    vector<Matrix> row(n, zero);
	    vector < vector<Matrix>> matrix(n, row);
	    for (int i = 0; i < n - 1; i++) {
		    matrix[i][i] = diag;
		    matrix[i][i + 1] = iMat;
		    matrix[i + 1][i] = iMat;
	    }
	    matrix[n - 1][n - 1] = diag;
	    Matrix newMatrix(matrix, n);
	    T = newMatrix;
	    rhs = inity(n, h);
	    Matrix f(rhs);
	    Matrix temp = conjugateGradient(T, f);
	    return temp.getVector();
    }
