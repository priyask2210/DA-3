> DA-3

```
#include <iostream>
#include <string>
using namespace std;

struct Service {
    int serviceNumber;
    string serviceName;
    float serviceCharge;
    string serviceDescription;
};

void view(Service* ser, int length, int sn) {
    int found = 0;
    for (int k = 0; k < length; k++) {
        if (ser[k].serviceNumber == sn) {
            found = 1;
            cout << "Service: " << ser[k].serviceName << endl;
            cout << "Service charge: " << ser[k].serviceCharge << endl;
            cout << "Description: " << ser[k].serviceDescription << endl;
        }
    }
    if (found == 0) {
        cout << "Record not found" << endl;
    }
}

void add(Service* ser, int& length, int sn, std::string p, float c, string d) {
    Service newService;
    newService.serviceNumber = sn;
    newService.serviceName = p;
    newService.serviceCharge = c;
    newService.serviceDescription = d;

    ser[length] = newService;
    length++;

    cout << "Record added" << endl;
}

void modify(Service* ser, int length, int sn) {
    int found = 0;
    for (int k = 0; k < length; k++) {
        if (ser[k].serviceNumber == sn) {
            found = 1;
            std::cout << "Service: " << ser[k].serviceName << endl;
            char m1;
            cout << "Modify service? (y/n) : ";
            std::cin >> m1;
            if (m1 == 'y') {
                string r1;
                cout << "Enter new service: ";
                cin >> r1;
                ser[k].serviceName = r1;
            } else if (m1 == 'n') {
                // Do nothing
            } else {
                cout << "Invalid entry. Kindly enter y (for yes) and n (for no)" << endl;
                break;
            }

            float a = ser[k].serviceCharge;
            cout << "Price: " << a << endl;
            char m2;
            cout << "Modify service charge? (y/n) : ";
            cin >> m2;
            if (m2 == 'y') {
                float r2;
                cout << "Enter new charge: ";
                cin >> r2;
                ser[k].serviceCharge = r2;
            } else if (m2 == 'n') {
                // Do nothing
            } else {
                cout << "Invalid entry. Kindly enter y (for yes) and n (for no)" << endl;
                break;
            }

            string b = ser[k].serviceDescription;
            cout << "Description: " << b << endl;
            char m3;
            cout << "Modify description? (y/n): ";
            cin >> m3;
            if (m3 == 'y') {
                string r3;
                cout << "Enter new description: ";
                cin >> r3;
                ser[k].serviceDescription = r3;
            } else if (m3 == 'n') {
                // Do nothing
            } else {
                cout << "Invalid entry. Kindly enter y (for yes) and n (for no)" << endl;
            }

            if (m1 == 'y' || m2 == 'y' || m3 == 'y') {
                cout << "Record modified" << endl;
            } else if (m1 == 'n' || m2 == 'n' || m3 == 'n') {
                cout << "Record not modified" << endl;
            }
        }
    }
    if (found == 0) {
        std::cout << "Record not found" << std::endl;
    }
}

void deleteRecord(Service* ser, int& length, int sn) {
    if (sn <= length) {
        string s = ser[sn - 1].serviceName;
        float c = ser[sn - 1].serviceCharge;
        string d = ser[sn - 1].serviceDescription;
        cout << "Service number: " << sn << endl;
        cout << "Service: " << s << std::endl;
        cout << "Service description: " << d << endl;
        cout << "Service charge: " << c << endl;
        char confirm;
        cout << "Are you sure (y/n)? : ";
        cin >> confirm;
        if (confirm == 'y') {
            for (int i = sn - 1; i < length - 1; i++) {
                ser[i] = ser[i + 1];
            }
            length--;
            cout << "Record deleted" << endl;
        } else if (confirm == 'n') {
            cout << "Record not deleted" << endl;
        } else {
            cout << "Invalid entry. Kindly enter y (for yes) and n (for no)" << endl;
        }
    } else {
        cout << "Record not found" << endl;
    }
}

void individual(Service* ser, int length, int sn) {
    if (sn <= length) {
        int s = sn - 1;
        string p = ser[s].serviceName;
        float c = ser[s].serviceCharge;
        string d = ser[s].serviceDescription;
        cout << "Service number: " << sn << endl;
        cout << "Service: " << p << endl;
        cout << "Service charge: " << c << endl;
        cout << "Service description: " << d << endl;
        int nop;
        std::cout << "Enter no. of people: ";
        std::cin >> nop;
        if (nop <= 9) {
            float tp = c * nop;
            float pa = tp - (10.0 / 100.0 * tp);
            cout << "Total price: " << tp << endl;
            cout << "Discount: 10%" << endl;
            cout << "Payable amount: " << pa << endl;
        } else {
            std::cout << "No. of people more than 9 - choose the party option" << std::endl;
        }
    } else {
        cout << "Record not found" << endl;
    }
}

void party(Service* ser, int length, int sn) {
    if (sn <= length) {
        int s = sn - 1;
        string p = ser[s].serviceName;
        float c = ser[s].serviceCharge;
        string d = ser[s].serviceDescription;
        cout << "Service number: " << sn << endl;
        cout << "Service: " << p << endl;
        cout << "Service description: " << d << endl;
        cout << "Service charge: " << c << endl;

        int nop;
        cout << "Enter no. of people: ";
        cin >> nop;
        if (nop >= 10) {
            float tp = c * nop;
            float pa = tp - (25.0 / 100.0 * tp);
            cout << "Total price: " << tp << endl;
            cout << "Discount: 25%" << endl;
            cout << "Payable amount: " << pa << endl;
        } else {
            std::cout << "No. of people less than 10 - choose the individual option" << endl;
        }
    } else {
        cout << "Record not found" << endl;
    }
}

int main() {
    const int MAX_SERVICES = 10; 
    Service ser[MAX_SERVICES];
    int length = 10;

    ser[0] = {1, "Facial (Skincare)", 150, "Using Aveeno and Clinique products"};
    ser[1] = {2, "Waxing (Skincare)", 30, "Using Veet hair removal cream and wax strips"};
    ser[2] = {3, "Hair cut (Hair care)", 50, "Using Jundo hair cut set"};
    ser[3] = {4, "Threading (Skincare)", 30, "Using Vanity threading set"};
    ser[4] = {5, "Hair colouring (Hair care)", 110, "Using L'Oreal products"};
    ser[5] = {6, "Hair straightening (Hair care)", 80, "Using Dyson straightening set"};
    ser[6] = {7, "Hair curling (Hair care)", 80, "Using Dyson straightening set"};
    ser[7] = {8, "Manicure (Skincare)", 60, "Using VLCC manicure set"};
    ser[8] = {9, "Pedicure (Skincare)", 60, "Using VLCC pedicure set"};
    ser[9] = {10, "Make up (Skincare)", 170, "Using Clinique makeup products"};

    int choice;
do {
    cout << endl;
    cout << "1.View" << endl << "2.Add" << endl << "3.Modify" << endl << "4.Delete" << endl << "5.Individual" << endl << "6.Party" << endl << "7.Exit" << endl;
    cout << "Enter choice (1-7): ";
    cin >> choice;

    if (choice == 1) {
        int sn;
        cout << "Enter service number: ";
        cin >> sn;
        view(ser, length, sn);
    } else if (choice == 2) {
        int sn;
        string p, d;
        float c;
        cout << "Enter service number: ";
        cin >> sn;
        cout << "Enter service: ";
        cin >> p;
        cout << "Enter service description: ";
        cin >> d;
        cout << "Enter service charge: ";
        cin >> c;
        add(ser, length, sn, p, c, d);
    } else if (choice == 3) {
        int sn;
        cout << "Enter service number: ";
        cin >> sn;
        modify(ser, length, sn);
    } else if (choice == 4) {
        int sn;
        cout << "Enter service number: ";
        cin >> sn;
        deleteRecord(ser, length, sn);
    } else if (choice == 5) {
        int sn;
        cout << "Enter service number: ";
        cin >> sn;
        individual(ser, length, sn);
    } else if (choice == 6) {
        int sn;
        cout << "Enter service number: ";
        cin >> sn;
        party(ser, length, sn);
    } else if (choice == 7) {
        cout << "Exiting program" << endl;
    } else {
        cout << "Invalid choice" << endl;
        break;
    }
} while (choice < 8);
return 0;
}
```
