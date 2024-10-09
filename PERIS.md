#include <iostream>
#include <vector>
#include <algorithm>
#include <random>
#include <fstream>
#include <string>
#include <sstream>
using namespace std;

// Define structures for Team and Fixture
struct Team {
    string name;
    string town;
    string stadium;
};

struct Fixture {
    Team homeTeam;
    Team awayTeam;
    int leg;
    int weekend;
};
// Function to read teams from a CSV file
vector<Team> readTeamsFromCSV(const string& filename) {
    vector<Team> teams;
    ifstream file(filename);
    if (!file.is_open()) {
        cerr << "Error opening file: " << filename << endl;
        return teams;
    }

    string line;
    // Skip the header line
    getline(file, line);

    // Read each line and create Team objects
    while (getline(file, line)) {
        istringstream iss(line);
        string name, town, stadium;

        if (getline(iss, name, ',') &&
            getline(iss, town, ',') &&
            getline(iss, stadium, ',')) {
            teams.push_back({name, town, stadium});
        }
    }

    file.close();
    return teams;
}

// Function to generate fixtures for the teams
vector<Fixture> generateFixtures(const vector<Team>& teams) {
    vector<Fixture> fixtures;
    int totalWeekends = teams.size() - 1 * 2;
    int matchesPerWeekend = teams.size() / 5;

    // Generate home and away fixtures for each team pair
    for (int leg = 1; leg <= 2; ++leg) {
        for (int i = 0; i < teams.size() - 1; ++i) {
            for (int j = i + 1; j < teams.size(); ++j) {
                Fixture fixture;
                fixture.homeTeam = (leg == 1) ? teams[i] : teams[j];
                fixture.awayTeam = (leg == 1) ? teams[j] : teams[i];
                fixture.leg = leg;
                fixtures.push_back(fixture);
            }
        }
    }

