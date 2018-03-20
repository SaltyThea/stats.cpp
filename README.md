# stats.cpp
Not fully functional
//stats.cpp

#include "stats.h"
#include <cassert> //provides asserts

using namespace CISP430_A1;

	//statistician( );
	//Postcondition: The object has been initialized, and is ready to accept
	//a sequence of numbers. Various statistics will be calculated about the
	//sequence.
	statistician::statistician() { 
		count = 0;		//By default, every private variables will be initialized to 0
		total = 0;		//to start each time a class is created..
		tiniest = 0;
		largest = 0;
	}

	//void next(double r)
	//The number r has been given to the statistician as the next number in
	//its sequence of numbers.
	void statistician::next(double r) {
		total += r; //Add up each sequence to total, given by user's input

		if (count == 0) { //starting point, set new values to tiniest and largest
			count++; //Starting sequence, 
			tiniest = r; //Sets the smallest input
			largest = r; //Sets the largest input
			return;
		}

		count++; //keeps track the # number of times this function is called

		if (r > largest){ //If temp greater than current largest, set new largest value
			largest = r;
		}
		if (r < tiniest){ //If r is less than tiniest, set new lowest value to tiniest
			tiniest = r; 
		}
	}

	//void reset( );
	//Postcondition: The statistician has been cleared, as if no numbers had
	//yet been given to it.
	void statistician::reset() {
		count = 0;		//Resets every value in object
		total = 0;		//as requested by user
		tiniest = 0;
		largest = 0;
	}

	//double mean( ) const
	//Precondition: length( ) > 0
	//Postcondition: The return value is the arithmetic mean (i.e., the
	//average of all the numbers in the statistician's sequence).
	double statistician::mean() const {
		assert(length() > 0); // If count > 0, execute statements
		double avg;		//Initialized as needed to return a double data type
		avg = total / count;
		return avg;
	}

	//double minimum() const
	//Precondition: length( ) > 0
	//Postcondition: The return value is the tiniest number in the
	//statistician's sequence.
	double statistician::minimum() const {
		assert(length() > 0); //If count > 0, return smallest value
		return tiniest;
	}

	//double maximum( ) const
	//Precondition: length( ) > 0
	//Postcondition: The return value is the largest number in the
	//statistician's sequence.
	double statistician::maximum() const {
		assert(length() > 0); //if count > 0, return largest value
		return largest;
	}

	//statistician operator +(const statistician& s1, const statistician& s2)
	//Postcondition: The statistician that is returned contains all the
	//numbers of the sequences of s1 and s2.
	statistician CISP430_A1::operator+(const statistician & s1, const statistician & s2)
	{
		//Declared a third object, add
		statistician add;

		//All values will be stored to add..
		add.count = s1.count + s2.count;
		add.total = s1.total + s2.total;
		add.tiniest = s1.tiniest + s2.tiniest;
		add.largest = s1.largest + s2.largest;
		return add; //return values to third object, s3
	}

	//statistician operator *(double scale, const statistician& s)
	//Postcondition: The statistician that is returned contains the same
	//numbers that s does, but each number has been multiplied by the
	//scale number.
	statistician CISP430_A1::operator*(double scale, const statistician & s)
	{
		statistician mult(s);//New stat object with same values of stat s;

		//Multiply all values to mult by scale, given by user's input
		mult.count *= scale;
		mult.total *= scale;
		mult.tiniest *= scale;
		mult.largest *= scale;
		return mult; //Retun new values to third object, s3
	}

	//bool operator ==(const statistician& s1, const statistician& s2)
	//Postcondition: The return value is true if s1 and s2 have the zero
	//length. Also, if the length is greater than zero, then s1 and s2 must
	//have the same length, the same  mean, the same minimum, 
	//the same maximum, and the same sum.
	bool CISP430_A1::operator==(const statistician & s1, const statistician & s2)
	{
		return
			((s1.length() > 0) && (s2.length() > 0) //Ff length > 0,
				&&(s1.length() == s2.length())		//then everything else
				&& (s1.mean() == s2.mean())			
				&& (s1.sum() == s2.sum())			//must be the same,
				&& (s1.minimum() == s2.minimum())	
				&& (s1.maximum() == s2.maximum())); //in order to return true, else false...
	}
