## FOURTH ORDER RUNGE KUTTA METHOD

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to an initial value problem using the runge kutta method of order 4.

**Input:**

	double u0 = initial u value;
	double t0 = initial t value;
	double time = time you want to solve for;
  
  	The user will provide a function to solve f(u, t)
  
**Output:** The function will output the value of u evaluated at time as a double

**Usage/Example:**

	fourRungeKutta(double u0, double t0, double time)
  	u0 = .1
  	t0 = 0
  	time = 1
  	f(u, t) = -u

Output from the lines above:

	0.0363
    
**Implementation/Code:** The following is the code for fourRungeKutta()

    double evalF(double t, double y) {
	    return -1 * y;
    }

    double fourRungeKutta(double u0, double t0, double time) {
	    double k = .0125;
	    double u = u0;
	    double t = t0;
	    while (t < time) {
		    double y1 = u;
		    double ev1 = evalF(t, y1);
		    double y2 = u + (.5 * k * ev1);
		    double ev2 = evalF(t + k / 2, y2);
		    double y3 = u + (k * .5 * ev2);
		    double ev3 = evalF(t + k / 2, y3);
		    double y4 = u + (k * ev3);
		    u += (k / 6) * (ev1 + (2 * ev2) + (2 * ev3) + evalF(t, y4));
		    t += k;
	    }
	    return u;
    }
