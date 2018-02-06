## LU FACTORIZATION

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will perform LU Factorization to solve for the vector x in Ax = b

**Input:** 
        
        Matrix A = A matrix
        Matrix b = b matrix

**Output:** The function will output a Matrix x.

**Usage/Example:**

        lufactorization(Matrix A, Matrix b);
        A = { {2, 4, -2}, {4, 9, -3}, {-2, -3, 7} }
        b = { { 3 }, { 7 }, { 5 } }
 
Output from the lines above:

        x = { {4.75}, {-.75}, {1.75} }
  
**Implementation/Code:** The following is the code for lufactorization()

	Matrix lufactorization(Matrix A, Matrix b) {
		int row = A.getRow();
		int col = A.getCol();
		Matrix E(row, col, 0);
		E.setVecUnit(0, 0, 1);
		Matrix Zero = E;
		Matrix L(row);
		Matrix I(row);

		for (int i = 0; i < A.getCol() - 1; i++) {
			Matrix temp = rowSwapper(A, i);
			L = temp * L;
			A = temp * A;

			for (int c = i; c < col - 1; c++) {
				for (int r = i + 1; r < row; r++) {
					E.setVecUnit(r, c, -(A.getVecUnit(r, c) / A.getVecUnit(c, c)));
					E.setVecUnit(r, r, 1);
				}
				A = E * A;
				L = E * L;
				E = Zero;
				E.setVecUnit(i + 1, i + 1, 1);
				Zero = E;
			}
		}

		Matrix C = L * b;
		Matrix x(b.getRow(), 1, 0);
		int r = x.getRow();
		for (int i = r - 1; i >= 0; i--) {
			double left = C.getVecUnit(i, 0);
			for (int j = i; j < r; j++) {
				left -= (A.getVecUnit(i, j) * x.getVecUnit(j, 0));
			}
			x.setVecUnit(i, 0, (left / A.getVecUnit(i, i)));
		}
		return x;
	}

**Link for rowSwapper():**
	[rowSwapper()](rowSwapper.md)
