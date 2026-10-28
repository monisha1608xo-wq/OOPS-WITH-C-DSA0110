#include <climits>
#include <iostream>
using namespace std;

int main() {
    bool valid = true;
    char zoneCode = 'I';
    int hour = 18;
    long long balancePaise = 10000;
    unsigned int journeys = 3000000;
    float percentage = 20.0f;
    double rupees = 36.50;
    auto fare = 3000LL;

    cout << "DATA TYPE ANALYSIS\n\n";

    cout << boolalpha;

    cout << "bool       size = " << sizeof(valid) << " byte\n";
    cout << "char       size = " << sizeof(zoneCode) << " byte\n";
    cout << "int        size = " << sizeof(hour) << " bytes\n";
    cout << "long long  size = " << sizeof(balancePaise) << " bytes\n";
    cout << "unsigned   size = " << sizeof(journeys) << " bytes\n";
    cout << "float      size = " << sizeof(percentage) << " bytes\n";
    cout << "double     size = " << sizeof(rupees) << " bytes\n";
    cout << "auto       size = " << sizeof(fare) << " bytes\n";

    cout << "\nVALUES\n";

    cout << "Valid: " << valid << '\n';
    cout << "Zone Code: " << zoneCode << '\n';
    cout << "Hour: " << hour << '\n';
    cout << "Balance: " << balancePaise << " paise\n";
    cout << "Journeys: " << journeys << '\n';
    cout << "Percentage: " << percentage << '\n';
    cout << "Fare: " << fare << " paise\n";

    cout << "\nINT RANGE\n";
    cout << "INT_MIN = " << INT_MIN << '\n';
    cout << "INT_MAX = " << INT_MAX << '\n';

    cout << "\nLONG LONG RANGE\n";
    cout << "LLONG_MIN = " << LLONG_MIN << '\n';
    cout << "LLONG_MAX = " << LLONG_MAX << '\n';

    long long networkCollection = 3000000LL * 3000LL;

    cout << "\nNetwork collection for 3,000,000 fares of Rs 30:\n";
    cout << networkCollection << " paise\n";
    cout << "Rs " << networkCollection / 100 << '\n';

    cout << "\nMoney should be stored as integer paise to avoid "
            "floating-point rounding problems.\n";

    return 0;
}