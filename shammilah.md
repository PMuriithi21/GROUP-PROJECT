// Function to display fixtures on the console
void displayFixtures(const vector<Fixture>& fixtures) {
    for (const auto& fixture : fixtures) {
        cout << "Weekend #" << fixture.weekend << ": "
                  << fixture.homeTeam.name << " vs " << fixture.awayTeam.name
                  << " (Leg " << fixture.leg << ")\n"
                  << "  Stadium: " << fixture.homeTeam.stadium << " (" << fixture.homeTeam.town << ")\n"
                  << "  Away team from: " << fixture.awayTeam.town << "\n\n";
    }
}

// Main function
int main() {
    // Read teams from CSV file
    vector<Team> teams = readTeamsFromCSV("teams_csvFile.csv");
    if (teams.empty()) {
        cerr << "No teams were read from the CSV file. Exiting." << endl;
        return 1;
    }

    // Generate fixtures
    vector<Fixture> fixtures = generateFixtures(teams);

    // Display fixtures on console
    displayFixtures(fixtures);

    // Save fixtures to CSV file
    saveFixturesToCSV(fixtures, "fixtures.csv");
    cout << "Fixtures have been saved to fixtures.csv" << endl;

 return 0;
}
