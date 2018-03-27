# String-of-102s
This project will sort an input of 1s,0s, and 2s in the order of 102 and will display the output. Each digit can only be evaluated once. No extra space can be used (i.e. pointers). You cannot simply count each occurrence of 1s, 0s, and 2s. 
#include <iostream>
#include <cstring>
#include<string>
using namespace std;

void StringtointArray(string s, int l,  int a[]);
bool ValidInput(int a[], int l);
void SWAP(int a[], int i, int j);
void Sort_102(int a[], int l);

int main()
{
        //variable to take users choice
        char choice;

        cout << "Hello! Welcome to our first programming project of the semester for CISC 2200. In this program, the user, you, will be entering a string of digits containing the numbers 0, 1, and 2. Once the digits are entered, our program will transfer your digits into an array. Next, the program will parse through the array to make sure that the input is valid (i.e. there are no other entries besides 0, 1, and 2). If the array is invalid, the program will quit. If the array is valid, the program will continue and  the combination of our functions, Sort_102 and SWAP, will rearrange your array and put it in the order of 1's, 0's, and 2's. Would you like to test it out? ";
        cin >> choice;

        //if then else statement depending on whether the user says they want to test it out or not
        if(choice == 'Y' or choice == 'y')
        {
                //variable to take users input
                string sdigits;

                //taking users input
                cout << "Please enter a string containing only the digits 0, 1, and 2 :";
                cin.ignore();
                getline(cin, sdigits);

                //variable for the size of the array depending on the users input and the array to store the input in
                int length = sdigits.length(), digits[length];

                //call to function to convert string into array
                StringtointArray(sdigits, length, digits);

                //output the users original array and the size of it
                cout << "Your input is : ";
                for(int i = 0; i < length; i++)
                {
                        cout << digits[i];
                }
                cout << endl;

                //output of the size of the array
                cout << "The size of your array is : " << length << endl;

                //call to function to check if the input is valid, if it is, the program continues, if not, it will exit
                if(ValidInput(digits, length))
                {
                        cout << "Your input is valid! The program will continue." << endl;
                }
                else
                {
                        cout << "Invalid input. Program will now end." << endl;
                        exit(1);
                }

                //call to sorting function
                Sort_102(digits, length);

                //output of sorted array
                cout <<"Your sorted array is : ";
                for(int i = 0; i < length; i++)
                {
                        cout << digits[i];
                }

                cout << endl;
        }
        //exit program if choice is no
        else if(choice == 'N' or choice == 'n')
        {
                cout << "Thank you, have a nice day!" << endl;
        }
        //exit program if choice is invalid
        else
        {
                cout << "Invalid choice. Goodbye!" << endl;
        }

        return 0;
}

//function that converts string to array
void StringtointArray(string s, int l, int a[])
{
        //for loop to parse through the array to add the string at each index into it
        for(int i = 0; i < l; i++)
        {
                        a[i] = s.at(i) - '0'; //https://stackoverflow.com/questions/14543129/store-a-string-to-integer-arra
        }
}

//boolean function to check if string input is valid
bool ValidInput(int a[], int l)
{
        bool isValid;
        for(int i = 0; i < l; i++)
        {
                if(a[i] == 0 or a[i] == 1 or a[i] == 2)
                {
                        isValid = true;
                }
                else
                {
                        isValid = false;
                }
        }
        //returns true if string is valid, false if not
        return isValid;
}

//function to swap the array at two passed in indices
void SWAP(int a[], int i, int j)
{
        int temp;
        temp = a[i];
        a[i] = a[j];
        a[j] = temp;
        cout << "Swapped" << endl;
}

// sorting function
void Sort_102(int a[], int l)
{
        //variables to parse through the array, keep track of the next place a 1 should go, and the next place a 2 should go
        int counter = 0, index1 = 0, index2 = (l-1);

        //while loop to parse through array
        while(index1 < index2 and counter < l and counter<index2)
        {
        //      for (int i=0; i<l;i++)
        //      {
        //              cout <<a[i];
        //      }
        //              cout << endl;

                if(a[counter] == 0)
                {
                        counter++;
                }
                if(a[counter] == 1 and counter >= index1)
                {
                        if(a[index1] != 1)
                        {
                                SWAP(a, index1, counter);
                        }
                        else if(a[index1]== 1 and a[index1+1] != 1)
                        {
                                counter++;
                        }
                        else
                        {
                                counter++;
                        }
                }
                else if(a[counter] == 2)
                {
                        if(a[index2] != 2)
                                                                                                                              
                        {
                                SWAP(a, index2, counter);
                                counter--;
                        }
                        else if(a[index2-1] != 2)
                        {
                                SWAP(a, index2-1, counter);
                        }
                        else
                        {
                                counter++;
                        }
                }
                if (a[index1] == 1)
                {
                        index1++;
                }
                if(a[index2] == 2)
                {
                        index2--;
                }
        }
}
