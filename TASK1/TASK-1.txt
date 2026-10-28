#include <iostream>
#include <string>
using namespace std;

class Passenger {
private:
    string name;
    bool student;
    bool seniorCitizen;

public:
    Passenger(string n, bool s, bool senior)
        : name(n), student(s), seniorCitizen(senior) {}

    void display() const {
        cout << "Passenger: " << name << '\n';
        cout << "Student: " << boolalpha << student << '\n';
        cout << "Senior Citizen: " << seniorCitizen << '\n';
    }
};

enum class Zone {
    Inner,
    Middle,
    Outer
};

class Journey {
private:
    Zone zone;
    int hour;

public:
    Journey(Zone z, int h) : zone(z), hour(h) {}

    void display() const {
        cout << "Journey Zone: ";

        switch (zone) {
            case Zone::Inner:
                cout << "Inner";
                break;
            case Zone::Middle:
                cout << "Middle";
                break;
            case Zone::Outer:
                cout << "Outer";
                break;
        }

        cout << "\nHour: " << hour << ":00\n";
    }
};

class FareTable {
public:
    static constexpr long long INNER_FARE = 1000;
    static constexpr long long MIDDLE_FARE = 2000;
    static constexpr long long OUTER_FARE = 3000;

    static long long getFare(Zone zone) {
        switch (zone) {
            case Zone::Inner:
                return INNER_FARE;
            case Zone::Middle:
                return MIDDLE_FARE;
            case Zone::Outer:
                return OUTER_FARE;
        }

        return 0;
    }
};

class SmartCard {
private:
    long long balancePaise;

public:
    SmartCard(long long balance) : balancePaise(balance) {}

    long long getBalance() const {
        return balancePaise;
    }

    bool canTravel(long long fare) const {
        return balancePaise - fare >= 5000;
    }

    void deduct(long long fare) {
        if (canTravel(fare)) {
            balancePaise -= fare;
        }
    }
};

int main() {
    cout << "CITY METRO SMART-CARD SYSTEM\n\n";

    Passenger passenger("Student Passenger", true, false);
    passenger.display();

    cout << "\n";

    Journey journey(Zone::Outer, 18);
    journey.display();

    long long fare = FareTable::getFare(Zone::Outer);

    SmartCard card(10000);

    cout << "\nFare: Rs " << fare / 100 << "." << fare % 100 << '\n';
    cout << "Initial Balance: Rs "
         << card.getBalance() / 100 << "." << card.getBalance() % 100 << '\n';

    if (card.canTravel(fare)) {
        card.deduct(fare);
        cout << "Journey Allowed\n";
    } else {
        cout << "Journey Denied\n";
    }

    cout << "Final Balance: Rs "
         << card.getBalance() / 100 << "." << card.getBalance() % 100 << '\n';

    return 0;
}