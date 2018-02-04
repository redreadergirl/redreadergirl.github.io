## 1 NORM OF DIFFERENCE IN VECTORS

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the 1 norm of the difference between 2 vectors

**Input:** 
        
	vector<double> A = first vector
	vector<double> B = second vector

**Output:** The function will output the 1 norm of A - B

**Usage/Example:**

	difonorm(vector<double> A, vector<double> B)
	A = {6, 5, 4}
	B = {5, 3, 1}
       
Output from the lines above:

	6
  
**Implementation/Code:** The following is the code for difonorm()

	double difonorm(vector<double> A, vector<double> B) {
		vector<double> E;
		for (int i = 0; i < A.size(); i++) {
			E.push_back(A[i] - B[i]);
		}
		return onorm(E);
	}
