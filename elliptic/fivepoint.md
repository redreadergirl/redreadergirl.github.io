## FIVE POINT STENCIL

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute an approximation of the solution to the Laplace Equation using a 5-point stencil.

**Input:**

	int n: number of divisions in the mesh in both x and y
  	string y: f(x) - User will provide code if they don't want f(x)=sin(xy)
	
**Output:** The function will output a vector of doubles with the solutions in the following order:
    
    {U11, U21, U31, U12, U22, U32, U13, U23, U33}

**Usage/Example:**

    fivePointStencil(int n, string y)
    n = 3
    y = "sin(xy)"

Output from the lines above:

  	{-0.077, -0.299, 0.015, -0.299, -0.584, -0.4085, 0.015, -0.4085, -0.815}
	
**Implementation/Code:** The following is the code for fivePointStencil()

	vector<double> inity(string y, int n, double h) {
		vector<double> answer(n * n, 0);
			for (int i = 0; i < n; i++) {
				for (int j = 0; j < n; j++) {
					answer[i * n + j] += sin(((i + 1) * (j+1)) / (h * h));
				}
			}
			return answer;
    	}

    vector<double> fivePointStencil(double n, string y) {
	    double h = 1 / (n + 1);
	    Matrix diag({ {-4, 1, 0}, {1, -4, 1}, {0, 1, -4} });
	    Matrix iMat(3);
	    Matrix zero(3, 3, 0);
	    vector<Matrix> row(n, zero);
	    vector < vector<Matrix>> matrix(n, row);
	    for (int i = 0; i < n - 1; i++) {
		    matrix[i][i] = diag;
		    matrix[i][i + 1] = iMat;
		    matrix[i + 1][i] = iMat;
	    }
	    matrix[n - 1][n - 1] = diag;
	    Matrix newMatrix(matrix, 3);
	    Matrix T = newMatrix;
	    vector<double> rhs = inity(y, n, h);
	    Matrix f(rhs);
	    Matrix temp = lufactorization(T, f);
	    return temp.getVector();
    }
  
* Matrix Class: [Matrix](../append/matrix.md)
* LU Factorization: [lufactorization()](../append/lufactorization.md)
