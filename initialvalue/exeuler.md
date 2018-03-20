## EXPLICIT EULERS METHOD

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the solution to an initial value problem using the explicit eulers method.

**Input:**

  	double y0 = initial y value;
  	double t0 = initial t value;
  	double time = time you want to solve for;
  
  The user will provide a function to solve f(t, y);
  
**Output:** The function will output the function evaluated at time as a double

**Usage/Example:**

	explicitEulers(double y0, double t0, double time)
  	y0 = 1;
  	t0 = 0;
  	time = 4;
  	f(t, y) = y;

Output from the lines above:

	53.2611
    
**Implementation/Code:** The following is the code for explicitEulers()

  	double explicitEulers(double y0, double t0, double time) {
	  double k = .0125;
	  double y = y0;
	  double t = t0;
	  while (t < time) {
		  double u = evalF(t, y);
		  y += (k * u);
	  	t += k;
	  }
	  return y;
  	}
