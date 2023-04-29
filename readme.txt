# calender.039


#include<iostream>
using namespace std;
int dayNumber(int day, int month, int year)
{
   static int A[] = { 0, 3, 2, 5, 0, 3, 5, 1, 4, 6, 2, 4 };
   year -= month < 3;
   return ( year + year/4 - year/100 + year/400 + A[month-1] + day) % 7;
}
string getMonthName(int monthNumber) 
{
   string M[] = {"January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"};
   return (M[monthNumber]);
}
int numberOfDays (int monthNumber, int year)
{
   switch(monthNumber)
   {
      case 0 :
      case 2 :
      case 4 :
      case 6 :
      case 7 :
      case 9 :
      case 11: return(31);
      break;
      case 1 :
         if (year % 400 == 0 || (year % 4 == 0 && year %100 != 0))
            return (29);
         else
            return (28);
      break;
      case 3 :
      case 5 :
      case 8 :
      case 10 : return(30);
      break;
   }
}
void printCalendar(int year, string reminders[][31])
{
   cout<<"\t\t\t Calendar - Year "<<year;
   int days;
   int current = dayNumber (1, 1, year);
   for (int i = 0; i < 12; i++)
   {
      days = numberOfDays (i, year);
      cout<<endl<<"\t\t ----X----"<<getMonthName (i).c_str()<<"----X---- \t\t"<<endl;
      cout<<" Sun  Mon  Tue   Wed    Thu    Fri    Sat \n";
      int k;
      for (k = 0; k < current; k++)
         cout<<"\t";
      for (int j = 1; j <= days; j++)
      {
         printf("%3d ", j);
         if (reminders[i][j-1] != "")
            cout << " (" << reminders[i][j-1] << ") ";

         if (++k > 6)
         {
            k = 0;
            cout<<endl;
         }
      }
      if (k)
         cout<<endl;
         current = k;
   }
   return;
};
   int main()
{
   int year;
   cout<<"Enter the year\n";
   cin>>year;
   string reminders[12][31];
   for (int i = 0; i < 12; i++) {
      for (int j = 0; j < 31; j++) {
         reminders[i][j] = "";
      }
   }

   int choice = 0;
   while (choice != 4) 
   {
      cout << "\nOptions:\n";
      cout << "1. Add reminder\n";
      cout << "2. Print calendar\n";
      cout << "3. Clear reminders\n";
      cout << "4. Quit\n";
      cout << "Enter choice: ";
      cin >> choice;
   };
      switch(choice)
      {
         case 1:
            int month, day;
            cout << "Enter month (1-12) and day (1-31): ";
            cin >> month >> day;
            cout << "Enter reminder for month " << month << " day " << day << ": ";
            cin >> reminders[month-1][day-1];
            break;

         case 2:
            printCalendar(year, reminders);
            break;

         case 3:
            for (int i = 0; i < 12; i++) {
               for (int j = 0; j < 31; j++) {
                  reminders[i][j] = "";
               }
            }
            cout << "Reminders cleared.\n";
            break;

         case 4:
            cout << "Goodbye!\n";
            break;

         default:
            cout << "Invalid choice. Please try again.\n";
            break;
      }
   }
   return 0;
}
