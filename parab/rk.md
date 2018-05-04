## RUNGE KUTTA METHOD

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to the heat equation using the runge kutta method.

**Input:**

	double k = change in t
  double h =  change in x
  int n = size of mesh
  vector<double> f = initial values of x's
  int finalt = time you are solving for
  int alpha = coefficient in front of uxx
  
**Output:** The function will output a column vector of solutions at time finalt

**Usage/Example:**

	rungeKuttaParab(.01, 1, 11, {0, .1, .2, .3, .4, .5, .6, .7, .8, .9, 1}, 1, 1)

Output from the lines above:

	{0, .1, .2, .3, .4, .5, .603, .719, .899, 1.347, 2.718}
    
**Implementation/Code:** The following is the code for rungeKuttaParab()

	   vector<double> rungeKuttaParab(double k, double h, int n, vector<double> u, int finalt, int alpha) {
	    int numOfSteps = finalt / k;
	    double step = (alpha * k) / (h * h);
	    vector<double> y1(n);
	    vector<double> y2(n);
	    vector<double> y3(n);
	    vector<double> y4(n);
	    for (int i = 0; i < numOfSteps; i++) {
	    	y1 = u;

	    	y2[0] = u[0] + ((step / 2) * y1[0]);
		    for (int j = 1; j < n - 1; j++) {
			    y2[j] = u[j] + ((step / 2) * (y1[j - 1] - (2 * y1[j]) + y1[j + 1]));
		    }
    		y2[n - 1] = u[n - 1] + ((step / 2) * y1[n - 1]);

		    y3[0] = u[0] + ((step / 2) * y2[0]);
		    for (int j = 1; j < n - 1; j++) {
			    y3[j] = u[j] + ((step / 2) * (y2[j - 1] - (2 * y2[j]) + y2[j + 1]));
	    	}
		    y3[n - 1] = u[n - 1] + ((step / 2) * y2[n - 1]);

		    y4[0] = u[0] + ((step) * y3[0]);
		    for (int j = 1; j < n - 1; j++) {
			    y4[j] = u[j] + ((step) * (y3[j - 1] - (2 * y3[j]) + y3[j + 1]));
	    	}
		    y4[n - 1] = u[n - 1] + ((step) * y3[n - 1]);
		
		    u[0] = u[0] + ((step / 6) * (y1[0] + (2 * y2[0]) + (2 * y3[0]) + y4[0]));
		    for (int j = 1; j < n - 1; j++) {
			    u[j] = u[j] + ((step / 6) * ((y1[j - 1] - (2 * y1[j]) + y1[j + 1]) + (2 * (y2[j - 1] - (2 * y2[j]) + y2[j + 1])) + (2 * (y3[j - 1] - (2 * y3[j]) + y3[j + 1])) + (y4[j - 1] - (2 * y4[j]) + y4[j + 1])));
	    	}
		    u[n-1] = u[n-1] + ((step / 6) * (y1[n-1] + (2 * y2[n-1]) + (2 * y3[n-1]) + y4[n-1]));
	    }
	    return u;
    }
