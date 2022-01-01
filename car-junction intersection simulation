#pragma once
#include "TrafficLight.h"
# define MAX 10
# define YELLOW_TIME 4

class Intersection {
private:
	TrafficLight Light[MAX];
	double cycleTime;
	int NumOfLights;
	double TrafficFlowRate[MAX];
	double newGreentime[MAX];
	double TotalTraffic;
public:
	Intersection() {
		NumOfLights = 0;
		cycleTime = 0;
		for (int i = 0; i < NumOfLights; i++) {
			TrafficFlowRate[i] = 0;
			newGreentime[i] = 0;
		}
		TotalTraffic = 0;
	}

	int getNumOfLights() {
		return NumOfLights;
	}

	double getcycletime() {
		return cycleTime;
	}

	double getTrafficFlowRate(int i) {
		return TrafficFlowRate[i];
	}

	double getTotalTraffic() {
		return TotalTraffic;
	}

	void readTrafficData() {
		ifstream in;
		in.open("traffic.txt");
		if (in.fail()) {
			cerr << "Error opening file" << endl;
			exit(-1);
		}
		in >> cycleTime;

		//Reading Traffic flow rate values and cumulatively computing the sum 
		for (int i = 0; i < NumOfLights; i++) {
			in >> TrafficFlowRate[i];
			TotalTraffic += TrafficFlowRate[i];
		}
		in.close();
	}

	void updateTiming(){
		// Populating the array to store the computed greentimes for the trafficlights
		for (int i = 0; i < NumOfLights; i++)
		{
			newGreentime[i] = (TrafficFlowRate[i] / TotalTraffic) * cycleTime;
		}
		
	}

	void AddLight(TrafficLight Light) {
		if (NumOfLights < MAX) {
			this->Light[NumOfLights] = Light;
			NumOfLights++;
		}
		else
		{
			cout << "Sorry no more Traffic Lights can be added" << endl;
		}
	}

	double getnewGreentime(int i) {
		return newGreentime[i];
	}

	void DropLight(int ID) {
		// Dropping traffic light via its ID
		bool located= false;
		for (int i = 0; i < NumOfLights; i++) {
			if (ID == Light[i].getID())
			{
				cout << "Traffic Light to be removed found" << endl;
				for (int j = i; j < NumOfLights; j++)
				{
					Light[j] = Light[j + 1];
				}
				NumOfLights--;
				located = true;
			}
		}
		if (!located) {
			cout << "Can't find the Light to drop" << endl;
		}

	}

};
