#pragma once
#include <iostream>
#include <ctime>
#include <fstream>
#include <cmath>


using namespace std;

class TrafficLight {
private:
	int ID;
	int state;
	double greentimer;
	static int NumOfLights;

public:
	TrafficLight() {
		NumOfLights++;
		ID = NumOfLights;
		state = 1;
		greentimer = 0;
	}
	int getNumOfLights() {
		return NumOfLights;
	}
	int getID() {
		return ID;
	}
	void setstate(int state) {
		this->state = state;
	}
	int getstate() {
		return state;
	}
	void setgreentimer(double greentimer) {
		this->greentimer = greentimer;
	}
	double getgreentimer() {
		return greentimer;
	}
	void printLightInfo() {		//Printing details of a traffic light object
		//Printing eetails of a Traffic light( ID, state and corresponding light colour)
		cout << "ID: " << ID << endl;
		switch (getstate()) {
		case 0: cout << "0-off" << endl;
			break;
		case 1: cout << "1-Red" << endl;
			break;
		case 2: cout << "2-Yellow" << endl;
			break;
		case 3: cout << "3-Green" << endl;
			break;
		}
		cout << "Greentime: " << getgreentimer() << endl;
	}
	void SimulateprintLightInfo() {		//Printing details of a traffic light for simulation purposes
		// Using the states to print out the respective colours fr simulation purposes
		switch (getstate()) {
		case 0: cout << "Light " << ID << " off" << endl;
			break;
		case 1: cout << "Light " << ID << " Red" << endl;
			break;
		case 2: cout << "Light " << ID << " Yellow" << endl;
			break;
		case 3: cout << "Light " << ID << " Green" << endl;
			break;
		}
	}
	void wait(double seconds) {	
		//Delaying the output screen for some seconds 
		time_t start_time = time(NULL);
		while (time(NULL) < start_time + seconds) {}
	}
};

int TrafficLight::NumOfLights = 0;	//Initialisation of static variable
