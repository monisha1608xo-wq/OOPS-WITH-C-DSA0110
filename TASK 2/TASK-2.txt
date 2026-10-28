#include <iostream>
using namespace std;

constexpr long long INNER_FARE_PAISE = 1000;
constexpr long long MIDDLE_FARE_PAISE = 2000;
constexpr long long OUTER_FARE_PAISE = 3000;

constexpr int PEAK_SURCHARGE_PERCENT = 20;
constexpr long long MIN_BALANCE_PAISE = 5000;

enum class Zone {
    Inner,
    Middle,
    Outer
};

long long getFare(Zone zone) {
    switch (zone) {
        case Zone::Inner:
            return INNER_FARE_PAISE;

        case Zone::Middle:
            return MIDDLE_FARE_PAISE;

        case Zone::Outer:
            return OUTER_FARE_PAISE;
    }

    return 0;
}

long long calculateFare(Zone zone, bool peak) {
    long long fare = getFare(zone);

    if (peak) {
        fare += fare * PEAK_SURCHARGE_PERCENT / 100;
    }

    return fare;
}

int main() {
    cout << "TOKEN AND CONSTANT DEMONSTRATION\n\n";

    cout << "Inner Fare: Rs "
         << INNER_FARE_PAISE / 100 << "."
         << INNER_FARE_PAISE % 100 << '\n';

    cout << "Middle Fare: Rs "
         << MIDDLE_FARE_PAISE / 100 << "."
         << MIDDLE_FARE_PAISE % 100 << '\n';

    cout << "Outer Fare: Rs "
         << OUTER_FARE_PAISE / 100 << "."
         << OUTER_FARE_PAISE % 100 << '\n';

    cout << "Peak Surcharge: "
         << PEAK_SURCHARGE_PERCENT << "%\n";

    cout << "Minimum Balance: Rs "
         << MIN_BALANCE_PAISE / 100 << "."
         << MIN_BALANCE_PAISE % 100 << '\n';

    cout << "\nOuter Peak Fare: Rs "
         << calculateFare(Zone::Outer, true) / 100
         << "."
         << calculateFare(Zone::Outer, true) % 100
         << '\n';

    return 0;
}