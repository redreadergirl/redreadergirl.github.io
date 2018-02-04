## 2 NORM

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the 2 norm of a vector

**Input:**

	vector<double> A = vector
	
**Output:** The function will output the 2 norm of vector A.

**Usage/Example:**

	tnorm(vector<double> A)
	A = {1, 2, 3}

**Output from the lines above:**

	3.742
    
**Implementation/Code:** The following is the code for tnorm()

	double tnorm(vector<double> E) {
		double norm = 0;
		for (int i = 0; i < E.size(); i++) {
			norm += pow(E[i], 2);
		}
		return sqrt(norm);
	}
