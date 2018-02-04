## 2 NORM OF DIFFERENCE IN VECTORS

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the 2 norm of the difference between 2 vectors.

**Input:** 
        
        vector<double> A = first vector
        vector<double> B = second vector

**Output:** The function will output the norm A - B.

**Usage/Example:**

        diftnorm(vector<double> A, vector<double> B)
        A = {6, 5, 4}
        B = {5, 3, 1}
       
Output from the lines above:

        3.742
  
**Implementation/Code:** The following is the code for diftnorm()

    double diftnorm(vector<double> A, vector<double> B) {
	    vector<double> E;
	    for (int i = 0; i < A.size(); i++) {
	      E.push_back(A[i] - B[i]);
      }
      return tnorm(E);
    }
