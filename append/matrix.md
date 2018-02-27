## MATRIX CLASS

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This class defines a matrix and provides functions that allow you to multiply and add matrices.
  
**Implementation/Code:** 

	class Matrix {
	public:

		//Give size and what to fill it with
		Matrix(int r, int c, int init) {
			vector<double> vec1(c, init);
			vector<vector<double>> vec2(r, vec1);
			vec = vec2;
		}

		//initiate identity matrix
		Matrix(int n) {
			vector<double> vec1(n, 0);
			vector<vector<double>> vec2(n, vec1);
			for (int i = 0; i < n; i++) {
				vec2[i][i] = 1;
			}
			vec = vec2;
		}
		
		//turn vector into matrix
		Matrix(vector<double> vec) {
			vector<vector<double>> matrix;
			for (int i = 0; i < vec.size(); i++) {
				vector<double> temp;
				temp.push_back(vec[i]);
				matrix.push_back(temp);
			}
			this->vec = matrix;
		}
		
		//initialize matrix when given vector of vector of double
		Matrix(vector<vector<double>> vec) {
			this->vec = vec;
		}
		
		//create copy of matrix
		Matrix(const Matrix &m) {
			this->vec = m.vec;
		}
		
		//create matrix of matrices
		Matrix(vector<vector<Matrix>> matrix, int n) {
			vector<double> col(matrix.size() * n, 0);
			vector <vector<double>> row(matrix.size() * n, col);
			for (int i = 0; i < matrix.size(); i++) {
				for (int j = 0; j < matrix.size(); j++) {
					Matrix temp = matrix[i][j];
					for (int k = 0; k < n; k++) {
						for (int l = 0; l < n; l++) {
							row[i*n + k][j*n + l] = temp.vec[k][l];
						}
					}
				}
			}
			vec = row;
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

		Matrix operator-(const Matrix &b) {
			Matrix matrix(*this);
			for (int i = 0; i < matrix.vec.size(); i++) {
				for (int j = 0; j < matrix.vec[0].size(); j++) {
					matrix.vec[i][j] -= b.vec[i][j];
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

		Matrix operator*(const vector<double> &b) {
			Matrix matrix(this->vec.size(), this->vec[0].size(), 0);
			for (int i = 0; i < this->vec.size(); i++) {
				double total = 0;
				for (int j = 0; j < this->vec[0].size(); j++) {
					matrix.vec[i][j] = this->vec[i][j] * b[i];
				}
			}
		}

		vector<double> getVector() {
			vector<double> temp;
			for (int i = 0; i < this->vec.size(); i++) {
				temp.push_back(this->vec[i][0]);
			}
			return temp;
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

		Matrix trid(int a, int b, double h, int n) {
			Matrix A(n, n, 0);
			for (int i = 0; i < n; i++) {
				A.vec[i][i] = (-2 / pow(h, 2));
				A.vec[i][i + 1] = 1 / pow(h, 2);
				A.vec[i + 1][i] = 1 / pow(h, 2);
			}
			return A;
		}

		void normalize(double norm) {
			for (int i = 0; i < this->vec.size(); i++) {
				this->vec[i][0] *= (1 / norm);
			}
		}

		Matrix transpose() {
			Matrix m(1, this->vec.size(), 0);
			for (int i = 0; i < this->vec.size(); i++) {
				m.vec[0][i] = this->vec[i][0];
			}
			return m;
		}

	private:
		vector<vector<double>> vec;
	};
