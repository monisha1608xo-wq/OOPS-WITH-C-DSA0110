#include <iomanip>
#include <iostream>
#include <limits>
using namespace std;

int main()
{
    int hour;

    cout << "Enter journey hour (0-23): ";

    cin >> hour;

    while (cin.fail() || hour < 0 || hour > 23) {

        cout << "Invalid hour. Please enter a number from 0 to 23: ";

        cin.clear();

        cin.ignore(numeric_limits<streamsize>::max(), '\n');

        cin >> hour;
    }

    bool peak =
        (hour >= 8 && hour < 10) ||
        (hour >= 17 && hour < 20);

    long long farePaise = 3000;

    if (peak) {
        farePaise += farePaise * 20 / 100;
    }

    cout << fixed << setprecision(2);

    cout << "\nJOURNEY REPORT\n";
    cout << "Hour: " << setw(2) << setfill('0') << hour << ":00\n";
    cout << setfill(' ');
    cout << "Peak Hour: " << boolalpha << peak << '\n';

    cout << "Fare: Rs "
         << farePaise / 100.0
         << '\n';

    cout << "\nFormatted Fare: Rs "
         << farePaise / 100
         << '.'
         << setw(2)
         << setfill('0')
         << farePaise % 100
         << '\n';

    return 0;
}