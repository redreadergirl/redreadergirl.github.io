## ANALYTIC SOLUTION TO LOGISTIC MODEL OF POPULATION GROWTH

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the analytic solution to the logistic model of population growth P'=αP-βP^2

**Input:**

	double alpha = α
  double beta = β
	double p0 = P(0)
	double t = time you want to solve for;
  
**Output:** The function will output the value u evaluated at time t as a double

**Usage/Example:**

    logisticModel(double alpha, double beta, double p0, double t)
    alpha = .1
    beta = .0001
    p0 = 25
    t = 1

Output from the lines above:

	27.5568
    
**Implementation/Code:** The following is the code for simpleIVP()

    double logisticModel(double alpha, double beta, double p0, double t) {
	    double eat = 1;
	    double x = alpha * t;
	    double fact = 1;
	    for (int i = 1; i < 10; i++) {
		    fact *= i;
		    eat += pow(x, i) / fact;
	    }
	    double p = (alpha * p0 * eat) / (alpha - (beta * p0) + (beta * p0 * eat));
	    return p;
    }
