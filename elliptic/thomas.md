## THOMAS ALGORITHM

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will use the Thomas Algorithm to compute the solution to an elliptic ODE.

**Input:**

  int n = size of mesh
  
  Input related to the ODE will be initiated using initede()
	
	
**Output:** The function will output a vector<double> of U at every mesh point

**Usage/Example:**

	thomas(int n)
  n = 4;
  f = x;
  a = 1;
  b = 2;
  ua = 1;
  ub = 2;

Output from the lines above:

	{.0798611, -0.762153, -1.66406}
    
**Implementation/Code:** The following is the code for thomas()

  vector<double> thomas(int n) {
	  initEDE(n);
	  for (int i = 1; i < n - 1; i++) {
		  T.setVecUnit(i, i, (T.getVecUnit(i, i) - T.getVecUnit(i - 1, i) * (T.getVecUnit(i, i - 1) / T.getVecUnit(i - 1, i - 1))));
		  rhs[i] = rhs[i] - (rhs[i - 1] * (T.getVecUnit(i, i - 1) / T.getVecUnit(i, i)));
	  }
	  vector<double> ans;
	  for (int i = 0; i < n - 1; i++) {
		  ans.push_back(0);
	  }
	  ans[n - 2] = rhs[n - 2] / T.getVecUnit(n - 2, n - 2);
	  for (int i = n - 3; i >= 0; i--) {
		  ans[i] = (rhs[i] - (ans[i + 1] * T.getVecUnit(i, i + 1))) / T.getVecUnit(i, i);
	  }
	  return ans;
  }
