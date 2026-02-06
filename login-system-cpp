#include<iostream>
#include<fstream>
#include<string>
#include<sstream>

using namespace std;

void intro() {
    cout << "\n*************************" << endl;
    cout << "Press 1 for Registration " << endl;
    cout << "Press 2 for Login " << endl;
    cout << "Press 3 to exit " << endl;
    cout << "*************************" << endl;
}

void registration() {
    string name, username, password;
    int key;

    cin.ignore();
    cout << "Enter Fullname: ";
    getline(cin, name);
    cout << "Enter Username: ";
    getline(cin, username);
    cout << "Enter Password: ";
    getline(cin, password);
    cout << "Enter Recovery key (numbers only): ";
    cin >> key;

    ofstream reg("data.txt", ios::app);
    if (reg.is_open()) {
        reg << name << endl;
        reg << username << endl;
        reg << password << endl;
        reg << key << endl;
        reg.close();
        cout << "\n*************************" << endl;
        cout << "Registration Successful...." << endl;
        cout << "*************************\n" << endl;
    }
    else {
        cout << "Error in opening file..." << endl;
    }
}

void recovery(string username_to_find) {
    string name, username, password, new_password;
    int key, recovery_key;

    cin.ignore();
    cout << "\nEnter Full Name : ";
    getline(cin, name);
    cout << "Enter Recovery Key : ";
    cin >> recovery_key;

    ifstream reg("data.txt");
    ofstream temp("temp.txt");

    string stored_name, stored_username, stored_password;
    int stored_key;
    bool found = false;

    while (getline(reg, stored_name)) {
        getline(reg, stored_username);
        getline(reg, stored_password);
        reg >> stored_key;
        reg.ignore(); 

        if (stored_username == username_to_find) {
            if (stored_name == name && stored_key == recovery_key) {
                cout << "\n*******************" << endl;
                cout << "Details Matched..." << endl;
                cout << "*******************" << endl;

                cin.ignore();
                cout << "Enter New Password : ";
                getline(cin, new_password);

                temp << stored_name << endl;
                temp << stored_username << endl;
                temp << new_password << endl;
                temp << stored_key << endl;

                found = true;

                cout << "\n***********************" << endl;
                cout << "Password Changed,,," << endl;
                cout << "***********************\n" << endl;
            }
            else {
                cout << "\nWrong recovery details..." << endl;
                temp << stored_name << endl;
                temp << stored_username << endl;
                temp << stored_password << endl;
                temp << stored_key << endl;
            }
        }
        else {
            temp << stored_name << endl;
            temp << stored_username << endl;
            temp << stored_password << endl;
            temp << stored_key << endl;
        }
    }

    reg.close();
    temp.close();

    remove("data.txt");
    rename("temp.txt", "data.txt");
}

void login() {
    string username, password;

    cout << "Enter Username : ";
    cin >> username;
    cin.ignore();
    cout << "Enter Password : ";
    getline(cin, password);

    ifstream reg("data.txt");
    if (!reg.is_open()) {
        cout << "\nNo users registered yet..." << endl;
        return;
    }

    string stored_name, stored_username, stored_password;
    int stored_key;
    bool found = false;

    while (getline(reg, stored_name)) {
        getline(reg, stored_username);
        getline(reg, stored_password);
        reg >> stored_key;
        reg.ignore(); 

        if (username == stored_username) {
            found = true;
            if (password == stored_password) {
                cout << "\n******************" << endl;
                cout << "Login Successful..." << endl;
                cout << "Welcome, " << stored_name << "!" << endl;
                cout << "******************\n" << endl;
                reg.close();
                return;
            }
            else {
                cout << "\nWrong Password..." << endl;
                char recover;
                cout << "Want to recover your password? (y/n): ";
                cin >> recover;

                if (recover == 'y' || recover == 'Y') {
                    reg.close();
                    recovery(username);
                    return;
                }
                else {
                    reg.close();
                    return;
                }
            }
        }
    }

    if (!found) {
        cout << "\nUsername not found... Please register first." << endl;
    }

    reg.close();
}

int main() {
    int choice;

    do {
        intro();
        cout << "Enter your choice : ";
        cin >> choice;

        if (choice == 1) {
            registration();
        }
        else if (choice == 2) {
            login();
        }
        else if (choice == 3) {
            cout << "\nThank you for using the system  :)" << endl;
            break;
        }
        else {
            cout << "\nWrong choice... Please select between 1-3.\n" << endl;
        }

    } while (choice != 3);

    return 0;
}
