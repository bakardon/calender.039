# calender.039
link for onedrive since the other one has issues.....
https://1drv.ms/w/s!Aq_l1Y9nam8ehkCKR2xaaT3IU9k6?e=ETqMVi

link for figma...
https://www.figma.com/file/riWr0DQHfaPLQERJWkHgtw/calender7?type=design&node-id=0%3A1&t=E6nu2fUBjzRfGAy8-1

figma code...
<iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Ffile%2FriWr0DQHfaPLQERJWkHgtw%2Fcalender7%3Ftype%3Ddesign%26node-id%3D0%253A1%26t%3DE6nu2fUBjzRfGAy8-1" allowfullscreen></iframe>


#include <iostream>
#include <string>
class Calendar {
public:
    Calendar(int year) : m_year(year) {}
    void printCalendar();
    void addReminder(int day, const std::string& reminder);
    void clearReminders();
private:
    int m_year;
    std::string m_reminders[12][31];
};
void Calendar::printCalendar() {
    std::string months[] = {"January", "February", "March", "April", "May", "June", 
                            "July", "August", "September", "October", "November", "December"};
    int daysInMonth[] = {31, m_year % 4 == 0 ? 29 : 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
    int startingDay = 0;
    std::cout << "Calendar for year " << m_year << std::endl;
    for (int month = 0; month < 12; month++) {
        std::cout << std::endl << months[month] << std::endl;
        std::cout << "Sun Mon Tue Wed Thu Fri Sat" << std::endl;
        for (int i = 0; i < startingDay; i++) {
            std::cout << "    ";
        }
        for (int day = 1; day <= daysInMonth[month]; day++) {
            if ((day + startingDay - 1) % 7 == 0 && day != 1) {
                std::cout << std::endl;
            }
            std::cout << day;
            if (!m_reminders[month][day-1].empty()) {
                std::cout << " [" << m_reminders[month][day-1] << "]";
            }
            if (day < 10) {
                std::cout << "   ";
            }
            else {
                std::cout << "  ";
            }
            startingDay = (startingDay + 1) % 7;
        }
    }
    std::cout << std::endl;
}

void Calendar::addReminder(int day, const std::string& reminder) {
    int month, dayOfMonth;
    month = day / 100 - 1;
    dayOfMonth = day % 100 - 1;
    m_reminders[month][dayOfMonth] = reminder;
}

void Calendar::clearReminders() {
    for (int month = 0; month < 12; month++) {
        for (int day = 0; day < 31; day++) {
            m_reminders[month][day] = "";
        }
    }
}
int main() {
    int year;
    std::cout << "Enter year: ";
    std::cin >> year;
    Calendar calendar(year);
    std::string reminder;
    char choice;
    while (true) {
        std::cout << std::endl;
        std::cout << "Please select an option:" << std::endl;
        std::cout << "1. Print Calendar" << std::endl;
        std::cout << "2. Add Reminder" << std::endl;
        std::cout << "3. Clear Reminders" << std::endl;
        std::cout << "4. Quit" << std::endl;
        std::cin >> choice;
        switch (choice) {
            case '1':
                calendar.printCalendar();
                break;
            case '2':
                int day;
                std::cout << "Enter day : ";
                std::cin >> day;
                std::cout << "Enter reminder : ";
                std::cin.ignore();
                std::getline(std::cin, reminder);
                calendar.addReminder(day, reminder);
                std::cout << "Reminder added successfully." << std::endl;
                break;
            case '3':
                calendar.clearReminders();
                std::cout << "All reminders cleared." << std::endl;
                break;
            case '4':
                std::cout << "Thank you for using Calendar." << std::endl;
                return 0;
            default:
                std::cout << "Invalid input. Please try again." << std::endl;
        }
    }
    return 0;
}

