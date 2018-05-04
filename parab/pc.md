## PREDICTOR CORRECTOR METHOD

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to the heat equation using the predictor corrector method.

**Input:**

	double k = change in t
  double h =  change in x
  int n = size of mesh
  vector<double> f = initial values of x's
  int finalt = time you are solving for
  int alpha = coefficient in front of uxx
  
**Output:** The function will output a column vector as a Matrix of solutions at time finalt

**Usage/Example:**

	predCorParab(.01, 1, 11, {0, .1, .2, .3, .4, .5, .6, .7, .8, .9, 1}, 1, 1)

Output from the lines above:

	{0, 8.5e43, -9.9e43, 8.3e43, -6e43, 3.8e43, -2.3e43, 1.1e43, -4.9e42, 1.5e42, 2672.3}
    
**Implementation/Code:** The following is the code for preCorParab()

	  vector<double> predCorParab(double k, double h, int n, vector<double> f, int finalt, int alpha) {
	    int numOfSteps = finalt / k;
	    double step = (alpha * k) / (h * h);
	    vector<double> u0(n);
   	u0 = f;

	    numOfSteps--;
	    vector<double> u1(n);
	    u1[0] = u0[0] + (step * u0[0]);
	    for (int i = 1; i < n - 1; i++) {
	    	u1[i] = u0[i] + (step * (u0[i - 1] - (2 * u0[i]) + u0[i + 1]));
	    }
	    u1[n - 1] = u0[n - 1] + (step * u0[n-1]);
	    u1[0] = u0[0] + ((step / 2)* (u0[0] + u1[0]));
	    for (int i = 1; i < n - 1; i++) {
		    u1[i] = u0[i] + ((step / 2) * (u0[i - 1] - (2 * u0[i]) + u0[i + 1] + u1[i - 1] - (2 * u1[i]) + u1[i + 1]));
    	}
	    u1[n - 1] = u0[n - 1] + ((step / 2) * (u0[n - 1] + u1[n - 1]));

	    numOfSteps--;
	    vector<double> u2(n);
	    u2[0] = u1[0] + ((step / 2) * ((-1 * u0[0]) + (3 * u1[0])));
	    for (int i = 1; i < n - 1; i++) {
		    u2[i] = u1[i] + ((step / 2) * ((-1 * (u0[i - 1] - (2 * u0[i]) + u0[i + 1])) + (3 * (u1[i - 1] - (2 * u1[i]) + u1[i + 1]))));
    	}
	    u2[n - 1] = u1[n - 1] + ((step / 2) * ((-1 * u0[n - 1]) + (3 * u1[n - 1])));
	    u2[0] = u1[0] + ((step / 12) * ((-1 * u0[0]) + (8 * u1[0]) + (5 * u2[0])));
	    for (int i = 1; i < n - 1; i++) {
		    u2[i] = u1[i] + ((step / 12) * ((-1 * (u0[i - 1] - (2 * u0[i]) + u0[i + 1])) + (8 * (u1[i - 1] - (2 * u1[i]) + u1[i + 1])) + (5 * (u2[i - 1] - (2 * u2[i]) + u2[i + 1]))));
    	}
	    u2[n-1] = u1[n-1] + ((step / 12) * ((-1 * u0[n-1]) + (8 * u1[n-1]) + (5 * u2[n-1])));

	    numOfSteps--;
	    vector<double> u3(n);
	    u3[0] = u2[0] + ((step / 12) * ((5 * u0[0]) + (-16 * u1[0]) + (23 * u2[0])));
	    for (int i = 1; i < n - 1; i++) {
		    u3[i] = u2[i] + ((step / 12) * ((5 * (u0[i - 1] - (2 * u0[i]) + u0[i + 1])) + (-16 * (u1[i - 1] - (2 * u1[i]) + u1[i + 1])) + (23 * (u2[i - 1] - (2 * u2[i]) + u2[i + 1]))));
    	}
	    u3[n-1] = u2[n-1] + ((step / 12) * ((5 * u0[n-1]) + (-16 * u1[n-1]) + (23 * u2[n-1])));
	    u3[0] = u2[0] * ((step / 24) * (u0[0] + (-5 * u1[0]) + (19 * u2[0]) * (9 * u3[0])));
	    for (int i = 1; i < n - 1; i++) {
		    u3[i] = u2[i] * ((step / 24) * ((u0[i - 1] - (2 * u0[i]) + u0[i + 1]) + (-5 * (u1[i - 1] - (2 * u1[i]) + u1[i + 1])) + (19 * (u2[i - 1] - (2 * u2[i]) + u2[i + 1])) * (9 * (u3[i - 1] - (2 * u3[i]) + u3[i + 1]))));
    	}
	    u3[n-1] = u2[n-1] * ((step / 24) * (u0[n-1] + (-5 * u1[n-1]) + (19 * u2[n-1]) * (9 * u3[n-1])));

	    vector<double> u4(n);

	    for (int j = 0; j < numOfSteps; j++) {
		    u4[0] = u3[0] + ((step / 24) * (-9 * u0[0]) + (37 * u1[0]) + (-59 * u2[0]) + (55 * u3[0]));
		    for (int i = 1; i < n - 1; i++) {
		    	u4[i] = u3[i] + ((step / 24) * (-9 * (u0[i - 1] - (2 * u0[i]) + u0[i + 1])) + (37 * (u1[i - 1] - (2 * u1[i]) + u1[i + 1])) + (-59 * (u2[i - 1] - (2 * u2[i]) + u2[i + 1])) + (55 * (u3[i - 1] - (2 * u3[i]) + u3[i + 1])));
	    	}
		    u4[n-1] = u3[n-1] + ((step / 24) * (-9 * u0[n-1]) + (37 * u1[n-1]) + (-59 * u2[n-1]) + (55 * u3[n-1]));
		    u4[0] = u3[0] + ((step / 720) * ((-19 * u0[0]) + (106 * u1[0]) + (-264 * u2[0]) + (646 * u3[0]) + (251 * u4[0])));
		    for (int i = 1; i < n - 1; i++) {
		    	u4[i] = u3[i] + ((step / 720) * ((-19 * (u0[i - 1] - (2 * u0[i]) + u0[i + 1])) + (106 * (u1[i - 1] - (2 * u1[i]) + u1[i + 1])) + (-264 * (u2[i - 1] - (2 * u2[i]) + u2[i + 1])) + (646 * (u3[i - 1] - (2 * u3[i]) + u3[i + 1])) + (251 * (u4[i - 1] - (2 * u4[i]) + u4[i + 1]))));
	    	}
	    	u4[n-1] = u3[n-1] + ((step / 720) * ((-19 * u0[n-1]) + (106 * u1[n-1]) + (-264 * u2[n-1]) + (646 * u3[n-1]) + (251 * u4[n-1])));
		    u0 = u1;
		    u1 = u2;
		    u2 = u3;
		    u3 = u4;
	    }
	    return u4; 
    }
