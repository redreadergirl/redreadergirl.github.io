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

	 for (int i = 0; i < A.getCol(); i++) {
	 	int max = 0;
	 	int maxRow = 0;
	 	for (int j = i; j < A.getRow(); j++) {
	 		if (A.getVecUnit(j, i) > max) {
	 			max = A.getVecUnit(j, i);
	 			maxRow = j;
			}
		}
		if (maxRow != i) {
			L = (A.swapRow(i, maxRow)) * L;
		}
	 }
	 if (A.getVecUnit(A.getRow() - 1, A.getCol() - 1) == 0) {
	 	bool swapped = false;
		int i = 0;
		while (swapped == false || i == A.getRow() - 1) {
			if (A.getVecUnit(A.getRow() - 1, i) != 0) {
				if (A.getVecUnit(i, A.getCol() - 1) != 0) {
					L = A.swapRow(A.getRow() - 1, i) * L;
					swapped = true;
				}
			}
			i++;
		}
	 }

	 for (int c = 0; c < col - 1; c++) {
		for (int r = 1; r < row; r++) {
			E.setVecUnit(r, c, -(A.getVecUnit(r, c) / A.getVecUnit(c, c)));
			E.setVecUnit(r, r, 1);
		}
		A = E * A;
		L = E * L;
		E = Zero;
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
				max = A.getVecUnit(j, i);
				maxRow = j;
			}
		}
		if (maxRow != i) {
			L = (A.swapRow(i, maxRow)) * L;
		}
	}
	if (A.getVecUnit(A.getRow() - 1, A.getCol() - 1) == 0) {
		bool swapped = false;
		int i = 0;
		while (swapped == false || i == A.getRow() - 1) {
			if (A.getVecUnit(A.getRow() - 1, i) != 0) {
				if (A.getVecUnit(i, A.getCol() - 1) != 0) {
					L = A.swapRow(A.getRow() - 1, i) * L;
					swapped = true;
				}
			}
			i++;
		}
	}
