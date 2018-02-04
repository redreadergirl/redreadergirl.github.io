## INFINITY NORM

Author: Claire Romney

Language: C++

Description/Purpose: This function will compute the infinity norm of a vector

Input:

	vector<double> A = vector
	
Output: The function will output the infinity norm of vector A.

Usage/Example:

	inorm(vector<double> A)
	A = {1, 2, 3}

Output from the lines above:

	3
    
Implementation/Code: The following is the code for inorm()

	double inorm(vector<double> E) {
		double norm = 0;
		for (int i = 0; i < E.size(); i++) {
			if (abs(E[i]) > norm) {
				norm = abs(E[i]);
			}
		}
		return norm;
	}
