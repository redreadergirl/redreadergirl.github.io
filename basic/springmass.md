## SPRING MASS SYSTEMS EQUATION

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the analytic solution at any time for a spring mass system.

**Input:** 

     m = constant
     c = constant
     k = constant
     ft = f(t)
     t = time
     y0 = initial condition of y(0)
     v0 = initial condition of y'(0)

**Output:** The function outputs the value of y at the given time t.

**Usage/Example:**

        springmass(1, 5, 6, 2, 0, 2, -1)
       
Output from the lines above:

        0.0841419
  
**Implementation/Code:** The following is the code for springmass()

    double springmass(double m, double c, double k, int t, int ft, double y0, double v0) {
	double yone;
	double y2;
	double yoneprime;
	double y2prime;
	double yp;
	double ypprime;
	double ysqrt = ((c * c) - (4 * m * k));
	double u1;
	double u2;
	double wronskian; (yone * y2prime) - (y2 * yoneprime);

	double temp = t;
	t = 0;
	if (ysqrt < 0) {
		ysqrt *= -1;
		double squarert = sqrt(ysqrt) / (2 * m);
		yone = (exp(((-1 * c) / (2 * m))*t) * cos(squarert * t));
		y2 = (exp(((-1 * c) / (2 * m))*t) * sin(squarert * t));
		double ex = ((-1 * c) / (2 * m));

		yoneprime = (exp(((-1 * c) / (2 * m))*t) * (-1) * squarert *sin(squarert * t)) + (((-1 * c) / (2 * m))) * (exp(((-1 * c) / (2 * m))*t) * cos(squarert * t));
		y2prime = (exp(((-1 * c) / (2 * m))*t) * squarert * cos(squarert * t)) + (((-1 * c) / (2 * m))) * (exp(((-1 * c) / (2 * m))*t) * sin(squarert * t));

		u1 = ((squarert / ex) * exp(-ex * t) * (sin(squarert * t) + ((1 / ex) * cos(squarert * t)))) / (1 + (squarert / (ex * ex)));
		u2 = ((-squarert / ex) * exp(-ex * t) * (cos(squarert * t) + ((1 / ex) * sin(squarert * t)))) / (1 - (squarert / (ex * ex)));

	}
	else if (ysqrt == 0) {
		yone = exp(((-1 * c) / (2 * m)) * t);
		y2 = t * yone;
		double ex = ((-1 * c) / (2 * m));

		yoneprime = ((-1 * c) / (2 * m)) * exp(((-1 * c) / (2 * m)) * t);
		y2prime = exp(((-1 * c) / (2 * m)) * t) + (t * yoneprime);

		u1 = (-1 * ft) * (((1 / -ex) * t * exp(-ex * t)) - ((1 / (ex * ex)) * exp(-ex * t)));
		u2 = (ft / -ex) * exp(-ex * t);
	}
	else {
		double test = ((-c) + sqrt(ysqrt)) / (2 * m);
		yone = exp(test * t);
		y2 = exp((((-1 * c) - sqrt(ysqrt)) / (2 * m)) * t);
		double ex1 = (((-1 * c) + sqrt(ysqrt)) / (2 * m));
		double ex2 = (((-1 * c) - sqrt(ysqrt)) / (2 * m));

		yoneprime = ex1 * yone;
		y2prime = ex2 * y2;

		wronskian = (yone * y2prime) - (y2 * yoneprime);

		u1 = -1 * (ft / wronskian) * ex2 * y2;
		u2 = (ft / wronskian) * ex1 * yone;
	}
	if (ft == 0) {
		u1 = 0;
		u2 = 0;
	}

	yp = (u1 * yone) + (u2 * y2);
	double u1prime = -1 * (y2 * ft) / wronskian;
	double u2prime = (yone * ft) / wronskian;
	ypprime = (u1 * yoneprime) + (u1prime * yone) + (u2 * y2prime) + (u2prime * y2);

	double yp0 = yp;
	double wron = yone * y2prime - (y2 * yoneprime);
	double c1 = ((y2prime / wron) * (y0 - yp0)) + (-1 * (y2 / wron) * (v0 - ypprime));
	double c2 = (-1 * (yoneprime / wron) * (y0 - yp0)) + ((yone / wron) * (v0 - ypprime));
	t = temp;

	if (ysqrt < 0) {
		ysqrt *= -1;
		double squarert = sqrt(ysqrt) / (2 * m);
		yone = (exp(((-1 * c) / (2 * m))*t) * cos(squarert * t));
		y2 = (exp(((-1 * c) / (2 * m))*t) * sin(squarert * t));
		double ex = ((-1 * c) / (2 * m));

		yoneprime = (exp(((-1 * c) / (2 * m))*t) * (-1) * squarert *sin(squarert * t)) + (((-1 * c) / (2 * m))) * (exp(((-1 * c) / (2 * m))*t) * cos(squarert * t));
		y2prime = (exp(((-1 * c) / (2 * m))*t) * squarert * cos(squarert * t)) + (((-1 * c) / (2 * m))) * (exp(((-1 * c) / (2 * m))*t) * sin(squarert * t));

		u1 = ((squarert / ex) * exp(-ex * t) * (sin(squarert * t) + ((1 / ex) * cos(squarert * t)))) / (1 + (squarert / (ex * ex)));
		u2 = ((-squarert / ex) * exp(-ex * t) * (cos(squarert * t) + ((1 / ex) * sin(squarert * t)))) / (1 - (squarert / (ex * ex)));

	}
	else if (ysqrt == 0) {
		yone = exp(((-1 * c) / (2 * m)) * t);
		y2 = t * yone;
		double ex = ((-1 * c) / (2 * m));

		yoneprime = ((-1 * c) / (2 * m)) * exp(((-1 * c) / (2 * m)) * t);
		y2prime = exp(((-1 * c) / (2 * m)) * t) + (t * yoneprime);

		u1 = (-1 * ft) * (((1 / -ex) * t * exp(-ex * t)) - ((1 / (ex * ex)) * exp(-ex * t)));
		u2 = (ft / -ex) * exp(-ex * t);
	}
	else {
		double test = ((-c) + sqrt(ysqrt)) / (2 * m);
		yone = exp(test * t);
		y2 = exp((((-1 * c) - sqrt(ysqrt)) / (2 * m)) * t);
		double ex1 = (((-1 * c) + sqrt(ysqrt)) / (2 * m));
		double ex2 = (((-1 * c) - sqrt(ysqrt)) / (2 * m));

		yoneprime = ex1 * yone;
		y2prime = ex2 * y2;

		wronskian = (yone * y2prime) - (y2 * yoneprime);

		u1 = -1 * (ft / wronskian) * ex2 * y2;
		u2 = (ft / wronskian) * ex1 * yone;
	}
	if (ft == 0) {
		u1 = 0;
		u2 = 0;
	}

	double yt = (c1 * yone) + (c2 * y2) + yp;
	return yt;
    }
