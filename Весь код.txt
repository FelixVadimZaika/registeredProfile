#include<iostream>
#include<fstream>
#include <string>
#include <windows.h>

using namespace std;
int main(){
    HANDLE color = GetStdHandle(STD_OUTPUT_HANDLE);
    string command, email, name, password, inName, inPassword, inEmail, registerName, registerPassword, registerEmail;

    while (1){
        cout << "\t*===========================*" << endl;
        cout << "\t| Log in or register please |" << endl;
        cout << "\t*===========================*" << endl;
        cout << "\tCommands: (register/login/exit)" << endl;
        cout << "-->_";
        getline(cin, command);

        if (command == "exit"){
            return 1;
        }
        if (command == "register"){

            ofstream g("registrationTest.txt");

            if (!g.is_open()){
                cout << "could not open file\n";
                return 0;
            }
            cout << "\n\n" << "New Username: ";
            getline(cin, registerName);

            cout << "New Password: ";
            getline(cin, registerPassword);

            cout << "New Email: ";
            getline(cin, registerEmail);

            g << registerName;
            g << '\n';
            g << registerPassword;
            g << '\n';
            g << registerEmail;
            g.close();
        }
        if (command == "login")
        {
            ifstream f("registrationTest.txt");
            if (!f.is_open()) {
                cout << "could not open file\n";
                return 0;
            }
            getline(f, name, '\n');
            getline(f, password, '\n');
            getline(f, email, '\n');
            f.close();

            //login
            while (1) {
                cout << "\n\n\n" << "Enter Username: ";
                getline(cin, inName);
                cout << "Enter Password: ";
                getline(cin, inPassword);
                cout << endl;
                if (inName == name && inPassword == password){
                    SetConsoleTextAttribute(color, FOREGROUND_GREEN);
                    cout << "Login Successful\n" << endl;
                    SetConsoleTextAttribute(color, FOREGROUND_RED | FOREGROUND_BLUE | FOREGROUND_GREEN);
                    cout << "Welcome, " << inName;
                    break;
                }
                SetConsoleTextAttribute(color, FOREGROUND_RED);
                cout << "incorrect name or password\n";
                SetConsoleTextAttribute(color, FOREGROUND_RED | FOREGROUND_BLUE | FOREGROUND_GREEN);
            }

        }
        cout << "\n\n\n\n\n";
    }
    return 1;
}