//# Spyder-s-Carwash

#include <iostream>
#include <iomanip>
#include <string>
#include <cmath>
#include <fstream>

 using namespace std;
//prototypes for functions
 int getpackage(string[],const int);
void showDetails();
void getfeatures(double[],string[], const double [], const int,int);
void reset(double[],double[],bool);


 int main()

 {
   //variables for user's name, array sizes
   //to transfer price values into carwash array and features array
   string user;
   const int pSize = 6, fSize= 5;
double packagePrice,subTotal,tax =.08,totalTax,total; // 8% tax rate
int packageNumber;
bool SuvAdd = false;



   // These are the Arrays for the Funtion holding
   // the costs  for features and for the carwash packages
   // starting them at zero as a null indicator

double carwashPackage [6] = {0,0,0,0,0,0};
double addFeatures[5] = {0,0,0,0,0,};
   // here are all the prices for the carwash items
   //p are the carwash packages and f is for add features
    
const double washPrices [6]= {6.99, 12.99,16.99, 25.99, 45.99, 55.99};
const double featurePrices[5] ={ 3.00, 1.50, 2.00, 24.00, 24.00};
const double SUVadder [6]= {3.0,3.0,3.0,7.0,7.0,7.0};


// these will be the strings for each item feature, and string for //  each package
string packageTitles[pSize] = { "Hand Wash", "Inside Out Wash", "Deluxe Wash", "Hand Wax Express", "Interior Express", "Ultimate"};
string featureTitles[fSize] = { "Tire Dressing", "Air Fragrance", "Clean Rubber Mats", "Shampoo and Hot Water Carpet", "Shampoo and Hot Water Seat"};

option:  //This option is coming from the Reset Function

//get their name
 
cout<< "What is your Name? (First name only)";
cin>> user;
cout<<"\nHello "<<user<<",\nWelcome to Spyder’s CarWash\n"<<endl;


//Go to getpackage function and get User's carwash choice
 packageNumber= getpackage (packageTitles,pSize);
 
//get and display package choice with SUV information
char suv;
cout<<"\n\nIs the Vehicle a Large SUV or Full Size Truck? (Y/N) "<<endl;
cin>> suv;
if (suv == 'y' || suv == 'Y')
{
cout<< " Okay, Large SUV or Full Size Truck\n";
carwashPackage[packageNumber] = washPrices[packageNumber] + SUVadder[packageNumber];
SuvAdd= true; 
}
else 
{
  cout<<" Okay, Regular size vehicle.\n";
  carwashPackage[packageNumber] = washPrices[packageNumber] ;
}
packagePrice=carwashPackage[packageNumber];
//display Carwash Package price after SUV validation
cout<< "Your Carwash Package price is : "<<packagePrice<<endl;


cout<<"\nNext we are going to go over some of the Add-On Features \nyou can get with your Carwash.\n\n";
  cout<<"\n\t\t\t\tPress Enter to see Add-On Features>>>";
  cin.get();  // PAUSE
    cin.get();// PAUSE
//Go to getfeatures function and get User's carwash Add-Ons
getfeatures(addFeatures,featureTitles, featurePrices,fSize,packageNumber);

cout<<"\n\nGreat! This is your Receipt\n\n"; 
 //finsih up with a Receipt Print
cout << fixed << showpoint << setprecision(2);


cout<< "**************************************************\n";
cout<< "***              Spyder’s CarWash              ***\n";
cout<< "**************************************************\n\n";
cout<<"Receipt\n";
cout<<"==================================================\n";
cout<<"Carwash for:  "<<user<<endl;  // Display user name
 cout<<"--------------------------------------------------\n";

cout<<"Carwash Package:\n\t";
if (SuvAdd)  //if statement to display SUV 
 cout<<"    +Large SUV or Full Size Truck\n\t";
cout<<packageTitles[packageNumber]<< "\t"<<packagePrice; 
 cout<<"\n\nExtra Features:"<<endl;
 //for loop to show each feature, excluding any that are hold null
 for (int count= 0; count < fSize; count++) 
 {
   if(addFeatures[count]!=0)
   {
   cout<<"\t"<<featureTitles[count]<<"\t"<<featurePrices[count]<<endl;
subTotal += addFeatures[count];
   }
 }
subTotal +=packagePrice;    //caluculate math for totals and taxes
totalTax= subTotal*tax ;
total = subTotal + totalTax;

//Display totals and taxes
 cout<<"--------------------------------------------------\n";
cout<<"\nSubTotal\t\t\t\t\t\t\t\t\t "<<subTotal<<endl;
cout<<"Tax\t\t\t\t\t\t\t\t\t\t\t  "<<totalTax<<endl;
cout<<"--------------------------------------------------\n";
cout<<"Total\t\t\t\t\t\t\t\t\t\t "<< total<<endl;
cout<<"==================================================\n";


//Lastly confirm order
bool done = false;
char confirm,confirm2;

do
{


cout<<"\n\nPress Y to Confirm this order:\nPress N to Restart your entire order:"<<endl;
cin>>confirm;
if(confirm == 'n'|| confirm == 'N')
  {
    cout<<"\nAre you sure you want to Restart your entire order:(Y/N)"<<endl;
      cin>>confirm2;
     if(confirm2 == 'y'|| confirm2 == 'Y')
     {
       cout<<"Okay, no problem.\nPlease only select items you would like for\nyour carwash on this order.\nPress Enter to Continue****";
       cin.get();
       reset (carwashPackage,addFeatures,SuvAdd);
       total=0,packagePrice=0,subTotal=0,totalTax=0;
       SuvAdd = false;

       goto option;
     }
  }
  else 
  done=true;
} 
while (!(done));

//The following is all the code for the Receipt except for 
//the math calculations that have already been made.
//this Receipt code will be transfer to text file named: Receipt

 ofstream outputfile;
  outputfile.open("Receipt.txt");




outputfile << fixed << showpoint << setprecision(2);


outputfile<< "**************************************************\n";
outputfile<< "***              Spyder’s CarWash              ***\n";
outputfile<< "**************************************************\n\n";
outputfile<<"Receipt\n";
outputfile<<"==================================================\n";
outputfile<<"Carwash for:  "<<user<<endl;  // Display user name
 outputfile<<"--------------------------------------------------\n";

outputfile<<"Carwash Package:\n\t";
if (SuvAdd)  //if statement to display SUV 
 outputfile<<"    +Large SUV or Full Size Truck\n\t";
outputfile<<packageTitles[packageNumber]<< "\t"<<packagePrice; 
 outputfile<<"\n\nExtra Features:"<<endl;
 //for loop to show each feature, excluding any that are hold null
 for (int count= 0; count < fSize; count++) 
 {
   if(addFeatures[count]!=0)
   {
   outputfile<<"\t"<<featureTitles[count]<<"\t"<<featurePrices[count]<<endl;

   }
 }


//Display totals and taxes
 outputfile<<"--------------------------------------------------\n";
outputfile<<"\nSubTotal\t\t\t\t\t\t\t\t\t "<<subTotal<<endl;
outputfile<<"Tax\t\t\t\t\t\t\t\t\t\t\t  "<<totalTax<<endl;
outputfile<<"--------------------------------------------------\n";
outputfile<<"Total\t\t\t\t\t\t\t\t\t\t "<< total<<endl;
outputfile<<"==================================================\n";


 outputfile<<  "Thank You, Please come again";

outputfile.close();


//Program Complete 
   return 0;
 }

//getpackage function to get carwash number from user
int getpackage(string ray[], const int p)
{
  // t will hold and return the user's package choice
int t;
bool leave = false;
char letter='d';
//show all package brief
 
  
  cout<< " \n                Car Wash Packages          ";  
  cout<< "\n--------------------------------------------------\n"; 
  cout<< "        1                 2                3   \n"; 
  cout<< "    Hand Wash       Inside and Out     Deluxe Wash    \n";
    cout<< "   $6.99/$9.99      $12.99/$15.99    $16.99/$19.99    \n\n";
  cout<< "        4                 5                6   \n"; 
  cout<< "Hand Wax Express    Interior Express     Ultimate    \n";
    cout<< " $25.99/$32.99       $45.99/$52.99     $55.99/$62.99    \n\n";
    cout<< "\t\t\t     Regular Car Price / \n\t\tLarge SUV and Full Size Trucks Price  \n--------------------------------------------------\n\n";


 do 
{ // get uses package number option
  cout<< "The Carwash packages are numbered 1-6\n\nChoose one of the 6 package numbers here \nor Press 0 to see more details:\n";
cin>> t ;

// this will take user to the show features function
if(t==0)
{
 showDetails();

}
//validate users package choice and go back to main function
if (t<=6 && t>=1)
{
  cout<< "You chosen package:  " << ray[(t-1)] << " \nIs this correct? (Y/N)\n";
cin>> letter;
if (letter == 'y' || letter == 'Y')
{
leave=true;
}
}
// error message
if (!(t<=6 && t>=0))
{
cout<< "\n***That is not a correct option.***\n\n--------------------------------------------------\n";
}

}
while (!(leave));
 
return (t-1);
}



//This Function is to display carwash feature details
//used cin.get tool to pause screen between information screens
void showDetails()
{
cout<< " \n                Car Wash Full Details\n";  
    cout<< "--------------------------------------------------\n"; 
  cout<< "Hand Wash  (Outside Only) \t\t\t   $6.99/$9.99 \n\t•Prep Wash and Grit Removal\n\t•Conveyor Wash\n\t•100% Hand Towel Wipe Down & Dry\n"; 
    cout<< "--------------------------------------------------\n"; 
  cout<< "Inside & Out  (Best Value!) \t\t $12.99/$15.99\n  ***Includes Hand Wash Package PLUS: \n\t•Power Vacuum of Carpets, Mats & Seats\n\t•Clean Windows Inside & Out\n\t•Clean Center Pockets, Consoles & Cup Holders\n\t•Interior Wipe Down of Dash, Displays & Door Jams\n";
    cout<< "--------------------------------------------------\n"; 
  cout<< "Deluxe Wash  \t\t\t\t\t     $16.99/$19.99\n  ***Includes Inside & Out Package PLUS: \n\t•Wheels & Tires Gentle Brush Cleaning and Tire Dressing\n\t•Scrub Brush Clean All Rubber Mats\n\t•Air Fragrance of Choice\n";
  cout<<"\n\t\t\t\tPress Enter to see Details Continued>>>";
 cin.get();
  cin.get();// PAUSE
 cout<< "\n--------------------------------------------------\n"; 
   cout<< "Hand Wax Express  \t\t\t\t     $25.99/$32.99\n ***Includes Inside & Out Package PLUS: \n\t•Clear Coat Sealant with UV Protection\n\t•Hand Apply Wax & Coat Polish\n\t•Wheels & Tires Gentle Brush Cleaning and Tire Dressing\n\t•Under Body Wash with Rust Inhibiter \n";
   cout<< "--------------------------------------------------\n"; 
  cout<< "Interior Express   \t\t\t\t     $45.99/$52.99\n ***Includes Inside & Out Package PLUS: \n\t•Shampoo & Hot Water Extraction\n\t\t  for All Carpets & Floor Mats\n\t•Shampoo & Hot Water Extraction for All Seat Cloth\n\t•Cleaning & Condition for Leather Seats**\n";
   cout<<"\n\t\t\t\tPress Enter to see Details Continued>>>";
   cin.get();// PAUSE
   cout<< "\n--------------------------------------------------\n"; 
  cout<< "Ultimate     \t\t\t\t\t     $55.99/$62.99 \n***Includes All Package Features***\n\t•Deluxe Wash Package\n\t•Hand Wax Express Package\n\t•Interior Express Package\n";
cout<< "--------------------------------------------------\n"; 
 cout<< "\t\t\t\tPackage Add-On Prices: ";
 cout<< "\n\t\t•Wheels & Tires\t\t\t\t\t     $3.00\n\t\t•Air Frangrance\t\t\t\t\t\t $1.50\n\t\t•Rubber Floor Mats\t\t\t\t\t $2.00\n\t\t•Shampoo **Carpet Only\t\t\t    $24.00\n\t\t•Shampoo **Seats Only \t\t\t    $24.00\n" ;

cout<< "--------------------------------------------------\n"; 
   cout<<"\n\t\t\t\tPress Enter to see Details Continued>>>";

  cin.get();// PAUSE
// show all 6 carwash packages again before leaving this function
     cout<< " \n                Car Wash Packages          ";  
  cout<< "\n--------------------------------------------------\n"; 
  cout<< "        1                 2                3   \n"; 
  cout<< "    Hand Wash       Inside and Out     Deluxe Wash    \n";
    cout<< "   $6.99/$9.99      $12.99/$15.99    $16.99/$19.99    \n\n";
  cout<< "        4                 5                6   \n"; 
  cout<< "Hand Wax Express    Interior Express     Ultimate    \n";
    cout<< " $25.99/$32.99       $45.99/$52.99     $55.99/$62.99    \n\n";
    cout<< "\t\t\t     Regular Car Price / \n\t\tLarge SUV and Full Size Trucks Price  \n--------------------------------------------------\n\n";
 
return ;
}


void getfeatures(double addon[],string titles[], const double prices [], const int size,int pack)
{
int t,addNum;
bool leave = false;
char letter='k', ask = 'k';

pack+=1;
//show Feature brief

 cout<< "\n\t\t\tPackage Add-On Prices: ";
 cout<<"\n--------------------------------------------------\n"; 
 cout<< "Add-On #1\t•Wheels & Tires\t\t\t\t     $3.00\nAdd-On #2\t•Air Frangrance\t\t\t\t\t $1.50\nAdd-On #3\t•Rubber Floor Mats\t\t\t\t $2.00\nAdd-On #4\t•Shampoo **Carpet Only\t\t    $24.00\nAdd-On #5\t•Shampoo **Seats Only \t\t    $24.00\n" ;

cout << fixed << showpoint << setprecision(2);

// do-while loop with a switch statements given the package number, each case is for a different package
 do
 {
  cout<< "\nThe Carwash Add-Ons are numbered 1-5\nChoose one of the 5 Add-On numbers here \nEnter 0 if you are done selecting Add-Ons for your Carwash:\n";
cin>>addNum;
if (addNum==0)
leave=true;
else
{   //subtract 1 from the users choice number to line up array elements
  addNum -=1;
  
 switch (pack)
 {
 case 1: // for Hand Wash add on features
 { 
 
  if (addNum==0 || addNum==1)
  {
    cout<<"\nYou have selected:\n"<< titles[addNum]<<"\t$"<<prices[addNum]<<"\nIs this the correct Add-on?(Y/N)"<<endl;
    cin>>ask;
    if (ask == 'y' || ask == 'Y')//Confirm
    {
      if(addon[addNum]==0)
      {    //refrences the arrays to add features to users carwash and display the cost
        addon[addNum]=prices[addNum];
        cout<<titles[addNum]<< " Has been added\n" ;

      }
    else
        {
          cout<<"\n**This Add-on has already been added to your Carwash.\n";
        }
    }
    else // user said no to confirmation
    { cout<<"\n\n";   }
  }
        // disqualified add-ons
          if (addNum==2 || addNum==3 || addNum==4 )
    {
      cout<<"\nOnly Add-Ons numbers 1 and 2 are available \nfor Hand Wash (Outside only)\nPlease make another selection.\n";
    }
    if (addNum>4 || addNum<0) //user enter a invalid choice
    cout<<"***That is not a valid choice**\nPlease select one of the 1-5 choices if \nyou wish to Add a feature to your Carwash\n";
//ask if user is done or not with add ons
cout << "\nWould you like to add anything else to your Car Wash?\n(Y/N)\n";
cin>> ask;
if (ask == 'y' || ask == 'Y')
leave=false;
else
leave=true;

 }
 break;
 case 2: // for Inside and Out wash add on features
 { 
 
  if (addNum>=0 && addNum<=4)
  {
    cout<<"\nYou have selected:\n"<< titles[addNum]<<"\t$"<<prices[addNum]<<"\nIs this the correct Add-on?(Y/N)"<<endl;
    cin>>ask;
    if (ask == 'y' || ask == 'Y')//Confirm
    {
      if(addon[addNum]==0) 
      {    //refrences the arrays to add features to users carwash and display the cost
        addon[addNum]=prices[addNum];
        cout<<titles[addNum]<< " Has been added\n" ;
      }
    else   // if addon element doesn't equal zero then: 
        {
          cout<<"\n**This Add-on has already been added to your Carwash.\n";
        }
    }
    else // user said no to confirmation
    { cout<<"\n\n";   }
  }
        
   
    if (addNum>4 || addNum<0) //user enter a invalid choice
    cout<<"***That is not a valid choice**\nPlease select one of the 1-5 choices if \nyou wish to Add a feature to your Carwash\n";
//ask if user is done or not with add ons
cout << "\nWould you like to add anything else to your Car Wash?\n(Y/N)\n";
cin>> ask;
if (ask == 'y' || ask == 'Y')
leave=false;
else
leave=true;

 }
 break;

case 3: // for Delux wash add on features
 { 
 
  if (addNum>=3 && addNum<=4)
  {
    cout<<"\nYou have selected:\n"<< titles[addNum]<<"\t$"<<prices[addNum]<<"\nIs this the correct Add-on?(Y/N)"<<endl;
    cin>>ask;
    if (ask == 'y' || ask == 'Y')//Confirm
    {
      if(addon[addNum]==0) 
      {    //refrences the arrays to add features to users carwash and display the cost
        addon[addNum]=prices[addNum];
        cout<<titles[addNum]<< " Has been added\n" ;
      }
    else   // if addon element doesn't equal zero then: 
        {
          cout<<"\n**This Add-on has already been added to your Carwash.\n";
        }
    }
    else // user said no to confirmation
    { cout<<"\n\n";   }
  }
         // disqualified add-ons
          if (addNum==0 || addNum==1 || addNum==2 )
    {
      cout<<"\nThat is a feature that is already included in \nthe Carwash Package you have selected, so there \nis no additional charge for this feature.\n";
    }
   
    if (addNum>4 || addNum<0) //user enter a invalid choice
    cout<<"***That is not a valid choice**\nPlease select one of the 1-5 choices if \nyou wish to Add a feature to your Carwash\n";
//ask if user is done or not with add ons
cout << "\nWould you like to add anything else to your Car Wash?\n(Y/N)\n";
cin>> ask;
if (ask == 'y' || ask == 'Y')
leave=false;
else
leave=true;

 }
 break;

case 4: // for Hand Wax wash add on features
 { 
 
  if (addNum>=1 && addNum<=4)
  {
    cout<<"\nYou have selected:\n"<< titles[addNum]<<"\t$"<<prices[addNum]<<"\nIs this the correct Add-on?(Y/N)"<<endl;
    cin>>ask;
    if (ask == 'y' || ask == 'Y')//Confirm
    {
      if(addon[addNum]==0) 
      {    //refrences the arrays to add features to users carwash and display the cost
        addon[addNum]=prices[addNum];
        cout<<titles[addNum]<< " Has been added\n" ;
      }
    else   // if addon element doesn't equal zero then: 
        {
          cout<<"\n**This Add-on has already been added to your Carwash.\n";
        }
    }
    else // user said no to confirmation
    { cout<<"\n\n";   }
  }
         // disqualified add-ons
          if (addNum==0)
    {
      cout<<"\nYour Hand Wax Express Carwash already includes this Feature \nfor tires. No extra charge.\n";
    }
   
    if (addNum>4 || addNum<0) //user enter a invalid choice
    cout<<"***That is not a valid choice**\nPlease select one of the 1-5 choices if \nyou wish to Add a feature to your Carwash\n";
//ask if user is done or not with add ons
cout << "\nWould you like to add anything else to your Car Wash?\n(Y/N)\n";
cin>> ask;
if (ask == 'y' || ask == 'Y')
leave=false;
else
leave=true;

 }
 break;

case 5: // for Interior Express wash add on features
 { 
 
  if (addNum>=0 && addNum<=1)
  {
    cout<<"\nYou have selected:\n"<< titles[addNum]<<"\t$"<<prices[addNum]<<"\nIs this the correct Add-on?(Y/N)"<<endl;
    cin>>ask;
    if (ask == 'y' || ask == 'Y')//Confirm
    {
      if(addon[addNum]==0) 
      {    //refrences the arrays to add features to users carwash and display the cost
        addon[addNum]=prices[addNum];
        cout<<titles[addNum]<< " Has been added\n" ;
      }
    else   // if addon element doesn't equal zero then: 
        {
          cout<<"\n**This Add-on has already been added to your Carwash.\n";
        }
    }
    else // user said no to confirmation
    { cout<<"\n\n";   }
  }
         // disqualified add-ons
          if (addNum==2 || addNum==3 || addNum==4)
    {
      cout<<"\nYour Interior Express Carwash already includes this Feature \nNo extra charge.\n";
    }
   
    if (addNum>4 || addNum<0) //user enter a invalid choice
    cout<<"***That is not a valid choice**\nPlease select one of the 1-5 choices if \nyou wish to Add a feature to your Carwash\n";
//ask if user is done or not with add ons
cout << "\nWould you like to add anything else to your Car Wash?\n(Y/N)\n";
cin>> ask;
if (ask == 'y' || ask == 'Y')
leave=false;
else
leave=true;

 }
 break;

case 6: // for Ultimate no features are available
 {  
    cout<<"\nCongratulations!\nWith the Ultimate Carwash Package you have selected, you have \nall Add-On Features already included for no extra charge.\n"<<endl;
    
leave=true;
 }
 break;
 //this will never occur
 default: cout << "Something went wrong, start over";
 }
}
 }while(!(leave));

return;
}

//this function will restart the program
//it uses for loops to clear the values in the arrays to null

void reset(double washPack[],double featureadds[],bool suvTruck)
{
int packsize = 6, fAddsize = 5;

for (int x=0 ; x < packsize; x++)
{
  
washPack[x]= 0;
cout<< washPack[x] <<endl;
}

for (int y=0 ; y < fAddsize; y++)
{
featureadds[y]= 0;

}

suvTruck = false;
cout<<"Carwash Ordering has successfully been Restarted\n\n\n";
  return;
}
