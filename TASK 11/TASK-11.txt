#include <iostream>
#include <string>
using namespace std;

enum class Zone {
    Inner,
    Middle,
    Outer
};

class FareTable {
private:
    static constexpr long long INNER = 1000;
    static constexpr long long MIDDLE = 2000;
    static constexpr long long OUTER = 3000;

public:
    static long long getBaseFare(Zone zone)
    {
        switch (zone) {

            case Zone::Inner:
                return INNER;

            case Zone::Middle:
                return MIDDLE;

            case Zone::Outer:
                return OUTER;
        }

        return 0;
    }
};

class SmartCard {
private:
    long long balancePaise;

    static constexpr long long MIN_BALANCE_PAISE = 5000;

public:
    explicit SmartCard(long long initialBalance)
        : balancePaise(initialBalance) {}

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

bool isPeak(int hour)
{
    return (hour >= 8 && hour < 10) ||
           (hour >= 17 && hour < 20);
}

long long calculateFare(Zone zone, int hour)
{
    long long fare = FareTable::getBaseFare(zone);

    if (isPeak(hour)) {
        fare += fare * 20 / 100;
    }

    return fare;
}

void printMoney(long long paise)
{
    cout << "Rs "
         << paise / 100
         << '.'
         << (paise % 100 < 10 ? "0" : "")
         << paise % 100;
}

int main()
{
    cout << "FINAL METRO FARE DESIGN\n";
    cout << "=======================\n\n";

    SmartCard card(10000);

    cout << "Initial Balance: ";
    printMoney(card.getBalance());
    cout << '\n';

    long long fare1 = calculateFare(Zone::Inner, 12);

    cout << "Journey 1 Fare: ";
    printMoney(fare1);
    cout << '\n';

    if (card.deduct(fare1)) {
        cout << "Journey 1: Allowed\n";
    } else {
        cout << "Journey 1: Denied\n";
    }

    long long fare2 = calculateFare(Zone::Outer, 18);

    cout << "Journey 2 Fare: ";
    printMoney(fare2);
    cout << '\n';

    if (card.deduct(fare2)) {
        cout << "Journey 2: Allowed\n";
    } else {
        cout << "Journey 2: Denied\n";
    }

    cout << "Final Balance: ";
    printMoney(card.getBalance());
    cout << '\n';

    cout << "\nDesign decisions:\n";
    cout << "1. Money is stored as integer paise.\n";
    cout << "2. Fare values are centralized in FareTable.\n";
    cout << "3. SmartCard balance is private.\n";
    cout << "4. Minimum balance is enforced by canTravel().\n";
    cout << "5. Peak surcharge uses integer arithmetic.\n";
    cout << "6. enum class is used for zones.\n";

    return 0;
}