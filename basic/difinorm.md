## INFINITY NORM OF DIFFERENCE IN VECTORS

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the infinity norm of the difference between 2 vectors

**Input:** 
        
	vector<double> A = first vector
	vector<double> B = second vector

**Output:** The function will output the infinity norm of A - B

**Usage/Example:**

	difinorm(vector<double> A, vector<double> B)
	A = {6, 5, 4}
	B = {5, 3, 1}
       
Output from the lines above:

        3
  
**Implementation/Code:** The following is the code for difinorm()

	double difinorm(vector<double> A, vector<double> B) {
		vector<double> E;
		for (int i = 0; i < A.size(); i++) {
			E.push_back(A[i] - B[i]);
		}
		return inorm(E);
	}
