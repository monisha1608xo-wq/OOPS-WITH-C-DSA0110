#include <iostream>
using namespace std;

constexpr long long MIN_BALANCE = 5000;

// --------------------------------------------------
// PROCEDURAL VERSION
// --------------------------------------------------

long long proceduralFare(int zone, bool peak)
{
    long long fare = 0;

    if (zone == 1)
        fare = 1000;
    else if (zone == 2)
        fare = 2000;
    else if (zone == 3)
        fare = 3000;

    if (peak)
        fare += fare * 20 / 100;

    return fare;
}

bool proceduralCanTravel(long long balance, long long fare)
{
    return balance - fare >= MIN_BALANCE;
}

void proceduralDeduct(long long& balance, long long fare)
{
    if (proceduralCanTravel(balance, fare))
        balance -= fare;
}

// --------------------------------------------------
// OBJECT-ORIENTED VERSION
// --------------------------------------------------

class SmartCard {
private:
    long long balancePaise;

public:
    SmartCard(long long balance)
        : balancePaise(balance) {}

    bool canTravel(long long fare) const
    {
        return balancePaise - fare >= MIN_BALANCE;
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

long long objectOrientedFare(int zone, bool peak)
{
    long long fare = 0;

    switch (zone) {
        case 1:
            fare = 1000;
            break;

        case 2:
            fare = 2000;
            break;

        case 3:
            fare = 3000;
            break;

        default:
            fare = 0;
    }

    if (peak)
        fare += fare * 20 / 100;

    return fare;
}

int main()
{
    cout << "PROCEDURAL VERSION\n";

    long long proceduralBalance = 10000;
    long long proceduralFareValue = proceduralFare(3, true);

    cout << "Fare: Rs "
         << proceduralFareValue / 100
         << "."
         << proceduralFareValue % 100
         << '\n';

    if (proceduralCanTravel(proceduralBalance, proceduralFareValue)) {
        proceduralDeduct(proceduralBalance, proceduralFareValue);
        cout << "Journey Allowed\n";
    } else {
        cout << "Journey Denied\n";
    }

    cout << "Balance: Rs "
         << proceduralBalance / 100
         << "."
         << proceduralBalance % 100
         << "\n\n";

    cout << "OBJECT-ORIENTED VERSION\n";

    SmartCard card(10000);

    long long objectFare = objectOrientedFare(3, true);

    cout << "Fare: Rs "
         << objectFare / 100
         << "."
         << objectFare % 100
         << '\n';

    if (card.deduct(objectFare)) {
        cout << "Journey Allowed\n";
    } else {
        cout << "Journey Denied\n";
    }

    cout << "Balance: Rs "
         << card.getBalance() / 100
         << "."
         << card.getBalance() % 100
         << '\n';

    return 0;
}