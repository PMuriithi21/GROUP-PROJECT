
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
        for (int i = 0; i < teams.size() - 1; ++i) 


