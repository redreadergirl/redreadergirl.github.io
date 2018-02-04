## 1 NORM

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the 1 norm of a vector

**Input:**

	vector<double> A = vector
	
**Output:** The function will output the 1 norm of vector A.

**Usage/Example:**

	onorm(vector<double> A)
	A = {1, 2, 3}

Output from the lines above:

	6
    
**Implementation/Code:** The following is the code for onorm()

	double onorm(vector<double> E) {
		double norm = 0;
		for (int i = 0; i < E.size(); i++) {
			norm += abs(E[i]);
		}
		return norm;
	}
