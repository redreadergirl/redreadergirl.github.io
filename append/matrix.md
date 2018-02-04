## MATRIX CLASS

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This class defines a matrix and provides functions that allow you to multiply and add matrices.
  
**Implementation/Code:** 

  	class Matrix {
  	public:

	  Matrix(int r, int c, int init) {
		  vector<double> vec1(c, init);
  		vector<vector<double>> vec2(r, vec1);
	  	vec = vec2;
	  }

  	  Matrix(vector<vector<double>> vec) {
	  	this->vec = vec;
	  }

	  Matrix(const Matrix &m) {
	  	this->vec = m.vec;
	  }
	  
	  Matrix(int n) {
		vector<double> vec1(n, 0);
		vector<vector<double>> vec2(n, vec1);
		for (int i = 0; i < n; i++) {
			vec2[i][i] = 1;
		}
		vec = vec2;
	  }
	
	  Matrix operator+(const Matrix &b) {
		  Matrix matrix(*this);
		  for (int i = 0; i < matrix.vec.size(); i++) {
		  	for (int j = 0; j < matrix.vec[0].size(); j++) {
		  		matrix.vec[i][j] += b.vec[i][j];
			  }
	  	}
		  return matrix;
	  }

	  Matrix operator*(const Matrix &b) {
		  Matrix matrix(this->vec.size(), b.vec[0].size(), 0);
		  for (int i = 0; i < this->vec.size(); i++) {
			  for (int j = 0; j < b.vec[0].size(); j++) {
				  double total = 0;
				  for (int k = 0; k < b.vec.size(); k++) {
					  total += (this->vec[i][k] * b.vec[k][j]);
			  	}
				  matrix.vec[i][j] = total;
		  	}
		  }
		  return matrix;
	  }

	  int getRow() {
		  return this->vec.size();
	  }

	  int getCol() {
		  return this->vec[0].size();
	  }

  	  void setVecUnit(int r, int c, double numb) {
	  	this->vec[r][c] = numb;
	  }

	  double getVecUnit(int r, int c) {
		  return this->vec[r][c];
	  }
	  
	  Matrix swapRow(int row1, int row2) {
		Matrix E(this->getCol());
		for (int i = 0; i < this->getCol(); i++) {
			swap(this->vec[row1][i], this->vec[row2][i]);
		}
		E.vec[row1][row1] = 0;
		E.vec[row2][row2] = 0;
		E.vec[row1][row2] = 1;
		E.vec[row2][row1] = 1;
		return E;
	  }

  	private:
	  vector<vector<double>> vec;
  	};
