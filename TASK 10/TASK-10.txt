#include <iomanip>
#include <iostream>
#include <limits>
using namespace std;

int main()
{
    const long long farePaise = 3000;
    const double fareRupees = 30.00;

    long long journeyCounts[] = {
        20000,
        500000,
        3000000
    };

    cout << fixed << setprecision(15);

    cout << "DOUBLE VS INTEGER PAISE\n";
    cout << "=======================\n\n";

    for (long long n : journeyCounts) {

        long long integerTotal = n * farePaise;

        double doubleTotal = n * fareRupees;

        long long doubleAsPaise =
            static_cast<long long>(doubleTotal * 100.0 + 0.5);

        cout << "Journeys: " << n << '\n';

        cout << "Integer total: "
             << integerTotal
             << " paise\n";

        cout << "Integer total: Rs "
             << integerTotal / 100
             << '.'
             << setw(2)
             << setfill('0')
             << integerTotal % 100
             << setfill(' ')
             << '\n';

        cout << "Double total: Rs "
             << doubleTotal
             << '\n';

        cout << "Double converted to paise: "
             << doubleAsPaise
             << '\n';

        cout << "Difference in paise: "
             << integerTotal - doubleAsPaise
             << '\n';

        cout << "-----------------------------\n";
    }

    cout << "\nINT RANGE CHECK\n";
    cout << "INT_MAX = "
         << numeric_limits<int>::max()
         << '\n';

    long long networkTotalPaise =
        3000000LL * 3000LL;

    cout << "Network total = "
         << networkTotalPaise
         << " paise\n";

    cout << "Network total = Rs "
         << networkTotalPaise / 100
         << '\n';

    long long intMax = numeric_limits<int>::max();

    cout << "\nDoes network total exceed INT_MAX? "
         << boolalpha
         << (networkTotalPaise > intMax)
         << '\n';

    cout << "\nCompile this program using:\n";
    cout << "g++ -std=c++17 -Wall -Wextra Task10_Execution.cpp\n";

    return 0;
}