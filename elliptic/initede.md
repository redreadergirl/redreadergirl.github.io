## INITIATE INPUT FOR ELLIPTIC ODE

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will initiate the input for an elliptic ordinary differential equation.

**Input:**

	int n = size of mesh
	string f = f(x) *user will provide a function, fillF(), which will compute f(x) for all values in mesh
	double a = lower bound
	double b = upper bound
	double ua = u evaluated at a
	double ub = u evaluated at b
	
**Output:** The function will create a tridiagonal coefficient system.

	Matrix T = Tridiagonal Coefficient Matrix
	vector<double> rhs = Right Hand Side (b, in Ax = b)

**Usage/Example:**

	initede(int n)
	n = 4;
	f = x;
	a = 1;
	b = 2;
	ua = 1;
	ub = 2;

Output from the lines above:

	No output. Function will define Matrix T and vector<double> rhs
    
**Implementation/Code:** The following is the code for initede()

	void initEDE(int n) {
	  string f;
	  double a, b, ua, ub;
	  Matrix temp(n - 1, n - 1, 0);
	  T = temp;
	
	  cout << "f(x) = ";
	  cin >> f;
	  cout << "a = ";
	  cin >> a;
	  cout << "b = ";
	  cin >> b;
	  cout << "ua = ";
	  cin >> ua;
	  cout << "ub = ";
	  cin >> ub;
	
	  for (int i = 0; i < n - 2; i++) {
		  T.setVecUnit(i, i, -2);
		  T.setVecUnit(i, i + 1, 1);
		  T.setVecUnit(i + 1, i, 1);
	  }
	  T.setVecUnit(n - 2, n - 2, -2);
	  double h = (b - a) / n;
	  vector<double> x;
	  for (int i = 0; i < n + 1; i++) {
		  x.push_back(a + (i * h));
	  }

	  rhs = fillF(f, h, n, x);

	  rhs[0] -= ua;
	  rhs[n - 2] -= ub;
	}
