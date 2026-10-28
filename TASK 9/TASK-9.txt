#include <iomanip>
#include <iostream>
#include <string>
using namespace std;

enum class Zone {
    Inner,
    Middle,
    Outer
};

constexpr long long MIN_BALANCE_PAISE = 5000;
constexpr int PEAK_SURCHARGE_PERCENT = 20;

long long baseFare(Zone zone)
{
    switch (zone) {

        case Zone::Inner:
            return 1000;

        case Zone::Middle:
            return 2000;

        case Zone::Outer:
            return 3000;
    }

    return -1;
}

bool isPeak(int hour)
{
    return (hour >= 8 && hour < 10) ||
           (hour >= 17 && hour < 20);
}

long long calculateFare(Zone zone, int hour)
{
    long long fare = baseFare(zone);

    if (fare < 0)
        return -1;

    if (isPeak(hour)) {
        fare += fare * PEAK_SURCHARGE_PERCENT / 100;
    }

    return fare;
}

bool canTravel(long long balance, long long fare)
{
    return fare >= 0 &&
           balance - fare >= MIN_BALANCE_PAISE;
}

string zoneName(Zone zone)
{
    switch (zone) {

        case Zone::Inner:
            return "Inner";

        case Zone::Middle:
            return "Middle";

        case Zone::Outer:
            return "Outer";
    }

    return "Unknown";
}

void printFare(long long fare)
{
    if (fare < 0) {
        cout << "Invalid";
        return;
    }

    cout << "Rs "
         << fare / 100
         << '.'
         << setw(2)
         << setfill('0')
         << fare % 100
         << setfill(' ');
}

int main()
{
    cout << "METRO FARE TESTING\n";
    cout << "==================\n\n";

    struct Test {
        string name;
        Zone zone;
        int hour;
        long long balance;
    };

    Test tests[] = {

        {"Inner Off-Peak", Zone::Inner, 12, 10000},

        {"Middle Off-Peak", Zone::Middle, 12, 10000},

        {"Outer Off-Peak", Zone::Outer, 12, 10000},

        {"Inner Peak", Zone::Inner, 8, 10000},

        {"Middle Peak", Zone::Middle, 18, 10000},

        {"Outer Peak", Zone::Outer, 19, 10000},

        {"Exactly 8 AM", Zone::Outer, 8, 10000},

        {"Exactly 10 AM", Zone::Outer, 10, 10000},

        {"Exactly 5 PM", Zone::Outer, 17, 10000},

        {"Exactly 8 PM", Zone::Outer, 20, 10000},

        {"Exactly Rs 50 Remaining", Zone::Middle, 12, 7000}
    };

    for (const Test& test : tests) {

        long long fare =
            calculateFare(test.zone, test.hour);

        cout << test.name << "\n";

        cout << "Zone: "
             << zoneName(test.zone) << '\n';

        cout << "Hour: "
             << test.hour << ":00\n";

        cout << "Fare: ";
        printFare(fare);
        cout << '\n';

        cout << "Can Travel: "
             << boolalpha
             << canTravel(test.balance, fare)
             << '\n';

        cout << "-------------------------\n";
    }

    cout << "\n5-JOURNEY MANUAL TEST\n";

    Zone journeyZones[] = {
        Zone::Inner,
        Zone::Middle,
        Zone::Outer,
        Zone::Inner,
        Zone::Middle
    };

    int journeyHours[] = {
        12,
        12,
        12,
        18,
        18
    };

    long long total = 0;

    for (int i = 0; i < 5; i++) {

        long long fare =
            calculateFare(journeyZones[i], journeyHours[i]);

        total += fare;

        cout << "Journey " << i + 1
             << ": ";

        printFare(fare);

        cout << '\n';
    }

    cout << "Total: ";
    printFare(total);
    cout << '\n';

    return 0;
}