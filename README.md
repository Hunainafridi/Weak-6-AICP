#include <iostream>
#include <iomanip>

using namespace std;

string checkSack(char contents, double weight) {
    if (contents != 'C' && contents != 'G' && contents != 'S') {
        return "Invalid contents. Sack must contain cement (C), gravel (G), or sand (S).";
    }

    if (contents == 'G' || contents == 'S') {
        if (!(weight >= 49.9 && weight <= 50.1)) {
            return "Incorrect weight for sand or gravel. Must be between 49.9 and 50.1 kg.";
        }
    } else {
        if (!(weight >= 24.9 && weight <= 25.1)) {
            return "Incorrect weight for cement. Must be between 24.9 and 25.1 kg.";
        }
    }

    return "Contents: " + string(1, contents) + ", Weight: " + to_string(weight) + " kg - Accepted";
}

void checkOrder() {
    int cementSacks, gravelSacks, sandSacks;
    int acceptedSacks = 0, rejectedSacks = 0;
    double totalWeight = 0.0, regularPrice = 0.0;

    cout << "Enter the number of cement sacks: ";
    cin >> cementSacks;
    cout << "Enter the number of gravel sacks: ";
    cin >> gravelSacks;
    cout << "Enter the number of sand sacks: ";
    cin >> sandSacks;

    for (int i = 0; i < cementSacks; ++i) {
        char contents;
        double weight;

        cout << "Enter contents for cement sack (C): ";
        cin >> contents;
        contents = toupper(contents);

        cout << "Enter weight for cement sack: ";
        cin >> weight;

        string message = checkSack(contents, weight);
        cout << message << endl;

        if (message.find("Accepted") != string::npos) {
            ++acceptedSacks;
            totalWeight += weight;
            regularPrice += 3.0;
        } else {
            ++rejectedSacks;
        }
    }

    for (int i = 0; i < gravelSacks; ++i) {
        char contents;
        double weight;

        cout << "\nEnter contents for gravel sack (G): ";
        cin >> contents;
        contents = toupper(contents);

        cout << "Enter weight for gravel sack: ";
        cin >> weight;

        string message = checkSack(contents, weight);
        cout << message << endl;

        if (message.find("Accepted") != string::npos) {
            ++acceptedSacks;
            totalWeight += weight;
            regularPrice += 2.0;
        } else {
            ++rejectedSacks;
        }
    }

    for (int i = 0; i < sandSacks; ++i) {
        char contents;
        double weight;

        cout << "\nEnter contents for sand sack (S): ";
        cin >> contents;
        contents = toupper(contents);

        cout << "Enter weight for sand sack: ";
        cin >> weight;

        string message = checkSack(contents, weight);
        cout << message << endl;

        if (message.find("Accepted") != string::npos) {
            ++acceptedSacks;
            totalWeight += weight;
            regularPrice += 2.0;
        } else {
            ++rejectedSacks;
        }
    }

    cout << fixed << setprecision(1);
    cout << "\nTotal weight of accepted sacks: " << totalWeight << " kg" << endl;
    cout << "Number of sacks rejected: " << rejectedSacks << endl;
    cout << "Regular price: $" << regularPrice << endl;

    int specialPacks = min(cementSacks, min(gravelSacks / 2, sandSacks / 2));

    if (specialPacks > 0) {
        double discountedPrice = regularPrice - specialPacks * 5.0;
        double amountSaved = specialPacks * 5.0;
        cout << "Discount price (" << specialPacks << " special pack(s)): $" << discountedPrice << endl;
        cout << "Amount saved: $" << amountSaved << endl;
    } else {
        cout << "No discount applicable." << endl;
    }
}

int main() {
    checkOrder();
    return 0;
}
