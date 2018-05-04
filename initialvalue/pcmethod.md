## PREDICTOR CORRECTOR METHOD

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to an initial value problem using a predictor corrector method. A fourth order Adams-Bashforth will be used as the predictor and a third order Adams-Moulton will be used as the corrector.

**Input:**

	double u0 = initial u value;
	double t0 = initial t value;
	double time = time you want to solve for;
  
  	The user will provide a function to solve f(u, t)
  
**Output:** The function will output the value of u evaluated at time as a double

**Usage/Example:**

	predictorCorrector(double u0, double t0, double time)
  	u0 = .1
  	t0 = 0
  	time = 1
  	f(u, t) = -u

Output from the lines above:

	0.0360
    
**Implementation/Code:** The following is the code for predictorCorrector()

    double evalF(double t, double y) {
	    return -1 * y;
    }

    double predictorCorrector(double u, double t, double time) {
	double k = .001;
	double eval0 = evalF(t, u);
	double ustar = u + (k * eval0);
	double evalstar = evalF(t, ustar);
	u += (k / 2) * (eval0 + evalstar);
	t += k;
	double eval1 = evalF(t, u);
	ustar = u + ((k / 2) * ((-1 * eval0) + (3 * eval1)));
	evalstar = evalF(t, ustar);
	t += k;
	u += (k / 12) * ((-1 * eval0) + (8 * eval1) + (5 * evalstar));
	double eval2 = evalF(t, u);
	ustar = u + ((k / 12) * ((5 * eval0) + (-16 * eval1) + (23 * eval2)));
	evalstar = evalF(t, ustar);
	t += k;
	u += (k / 24) * (eval0 + (-5 * eval1) + (19 * eval2) + (9 * evalstar));
	double eval3 = evalF(t, u);
	ustar = u + ((k / 24) * (-9 * eval0) + (37 * eval1) + (-59 * eval2) + (55 * eval3));
	while(t < time) {
		evalstar = evalF(t, u);
		t += k;
		u += (k / 720) * ((-19 * eval0) + (106 * eval1) + (-264 * eval2) + (646 * eval3) + (251 * evalstar));
		eval0 = eval1;
		eval1 = eval2;
		eval2 = eval3;
		eval3 = evalstar;
	}
	return u;
    }
