# cs300prgm1
//cs300, program1
//This program creates a part list and allows a user to print, create, modify parts and print a total.


#include <string>
#include <iostream>
#include <fstream>
using namespace std;


class Part //creates a Part class for our program
{
public:
  int part_number;    //From 1 to 100
  string description;   //Allows spaces
  int quantity;
  float price_per_item;
};

void printAllParts(Part [], int);
void addPart(Part [], int&);



int main() //Begin main function
{
  //big data structure: array of size 100
    Part arr[100]; //This is the array to hold objects.
    int count = 0; //Count to tell how many different parts in array.

    std::fstream file("inventory.txt", std::ios::in);
    if(file)
    	{
        int i = 0;
    		int part_number = 0;
    		std::string description = "";
    		int quantity = 0;
    		float unitPrice = 0;

    		// use a loop to keep reading file.
    		// if reading file fails, the loop will end
    		while(file >> part_number)
    		{
    			//
    			file.ignore();
    			std::getline(file, description);
    			file >> quantity;
    			file >> unitPrice;


          arr[i].part_number = part_number;
          arr[i].description = description;
          arr[i].quantity = quantity;
          arr[i].price_per_item = unitPrice;
          i++;
          count++;

    		}
    	}
    	else
    	{
    		std::cout<<"Error when reading from file \"inventory.txt\""<<std::endl;
    	}

    	// close file when done
    	file.close();


    int choice = 0;                       //Creates a table of choices for user
    cout<<"Welcome to Tiny Part Mgmt!"<<endl;
    cout<<"**************************"<<endl<<endl;
    cout<<"1. Print the Part"<<endl;
    cout<<"2. Create a Part"<<endl;
    cout<<"3. Modify a Part"<<endl;
    cout<<"4. Print Total"<<endl;
    cout<<"5. Exit the Program"<<endl<<endl;
    cout<<"Please make a choice: ";
    cin>>choice;

    while (cin.good() && choice != 5) //Switch case to process user choice
    {
      switch (choice){
        case 1:
        printAllParts(arr, count);
        cout<<"Print the part"<<endl;
        break;
        case 2:
        cin.ignore();
        addPart(arr, count);
        cout<<"Create a Part"<<endl;
        break;
        case 3:
        cout<<"Modify a Part"<<endl;
        break;
        case 4:
        cout<<"Print Total"<<endl;
        break;
        default:
        cout<<"Invalid Choice"<<endl;
      }
      cout<<"Dear user please make a choice: ";
      cin>>choice;


    }
    return 0;
}

void printAllParts(Part arr[], int count) //Function to print all parts
{
  for (int i = 0; i < count; i++)
  {
    cout<<"Part Number: "<<arr[i].part_number<<endl;
    cout<<"Description: "<<arr[i].description<<endl;
    cout<<"Quantity: "<<arr[i].quantity<<endl;
    cout<<"Unit Price: "<<arr[i].price_per_item<<endl;
  }
}

void addPart(Part arr[], int & count) //Function to add parts to a .txt file
{
  cout<<"New Part description: ";
  string desc;
  getline(cin, desc);


  cout<<"New Part Quantity: ";
  int quantity = 0;
  cin>>quantity;

  cout<<"New Part Unit Price: ";
  float price = 0;
  cin >> price;

  arr[count].part_number = count + 1;
  arr[count].description = desc;
  arr[count].quantity = quantity;
  arr[count].price_per_item = price;
}


//Save data to inventory.txt here
