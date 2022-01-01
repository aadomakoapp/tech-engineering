
#include<iostream>
#include<fstream>
#include<string>
#include<iomanip>
#include<cmath>
using namespace std;
//Decalaring function prototypes
void ReadData(double bumpHeight[], double velocity[], int& size, long& k, long& c, double& m);
void CarTripDisplacement(double bumpHeight[], double velocity[], double displacement[], int size, long k, long c, double m);
double CalculateDisplacement(double bumpHeight, double velocity, long k, long c, double m);
void WriteData(double bumpHeight[], double velocity[], double displacement[], int size, long k, long c, double m);
void MassEffectAnalysis(double bumpHeight[], double velocity[], int size, long k, long c);
void VelocityEffectAnalysis(double bumpHeight[], int size, long k, long c, double m);
void PrintData(string fileName);

int main() {
	int finaloption;
	const int MAXSIZE(100);		//Declaring and initialising maximum size for arrays
	int size(7), option;		//Declaring size of input arrays and option variable for decision sructure in menu
	double yt[MAXSIZE], xt[MAXSIZE], mass, vt[MAXSIZE];		// Declaring arrays and allocating memory of maxsize
	long stiffness, damping;
	ReadData(yt, vt, size, stiffness, damping, mass);	//Calling ReadData function to input data
	CarTripDisplacement(yt, vt, xt, size, stiffness, damping, mass);		//Calling CarTripDisplacement function to populate xt array
	WriteData(yt, vt, xt, size, stiffness, damping, mass);		//Calling WriteData function to write data into file
	PrintData("vehicleDisplacements.txt");		//Printing vehilceDisplacement.txt file to the output console
	do {			//Repeat whole program from menu
		do {		//Validate user input for menu
			cout << "Enter 1 to perform mass analyis" << endl;
			cout << "Enter 2 to perform velocity analysis" << endl;
			cin >> option;
			if (option != 1 && option != 2) {		//Prompting user for valid menu inputs
				cout << "Valid entries are only 1 and 2" << endl;
				cout << "Enter a valid integer: 1 or 2 only" << endl;
				cin >> option;
			}
		} while (option != 1 && option != 2);		

		switch (option) {
		case 1: {
			cout << "Mass-Analysis option selected" << endl;
			MassEffectAnalysis(yt, vt, size, stiffness, damping);		//Calling MassEffectAnalysis function to analyse varying mass on displacement
			PrintData("massResults.txt");		//Calling PrintData function to output massResults.txt to output console
			break;	
		}
		case 2: {
			cout << "Velocity-Analysis option selected" << endl;
			VelocityEffectAnalysis(yt, size, stiffness, damping, mass);		//Calling VelocityEffectAnalysis function to analyse varying velocity on displacement
			PrintData("velocityResults.txt");		//Calling PrintData function to output velocityResults.txt to output console
			break;
		}
		}
		//Options to return to menu or exit program
		cout << "Press 0 to exit the program" << endl;
		cout << "Press any other value to re-run the program from the menu" << endl;
		cin >> finaloption;
		if (finaloption == 0) {
			cout << "Program exiting" << endl;
		}
	} while (finaloption != 0);
	
	return 0;
}



void ReadData(double bumpHeight[], double velocity[], int& size, long& k,long& c, double& m){
	//Defining ReadData function

	//Creating an input-file stream
	ifstream in;
	in.open("vehicleDetails.txt");	
	if (in.fail()) {
		cerr << "Error in opening file" << endl;
		exit(-1);
	}
	//Reading unwanted strings and needed values
	string garbage, garbage1;
	in >> garbage>>m;
	in >> garbage>>k;
	in >> garbage>>c;
	in >> garbage >> garbage1;

	//Populating bumpHeight and velocity arrays
	for (int i = 0; i < size; i++) {
		in >> bumpHeight[i] >> velocity[i];
	}	
	in.close();		//Close input file
}


double CalculateDisplacement(double bumpHeight, double velocity, long k, long c, double m){
	//Defining  CalculateDisplacement function

	//Comouting equations needed for vertical displacement
	double damping_ratio, natural_freq, forcing_freq, freq_ratio, xt, a, numerator, denominator;
	damping_ratio = 0.5 * ((double)c / (sqrt(m * k)));
	natural_freq = sqrt(k / m);
	forcing_freq = 0.2909 * velocity;
	freq_ratio = forcing_freq/ natural_freq;
	numerator = (1 + pow((2 * damping_ratio * freq_ratio), 2));
	denominator = pow((1 - pow(freq_ratio, 2)), 2) + pow((2 * damping_ratio * freq_ratio), 2);
	a = sqrt(numerator / denominator);
	xt = bumpHeight * a;
	
	return xt;
}


void CarTripDisplacement(double bumpHeight[], double velocity[], double displacement[], int size, long k, long c, double m) {
	//Defining CarTripDisplacement

	//Populating displacement array
	for (int i = 0; i < size; i++) {
		displacement[i] = CalculateDisplacement(bumpHeight[i], velocity[i], k, c, m);
	}
}
	

void WriteData(double bumpHeight[], double velocity[], double displacement[], int size, long k, long c, double m) {
	//Defining WriteData dunction
	
	//Creating output-file stream
	ofstream out;
	out.open("vehicleDisplacements.txt");
	if (out.fail()) {
		cerr << "Error in opening file" << endl;
		exit(-2);
	}
	ReadData(bumpHeight, velocity, size, k, c, m);		//Calling ReadData function to read values into an outputfile(copy and Paste)
	
	//Writing into output file
	out << "Mass = " << m << " (unit is assumed in kg)" << endl;
	out << "Stiffness = " << k << " (unit is assumed in N/m)" << endl;
	out << "Damping = " << c << " ( unit is assumed in Ns/m)" << endl;
	out << endl;
	out << left << setw(20) << "Roughness(m)" << left << setw(20) << "Velocity(km/hr)" << setw(20) << "Displacement(m)" << endl;
	for (int i = 0; i < size; i++) {
		out << left << setw(20) << bumpHeight[i] << setw(20)
			<< velocity[i] << setw(20) << displacement[i] << endl;
	}
	out.close();		//Close output file
	cout << "Information has been written into vehicleDisplacements.txt" << endl;
}

void MassEffectAnalysis(double bumpHeight[], double velocity[], int size, long k, long c) {
	//Defining MassEffectAnalysis function

	//Creating outputfile stream
	ofstream out;
	out.open("massResults.txt");
	if (out.fail()) {
		cerr << "Error in opening file" << endl;
		exit(-3);
	}

	//Prompting user for mass range values
	double startmass, finalmass, stepsize;	
	cout << "Enter start value for mass in kg" << endl;
	cin >> startmass;
	cout << "Enter final value for mass in kg" << endl;
	cin >> finalmass;
	cout << "Enter step-size for mass in kg" << endl;
	cin >> stepsize;	
	double overallmax(0);
	
	//Performing mass analysis and Writing results into output file
	out << "Analysis of varying mass on displacement for current trip"<<endl;
	out << "Stiffness = " << k << " Nm" << endl;
	out << "Damping = " << c << " Ns/m" << endl;
	out << left << setw(15) << "Mass(kg)" << setw(15) << "Displacement(m)" << endl;
	for (double m = startmass; m <= finalmass; m += stepsize) {
		double max(0);
		for (int j = 0; j < size; j++) {
			double displacement = CalculateDisplacement(bumpHeight[j], velocity[j], k, c, m);
			if (displacement > max){
				max = displacement;
		}
		}
		if (max > overallmax) {
			overallmax = max;
		}
		out << left << setw(15) << m << setw(15) << max << endl;
	}
	out << endl;
	out << "Overall maximum displacement for this trip is: " << overallmax <<" m"<< endl;
	out.close();		//Close output file
	cout << "Information has been written into massResults.txt" << endl;
}


void VelocityEffectAnalysis(double bumpHeight[], int size, long k, long c, double m) {
	// Defining VelocityEfectAnalysis function
	
	//Creating output filestream
	ofstream out;
	out.open("velocityResults.txt");
	if (out.fail()) {
		cerr << "Error in opening file" << endl;
		exit(-4);
	}

	//Prompting user for velocity range values
	double startvel, finalvel, stepvel;
	cout << "Enter start value for velocity in km/hr" << endl;
	cin >> startvel;
	cout << "Enter final value for velocity in km/hr" << endl;
	cin >> finalvel;
	cout << "Enter step-size for velocity in km/hr" << endl;
	cin >> stepvel;
	double overrallmax(0);
	
	//Performing velocity anakysis and writing the results into an output file
	out << "Analysis of varying velocity on displacement for current trip" << endl;
	out << "Stiffness = " << k << " Nm" << endl;
	out << "Damping = " << c << " Ns/m" << endl;
	out << endl;
	out << left << setw(20) << "Velocity(km/hr)" << setw(25) << "Displacement(m)" << endl;
	
	for (double v = startvel; v <= finalvel; v += stepvel) {
		double max(0);
		for (int j = 0; j < size; j++) {
			double displacement = CalculateDisplacement(bumpHeight[j], v, k, c, m);
			if (displacement > max) {
				max = displacement;
			}
		}
		if (max > overrallmax) { 
			overrallmax = max;
		}
		out << left << setw(21) << v << setw(20) << max << endl;
	}
	out << endl;
	out << "Overall maximum displacement for this trip is: " << overrallmax << " m" << endl;
	out.close();		//Close out
	cout << "Information has been written into velocityResults.txt" << endl;
}

void PrintData(string fileName) {
	//Defining PrintData function

	//Creating input filestream
	ifstream inFile;
	inFile.open(fileName.c_str());
	if (inFile.fail()) {
		cerr << "Error in opening file" << endl;
		exit(-5);
	}
	char ch;
	
	//Reading every character and printing it to the output console
	while (!inFile.eof()) {
		inFile.get(ch);
		cout << ch;
	}

	inFile.close();		//Close in
}	
