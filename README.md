#include <iostream>
#include <algorithm>
#include <climits>
#include <conio.h>
#include <cctype>
#include <iomanip>
#include <limits>
#include <stdexcept>
#include <regex>
using namespace std;

void frontPage ();
void signUp (string accounts[][8], int number_of_accounts);
void newInfo(string accounts[][8], int number_of_accounts, string returnChangeInfo);
void bankNumberAndEnterPin (string accounts[][8], int number_of_accounts);
void displayAll(string accounts[][8], int number_of_accounts);
void messagePreparation ();
void showPersonalDetails(string accounts[][8], int number_of_accounts);
void transactionCancelled(string accounts[][8], int number_of_accounts);
string ageValidationMessage();
string changeInfo ();
string confirmation(string accounts[][8], int number_of_accounts);
string dataPrivacy();
string confirmDeleteAccount();
string confirmProceed();



int main () {
    char userInput;
    string returnChangeInfo, returnConfirmation, returnConfirmationDeletion, returnAgeValidationMessage, returnConfirmProceed;
    int number_of_accounts = 0;
    int maximum_accounts = 100;
    string accounts[maximum_accounts][8];

    do {
        system("cls");
        frontPage();
        cin >> userInput;
        if (userInput == '1') {

        } else if (userInput == '2') {
            returnAgeValidationMessage = ageValidationMessage();
            if (returnAgeValidationMessage == "1") {
                    if (dataPrivacy() == "1") {
                        messagePreparation();
                        signUp (accounts, number_of_accounts);
                        do {
                            showPersonalDetails(accounts, number_of_accounts);
                            returnConfirmation = confirmation(accounts, number_of_accounts);
                            if (returnConfirmation == "1") {
                                showPersonalDetails(accounts, number_of_accounts);
                                returnChangeInfo = changeInfo();
                                if (returnChangeInfo == "6") {
                                    signUp (accounts, number_of_accounts);
                                    showPersonalDetails(accounts, number_of_accounts);
                                } else if (returnChangeInfo == "7") {
                                    returnConfirmProceed = confirmProceed();
                                    if (returnConfirmProceed == "1"){
                                        bankNumberAndEnterPin(accounts, number_of_accounts);
                                        displayAll(accounts, number_of_accounts);
                                        number_of_accounts++;
                                        break;
                                    } 

                                } else if (returnChangeInfo == "8") {
                                    returnConfirmationDeletion = confirmDeleteAccount();

                                    if (returnConfirmationDeletion == "1") {
                                        transactionCancelled(accounts, number_of_accounts);
                                        break;
                                    } 
                                } else {
                                    newInfo (accounts, number_of_accounts, returnChangeInfo);
                                    do {
                                        showPersonalDetails(accounts, number_of_accounts);
                                        returnConfirmation = confirmation(accounts, number_of_accounts);
                                        if (returnConfirmation == "1") {
                                            showPersonalDetails(accounts, number_of_accounts);
                                            returnChangeInfo = changeInfo();
                                            if (returnChangeInfo == "6") {
                                                signUp (accounts, number_of_accounts);
                                                showPersonalDetails(accounts, number_of_accounts);       
                                            } else if (returnChangeInfo == "7") {
                                                returnConfirmProceed = confirmProceed();
                                                if (returnConfirmProceed == "1"){
                                                    bankNumberAndEnterPin(accounts, number_of_accounts);
                                                    displayAll(accounts, number_of_accounts);
                                                    number_of_accounts++;
                                                    break;
                                                } 
                                            } else if (returnChangeInfo == "8") {
                                                returnConfirmationDeletion = confirmDeleteAccount();

                                                if (returnConfirmationDeletion == "1") {
                                                    transactionCancelled(accounts, number_of_accounts);
                                                    break;
                                                } 
                                            } else {
                                                newInfo(accounts, number_of_accounts, returnChangeInfo);
                                                showPersonalDetails(accounts, number_of_accounts);
                                            }

                                        } else if (returnConfirmation == "2") {
                                           returnConfirmProceed = confirmProceed();
                                            if (returnConfirmProceed == "1"){
                                                bankNumberAndEnterPin(accounts, number_of_accounts);
                                                displayAll(accounts, number_of_accounts);
                                                number_of_accounts++;
                                                break;
                                            } 
                                        } else if (returnConfirmation == "3") {
                                            returnConfirmationDeletion = confirmDeleteAccount();
                                            if (returnConfirmationDeletion == "1") {
                                                transactionCancelled(accounts, number_of_accounts);
                                                break;
                                            }
                                        }
                                    } while (true);
                                    break;
                                }
                            } else if (returnConfirmation == "2") {
                                returnConfirmProceed = confirmProceed();
                                if (returnConfirmProceed == "1"){
                                    bankNumberAndEnterPin(accounts, number_of_accounts);
                                    displayAll(accounts, number_of_accounts);
                                    number_of_accounts++;
                                    break;
                                } 
                            } else if (returnConfirmation == "3") {
                                returnConfirmationDeletion = confirmDeleteAccount();

                                if (returnConfirmationDeletion == "1") {
                                    transactionCancelled(accounts, number_of_accounts);
                                    break;
                                } 
                            }
                        } while (returnConfirmationDeletion == "2" || returnChangeInfo == "6" || returnConfirmProceed == "2");
                    }
                } else {
                    continue;
                }
        } else if (userInput == '3'){
            break;
        } else {
            cout << "Invalid Input";
        }
    } while (true);

    return 0;
}

//First Page of the System
void frontPage () {
    cout << "*************************************************************************\n";
    cout << "*                                                                       *\n";
    cout << "*                       BANGKO SENTRAL NI EDSELL (BSE)                  *\n";
    cout << "*                                                                       *\n";
    cout << "*************************************************************************\n";
    cout << "*                                                                       *\n";
    cout << "*                        [1] Log in                                     *\n";
    cout << "*                        [2] Create Bank Account                        *\n";
    cout << "*                        [3] Exit                                       *\n";
    cout << "*                                                                       *\n";
    cout << "*************************************************************************\n";
    cout << "Your Choice: ";
} 

//Sign up ng personal info

//If user wants to change info
string changeInfo () {
    string userInput;
        cout << "*************************************************************************\n";
        cout << "*                                                                       *\n";
        cout << "*                          CHANGE INFORMATION                           *\n";
        cout << "*                                                                       *\n";
        cout << "*************************************************************************\n";
        cout << "*                                                                       *\n";
        cout << "*                         [1] Change Name                               *\n";
        cout << "*                         [2] Change Age                                *\n";
        cout << "*                         [3] Change Sex                                *\n";
        cout << "*                         [4] Change Address                            *\n";
        cout << "*                         [5] Change Email Address                      *\n";
        cout << "*                         [6] Change All Infomation                     *\n";
        cout << "*                         [7] Continue With Current Information         *\n";
        cout << "*                         [8] Cancel Transaction                        *\n";
        cout << "*                                                                       *\n";
        cout << "*************************************************************************\n";

    do {

        cout << "Enter Your Choice: ";
        cin >> userInput;


        if (userInput != "1" && userInput != "2" && userInput != "3" && userInput != "4" && userInput != "5" && userInput != "6" && userInput != "7" && userInput != "8") {
            cout << "Invalid Input \n";
        } else {
            break;
        }
    } while (true);
    return userInput;
}

//Dito kung saan mag eenter yung user ng new info
void newInfo(string accounts[][8], int number_of_accounts, string returnChangeInfo) {
    bool ageValidation = false;
    const regex emailPattern ("(\\w+)(\\.|_)?(\\w*)@(\\w+)(\\.(\\w+))+");

        if (returnChangeInfo == "1") {
           do {
                cout << "Enter Name: ";
                getline (cin >> ws, accounts[number_of_accounts][0]);
                if (accounts[number_of_accounts][0].length() < 10) {
                    cout << "Enter atleast 10 characters \n";
                }
            } while (accounts[number_of_accounts][0].length() < 10);
            transform (accounts[number_of_accounts][0].begin(), accounts[number_of_accounts][0].end(), accounts[number_of_accounts][0].begin(), ::toupper);
        } else if (returnChangeInfo == "2") {

                do {
                    cout << "Enter Age: ";
                    getline (cin >> ws, accounts[number_of_accounts][1]);
                    try {
                        int age_input = stoi(accounts[number_of_accounts][1]);
                        
                        if (age_input < 18 || age_input > 65) {
                            cout << "Age must be between 18 and 65 \n";
                        } else {
                            ageValidation = true;
                        }
                } catch (const invalid_argument& e) {
                    cout << "Age must be between 18 and 65 \n";                
                }
            } while (!ageValidation);
        } else if (returnChangeInfo == "3") {
            do {
                cout << "Enter Sex (MALE/FEMALE): ";
                getline (cin >> ws, accounts[number_of_accounts][2]);
                transform (accounts[number_of_accounts][2].begin(), accounts[number_of_accounts][2].end(), accounts[number_of_accounts][2].begin(), ::toupper);
                if (accounts[number_of_accounts][2] == "MALE" || accounts[number_of_accounts][2] == "FEMALE") {
                    break;
                } else {
                    cout << "\"MALE\" or \"FEMALE\" ONLY \n";
                }
            } while (true);
        } else if (returnChangeInfo == "4") {
            do {
                cout << "Enter Adress: ";
                getline (cin >> ws, accounts[number_of_accounts][3]);
                transform (accounts[number_of_accounts][3].begin(), accounts[number_of_accounts][3].end(), accounts[number_of_accounts][3].begin(), ::toupper);
                if (accounts[number_of_accounts][3].length() < 10) {
                    cout << "Must be atleast TEN (10) characters\n";
                } else {
                    break;
                }
            } while (true);

        } else if (returnChangeInfo == "5") {
            do {
                cout << "Enter Email Address: ";
                getline (cin >> ws, accounts[number_of_accounts][4]);
                transform (accounts[number_of_accounts][4].begin(), accounts[number_of_accounts][4].end(), accounts[number_of_accounts][4].begin(), ::toupper);
                if (!regex_match(accounts[number_of_accounts][4], emailPattern)) {
                    cout << "Enter a valid email adress (name@gmail.com) \n";
                }
            } while (!regex_match(accounts[number_of_accounts][4], emailPattern));
        }

}

//papakita na yung bank acc number tas mag enter pin
void bankNumberAndEnterPin (string accounts[][8], int number_of_accounts) {
    int count = 0;
    string pin, realPin, confirmPin, bankAccountNumber;
    bool pinValidation = false;
    
    system("cls");
    srand(time(0));

    for (int i = 1; i <= 19; i++) {
        if (i == 5 || i == 10 || i == 15) {
            bankAccountNumber += " ";
        } else {
            int randomNum = rand() % 9;
            bankAccountNumber += to_string(randomNum);
        }
    }   
    accounts[number_of_accounts][5] = bankAccountNumber; 




        do {
            system("cls");
            cout << "********************************************************************************\n";
            cout << "*                                                                              *\n";
            cout << "*                Your Bank Account Number is: " << bankAccountNumber << "              *\n";
            cout << "*                                                                              *\n";
            cout << "********************************************************************************\n";
            cout << "\nEnter a 6 numbers pin: ";
            cin >> pin;
            
            if (pin.length() == 6) {
                break;
            } else {
                cout << "INVALID INPUT. Enter a 6 numbers pin \n";
            }
        } while (true);



        do {
            cout << "Re-enter PIN for confirmation: ";
            cin >> confirmPin;

            if (confirmPin != pin) {
                cout << "Your PIN Does not match to your input\n";
            } else {
                accounts[number_of_accounts][6] = pin;
                break;

            }
        } while (true);
}

// Pa confirm kung tama na lahat ng details
string confirmation (string accounts[][8], int number_of_accounts) {
    string userInput;
    do { 
        showPersonalDetails(accounts, number_of_accounts);
        cout << "*************************************************************************\n";
        cout << "*                                                                       *\n";
        cout << "*                        WHAT DO YOU WANT TO DO NEXT?                   *\n";
        cout << "*                                                                       *\n";
        cout << "*************************************************************************\n";
        cout << "*                                                                       *\n";
        cout << "*                         [1] Change Information                        *\n";
        cout << "*                         [2] Proceed                                   *\n";
        cout << "*                         [3] Cancel Transaction                        *\n";
        cout << "*                                                                       *\n";
        cout << "*************************************************************************\n";
        cout << "Your Choice: ";
        cin >> userInput;
        system("cls");
        if (userInput == "1" || userInput == "2" || userInput == "3") {
            break;
        } else {
           cout << "Invalid Input. Please enter 1, 2, or 3 only \n";
        }
    } while (true);

    return userInput;

}

//papakita lahat ng info. para toh sa pagtapos mag enter ng user ng enter pin
void displayAll (string accounts[][8], int number_of_accounts) {
    system("cls");
    cout << "*************************************************************************\n";
    cout << "*                                                                       *\n";
    cout << "*                          YOUR PERSONAL INFORMATION                    *\n";
    cout << "*                                                                       *\n";
    cout << "*************************************************************************\n";
    cout << "                   Name: " << accounts[number_of_accounts][0] << "\n";
    cout << "                   Age: " << accounts[number_of_accounts][1] << "\n";
    cout << "                   Sex: " << accounts[number_of_accounts][2] << "\n";
    cout << "                   Address: " << accounts[number_of_accounts][3] << "\n";
    cout << "                   Email Address: " << accounts[number_of_accounts][4] << "\n";
    cout << "                   Bank Account Number: " << accounts[number_of_accounts][5] << "\n";
    cout << "                   Pin: " << accounts[number_of_accounts][6] << "\n";
    cout << "*************************************************************************\n\n";

    cout << "You succesfully created a bank account " << accounts[number_of_accounts][0] << ", You may now log in\n";
    cout << "PRESS ANY KEY TO CONTINUE: ";

    getch();
}

//message lang sa data privacy
string dataPrivacy() {
    string userInput;

    system("cls");

        cout << "**************************************************************************************************************************************\n";
        cout << "*                                                                                                                                    *\n";
        cout << "*                                                     TERMS AND CONDITIONS                                                           *\n";
        cout << "*                                                                                                                                    *\n";
        cout << "**************************************************************************************************************************************\n";
        cout << "*                                                                                                                                    *\n";
        cout << "*                              To create your account, we will need some personal information such as your name, age,                *\n";
        cout << "*                           and contact details. This information will be securely stored and used only for the purpose of           *\n";
        cout << "*                           managing your account and providing our services.                                                        *\n";
        cout << "*                                                                                                                                    *\n";
        cout << "*                              By proceeding, you agree to our terms and conditions, as well as our privacy policy, which explains   *\n";
        cout << "*                           how we collect, use, and protect your personal data.                                                     *\n";
        cout << "*                                                                                                                                    *\n";
        cout << "*                           Do you agree to provide this information and proceed with account creation?                              *\n";
        cout << "*                                                                                                                                    *\n";
        cout << "*                                                     [1] I AGREE                                                                    *\n";
        cout << "*                                                     [2] I DO NOT AGREE                                                             *\n";
        cout << "*                                                                                                                                    *\n";
        cout << "**************************************************************************************************************************************\n";

        do {

            cout << "Enter Choice: ";
            cin >> userInput;

             if (userInput != "1" && userInput != "2") {
                cout << "INVALID INPUT! ENTER 1 AND 2 ONLY \n";
             } else {
                break;
             }

        } while (true);

    system("cls");

    return userInput;
}
void messagePreparation () {
    cout << "************************************************************************************************************\n";
    cout << "*                                                                                                          *\n";
    cout << "*            Before proceeding on creating your BANK ACCOUNT, prepare for informations such as:            *\n";
    cout << "*                                                                                                          *\n";
    cout << "*                                          [1] Name                                                        *\n";
    cout << "*                                          [2] Age                                                         *\n";
    cout << "*                                          [3] Sex                                                         *\n";
    cout << "*                                          [4] Address                                                     *\n";
    cout << "*                                          [5] Email Address                                               *\n";
    cout << "*                                                                                                          *\n";
    cout << "************************************************************************************************************\n";
    cout << "Press Any Key if you are now prepared: ";
    getch();
}
string confirmDeleteAccount() {
    string userInput;
    system("cls");
        cout << "************************************************************************************************************\n";
        cout << "*                                                                                                          *\n";
        cout << "*             Are you sure you want to cancel transaction? Canceling the transaction will delete all       *\n";
        cout << "*             your personal information that you entered. Do you want to continue canceling?               *\n";
        cout << "*                                                                                                          *\n";
        cout << "*                                      [1] Yes, Cancel Transaction                                         *\n";
        cout << "*                                      [2] No, Restore Transaction                                         *\n";
        cout << "*                                                                                                          *\n";
        cout << "************************************************************************************************************\n";

        do {
            cout << "Enter Your Choice: ";
            cin >> userInput;

            if (userInput == "1" || userInput == "2") {
                break;
            } else {
                cout << "Enter 1 or 2 only \n";
            }
        } while (true);
        system("cls");

        return userInput;
}
void showPersonalDetails (string accounts[][8], int number_of_accounts) {
    system("cls");
    cout << "*************************************************************************\n";
    cout << "*                                                                       *\n";
    cout << "*                      FILL OUT THE REGISTRATION DETAILS                *\n";
    cout << "*                                                                       *\n";
    cout << "*************************************************************************\n";
    cout << "                                                                         \n";
    cout << "                   Name: " << accounts[number_of_accounts][0] << "\n";
    cout << "                   Age: " << accounts[number_of_accounts][1] << "\n";
    cout << "                   Sex: " << accounts[number_of_accounts][2] << "\n";
    cout << "                   Address: " << accounts[number_of_accounts][3] << "\n";
    cout << "                   Email Address: " << accounts[number_of_accounts][4] << "\n";
    cout << "                                                                         \n";
    cout << "*************************************************************************\n";
}
void signUp (string accounts[][8], int number_of_accounts) {
    bool ageValidation = false;
    const regex emailPattern ("(\\w+)(\\.|_)?(\\w*)@(\\w+)(\\.(\\w+))+");

    
    showPersonalDetails (accounts, number_of_accounts);
    do {
        cout << "Enter Name: ";
        getline (cin >> ws, accounts[number_of_accounts][0]);
        if (accounts[number_of_accounts][0].length() < 10) {
            cout << "Enter atleast 10 characters \n";
        }
    } while (accounts[number_of_accounts][0].length() < 10);

    transform (accounts[number_of_accounts][0].begin(), accounts[number_of_accounts][0].end(), accounts[number_of_accounts][0].begin(), ::toupper);

    showPersonalDetails (accounts, number_of_accounts);
    do {
        cout << "Enter Age: ";
        getline (cin, accounts[number_of_accounts][1]);
        
        try {
            int age_input = stoi(accounts[number_of_accounts][1]);
            
            if (age_input < 18 || age_input > 65) {
                cout << "Must be atleast 18 years old\n";
            } else {
                ageValidation = true;
            }
        } catch (const invalid_argument& e){
            cout << "Must be at least 18 years old \n";
        }

    } while (!ageValidation);

    showPersonalDetails (accounts, number_of_accounts);

    do {
        cout << "Enter Sex (MALE/FEMALE): ";
        getline (cin, accounts[number_of_accounts][2]);
        transform (accounts[number_of_accounts][2].begin(), accounts[number_of_accounts][2].end(), accounts[number_of_accounts][2].begin(), ::toupper);
            if (accounts[number_of_accounts][2] == "MALE" || accounts[number_of_accounts][2] == "FEMALE") {
                break;
            } else {
                cout << "\"MALE\" or \"FEMALE\" ONLY \n";
            }
    } while (true);

    showPersonalDetails (accounts, number_of_accounts);
    do {
        cout << "Enter Address: ";
        getline (cin, accounts[number_of_accounts][3]);
        transform (accounts[number_of_accounts][3].begin(), accounts[number_of_accounts][3].end(), accounts[number_of_accounts][3].begin(), ::toupper);
        if (accounts[number_of_accounts][3].length() < 10) {
            cout << "Must be atleast TEN (10) characters\n";
        } else {
            break;
        }
    } while (true);


    showPersonalDetails (accounts, number_of_accounts);

    do {
        cout << "Enter Email Address: ";
        getline (cin, accounts[number_of_accounts][4]);
        transform (accounts[number_of_accounts][4].begin(), accounts[number_of_accounts][4].end(), accounts[number_of_accounts][4].begin(), ::toupper);

        if (!regex_match(accounts[number_of_accounts][4], emailPattern)) {
            cout << "Enter a valid email adress (name@gmail.com) \n";
        }
    } while (!regex_match(accounts[number_of_accounts][4], emailPattern));

}
void transactionCancelled(string accounts[][8], int number_of_accounts) {
        accounts[number_of_accounts][0] = " ";
        accounts[number_of_accounts][1] = " ";
        accounts[number_of_accounts][2] = " ";
        accounts[number_of_accounts][3] = " ";
        accounts[number_of_accounts][4] = " ";

        cout << "************************************************************************************************************************\n";
        cout << "*                                                                                                                      *\n";
        cout << "*              Transaction Canceled. Rest assured that All PERSONAL INFORMATION that you entered was deleted.          *\n";
        cout << "*                                                                                                                      *\n";
        cout << "************************************************************************************************************************\n";
        cout << "Press any key to continue: ";
        getch();
}
string ageValidationMessage() {
    string userInput;
    system("cls");

    cout << "**************************************************************************************************************\n";
    cout << "*                                                                                                            *\n";
    cout << "*   In order to create a bank account, you must meet the legal requirement of being at least 18 years old.   *\n";
    cout << "*   Please Confirm: Are you 18 years old or older?                                                           *\n";
    cout << "*                                                                                                            *\n";
    cout << "*                                          [1] Yes, I am at least 18 years old                               *\n";
    cout << "*                                          [2] No, I am not                                                  *\n";
    cout << "*                                                                                                            *\n";
    cout << "**************************************************************************************************************\n";

    do {
        cout << "Enter Your Choice: ";
        cin >> userInput;

        if (userInput == "1" || userInput == "2") {
            break;
        } else {
            cout << "Enter [1] YES or [2] NO ONLY \n";
        }
    } while (true);
    system("cls");
    if (userInput == "1") {
        cout << "*******************************************************\n";
        cout << "*                                                     *\n";
        cout << "*      You are eligible to create a bank account!     *\n";
        cout << "*                                                     *\n";
        cout << "*******************************************************\n";
        cout << "Press any key to continue to the registration proccess: ";
        getch();
    } else {
        cout << "*******************************************************************************\n";
        cout << "*                                                                             *\n";
        cout << "*      We apologize, but you are not of legal age to create a bank account.   *\n";
        cout << "*      Please try again next time. Thank You.                                 *\n";
        cout << "*                                                                             *\n";
        cout << "*******************************************************************************\n";
        cout << "Press any key to go back to the front page: ";
        getch();
    }

    return userInput;
}
string confirmProceed() {
    string userInput;
    system("cls");

        cout << "************************************************************************************************************\n";
        cout << "*                                                                                                          *\n";
        cout << "*     Are you sure you want to proceed? By continuing, your personal information will be securely saved,   *\n";
        cout << "*     and your bank account number will be generated. You will then be asked to create a 6-digit PIN for   *\n";
        cout << "*     your account.                                                                                        *\n";
        cout << "*                                                                                                          *\n";
        cout << "*     Please Confirm: Do you want to proceed?                                                              *\n";
        cout << "*                                                                                                          *\n";
        cout << "*                                      [1] Yes, Proceed.                                                   *\n";
        cout << "*                                      [2] Go Back.                                                        *\n";
        cout << "*                                                                                                          *\n";
        cout << "************************************************************************************************************\n";     

        do {
            cout << "Enter Your Choice: ";
            cin >> userInput;

            if (userInput == "1" || userInput == "2") {
                break;
            } else {
                cout << "Enter 1 or 2 only, Thank you! \n";
            }
        } while (true);

    return userInput;
}

