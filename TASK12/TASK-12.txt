#include <iomanip>
#include <iostream>
#include <string>
using namespace std;

enum class Zone {
    Inner,
    Middle,
    Outer,
    Airport
};

class FareTable {
public:
    static constexpr long long INNER = 1000;
    static constexpr long long MIDDLE = 2000;
    static constexpr long long OUTER = 3000;
    static constexpr long long AIRPORT = 6000;

    static long long getFare(Zone zone)
    {
        switch (zone) {

            case Zone::Inner:
                return INNER;

            case Zone::Middle:
                return MIDDLE;

            case Zone::Outer:
                return OUTER;

            case Zone::Airport:
                return AIRPORT;
        }

        return 0;
    }
};

class FareCalculator {
public:

    static bool isPeak(int hour)
    {
        return (hour >= 8 && hour < 10) ||
               (hour >= 17 && hour < 20);
    }

    static long long calculate(
        Zone zone,
        int hour,
        bool weekend)
    {
        long long fare = FareTable::getFare(zone);

        bool peak = isPeak(hour);

        // Weekend discount has priority.
        // It does not combine with peak surcharge.
        if (weekend) {

            fare -= fare * 10 / 100;

        } else if (peak) {

            fare += fare * 20 / 100;
        }

        return fare;
    }
};

class MonthlyPass {
private:
    Zone zone1;
    Zone zone2;

public:
    MonthlyPass(Zone first, Zone second)
        : zone1(first), zone2(second) {}

    bool covers(Zone zone) const
    {
        return zone == zone1 || zone == zone2;
    }

    void display() const
    {
        cout << "Monthly Pass covers two selected zones.\n";
    }
};

class SmartCard {
private:
    long long balancePaise;

    static constexpr long long MIN_BALANCE_PAISE = 5000;

public:
    explicit SmartCard(long long balance)
        : balancePaise(balance) {}

    bool canTravel(long long fare) const
    {
        return balancePaise - fare >= MIN_BALANCE_PAISE;
    }

    bool deduct(long long fare)
    {
        if (!canTravel(fare))
            return false;

        balancePaise -= fare;
        return true;
    }

    long long getBalance() const
    {
        return balancePaise;
    }
};

void printMoney(long long paise)
{
    cout << "Rs "
         << paise / 100
         << '.'
         << setw(2)
         << setfill('0')
         << paise % 100
         << setfill(' ');
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

        case Zone::Airport:
            return "Airport";
    }

    return "Unknown";
}

void testFare(
    Zone zone,
    int hour,
    bool weekend)
{
    long long fare =
        FareCalculator::calculate(
            zone,
            hour,
            weekend);

    cout << zoneName(zone)
         << " | Hour: "
         << hour
         << ":00 | Weekend: "
         << boolalpha
         << weekend
         << " | Fare: ";

    printMoney(fare);

    cout << '\n';
}

int main()
{
    cout << "REDESIGNED METRO SMART-CARD SYSTEM\n";
    cout << "==================================\n\n";

    cout << "1. NORMAL OFF-PEAK\n";
    testFare(Zone::Inner, 12, false);
    testFare(Zone::Middle, 12, false);
    testFare(Zone::Outer, 12, false);
    testFare(Zone::Airport, 12, false);

    cout << "\n2. PEAK FARES\n";
    testFare(Zone::Inner, 8, false);
    testFare(Zone::Outer, 18, false);
    testFare(Zone::Airport, 18, false);

    cout << "\n3. WEEKEND DISCOUNT\n";
    testFare(Zone::Inner, 12, true);
    testFare(Zone::Outer, 12, true);
    testFare(Zone::Airport, 12, true);

    cout << "\n4. WEEKEND DURING PEAK TIME\n";
    testFare(Zone::Outer, 18, true);

    cout << "\n5. MONTHLY PASS\n";

    MonthlyPass pass(
        Zone::Inner,
        Zone::Middle);

    pass.display();

    cout << "Inner covered: "
         << pass.covers(Zone::Inner)
         << '\n';

    cout << "Middle covered: "
         << pass.covers(Zone::Middle)
         << '\n';

    cout << "Outer covered: "
         << pass.covers(Zone::Outer)
         << '\n';

    cout << "\n6. SMART CARD TEST\n";

    SmartCard card(10000);

    cout << "Initial Balance: ";
    printMoney(card.getBalance());
    cout << '\n';

    long long fare =
        FareCalculator::calculate(
            Zone::Airport,
            18,
            false);

    cout << "Airport Peak Fare: ";
    printMoney(fare);
    cout << '\n';

    if (card.deduct(fare)) {
        cout << "Journey Allowed\n";
    } else {
        cout << "Journey Denied - Minimum balance rule\n";
    }

    cout << "Final Balance: ";
    printMoney(card.getBalance());
    cout << '\n';

    cout << "\nDESIGN DECISION\n";
    cout << "The original design is MODIFIED.\n";
    cout << "A fare table supports the fourth zone.\n";
    cout << "Weekend discount is separated from peak surcharge.\n";
    cout << "MonthlyPass handles unlimited travel in two zones.\n";
    cout << "SmartCard continues to protect the minimum balance.\n";

    return 0;
}