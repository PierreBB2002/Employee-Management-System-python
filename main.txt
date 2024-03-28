import os.path
import re
from datetime import date

employeeList = []
vacationList = []
academicList = []
salaryList = []
courses = []
vacListDic = []
numberOfTimesDic = []
empCourseList = []
numOfCourseList = []


class Employee:
    def __init__(self, emp_ID, first_name, middle_name, last_name, date_of_birth, martial_status, number_of_children,
                 emp_gender, emp_email, emp_mobile, emp_fax, emp_type_1, emp_status, department, starting_date,
                 emp_salary, health_insurance_emp):
        self.health_insurance = health_insurance_emp
        self.salary = emp_salary
        self.starting_date = starting_date
        self.department = department
        self.status = emp_status
        self.type = emp_type_1
        self.fax = emp_fax
        self.mobile = emp_mobile
        self.email = emp_email
        self.gender = emp_gender
        self.number_of_children = number_of_children
        self.martial_status = martial_status
        self.date_of_birth = date_of_birth
        self.last_name = last_name
        self.middle_name = middle_name
        self.first_name = first_name
        self.emp_id = emp_ID
        self.emp_id_info = emp_ID


def convert(any_list):
    return any_list.split()


def convert_to_integer(string_G):
    return int(string_G)


def find_num_of_courses(courseList, course_name):
    counter = 0
    for ind in range(0, len(courseList)):
        if courseList[ind] == course_name:
            counter += 1
    return counter


def is_Exist(empp_id, listtttt):
    for i4 in employeeList:
        if i4.emp_id == empp_id:
            return True
    return False
def number_of_digit_counter(number):
    counter = 0
    while number != 0:
        number //= 10
        counter += 1
    return counter


def find_num_of_courses_for_emp(courseList):
    coursesList2 = courseList.split(" ")
    return len(coursesList2)


def find_num_of_emp_for_course(listt, courseName):
    countt = 0
    for ind1 in listt:
        if courseName == ind1["course"]:
            countt += 1
    return countt


File1 = input("Enter the name of a file that contains the employees' attributes ")
while not os.path.exists(File1):
    File1 = input(f"{File1} file is not found... re-enter the file name ")

File2 = input("Enter the name of a file that contains the employees' academic information ")
while not os.path.exists(File2):
    File2 = input(f"{File2} file is not found... re-enter the file name ")

File3 = input("Enter the name of a file that contains the number of vacation days for each employee ")
while not os.path.exists(File3):
    File3 = input(f"{File3} file is not found... re-enter the file name ")

f2 = open(File2, "r")
f3 = open(File3, "r")
f1 = open(File1, "r")
count = 0
count_f3 = 0
count_f2 = 0
for line in f3:
    if line != "\n":
        count_f3 += 1
for line in f1:
    if line != "\n":
        count += 1
for line in f2:
    if line != "\n":
        count_f2 += 1
f2.seek(0)
f3.seek(0)
f1.seek(0)
lines = f1.readlines()
lines_f3 = f3.readlines()
lines_f2 = f2.readlines()
for i in range(1, count_f3):
    word = re.split('; ', lines_f3[i])
    emp_id_f3 = int(word[0])
    year_f3 = word[1]
    NumOfVac = int(word[2])
    vacationDic = {
        "ID": emp_id_f3,
        "year": year_f3,
        "number_of_vacation": NumOfVac
    }
    vacationList.append(vacationDic)
for i in range(1, count_f2):
    word = re.split('; ', lines_f2[i])
    emp_id_f2 = int(word[0])
    semester_f2 = word[1]
    year_f2 = word[2]
    courses_f2 = word[3]
    AcademicDic = {
        "ID": emp_id_f2,
        "semester": semester_f2,
        "year": year_f2,
        "courses": courses_f2
    }
    academicList.append(AcademicDic)

for i in range(1, count):
    word = re.split('; |, ', lines[i])
    employee_id = int(word[0])
    first = word[1]
    middle = word[2]
    last = word[3]
    Birthdate = word[4]
    martial = word[5]
    numOfChild = int(word[6])
    gender = word[7]
    email = word[8]
    mobile = word[9]
    fax = word[10]
    emp_type = word[11]
    status = word[12]
    dep = word[13]
    start_date = word[14]
    salary = int(word[15])
    health_ins = bool(word[16])
    employeeList.append(Employee(employee_id, first, middle, last, Birthdate,
                                 martial, numOfChild, gender, email, mobile,
                                 fax,
                                 emp_type, status, dep,
                                 start_date, salary, health_ins))
while True:
    menu = \
        """
    =====================================================
    =                   MAIN MENU                       =
    =====================================================
    1.  Add a new employee record.
    2.  Update general attributes.
    3.  Add/update administrative employee attribute.
    4.  Add/update academic employee attribute.
    5.  Employee’s statistics.
    6.  Salary statistics.
    7.  Retirement information.
    8.  Courses statistics.
    9.  Administrative employees’ statistics
    10. Academic employees’ statistics.
    =====================================================
    =                Enter your choice                  =
    =====================================================
    """
    print(menu)
    choice = 0
    emp_id = 0
    try:
        choice = int(input("your choice: "))
    except ValueError:
        print("Invalid Input ")
    if choice == 1:
        try:
            emp_id = int(input("Enter the employee ID "))
        except ValueError:
            print("Invalid input ")
        while number_of_digit_counter(emp_id) != 5:
            try:
                print("id should contains only 5 integers ")
                emp_id = int(input("Enter the employee ID "))
            except ValueError:
                print("id should contains only 5 integers ")
                try:
                    emp_id = int(input("Enter the student ID "))
                except ValueError:
                    emp_id = int(input("Enter the employee ID "))
        if is_Exist(emp_id, employeeList)== False:
            name1 = input("First name: ")
            name2 = input("Middle name: ")
            name3 = input("Last Name ")
            BirthDate = input("Enter the date of birth ")
            while "/" not in BirthDate:
                print("Invalid input ")
                BirthDate = input("Enter the date of birth ")
            mar_status = input("Enter the martial status ")
            while mar_status != "Single" and mar_status != "Maried":
                print("Invalid input ")
                mar_status = input("Enter the martial status ")
            numberOfChild = 0
            try:
                numberOfChild = int(input("Enter the number of children "))
            except ValueError:
                print("Invalid input ")
                numberOfChild = int(input("Enter the number of children "))
            genderIMP = input("Enter the gender ")
            while genderIMP != "male" and genderIMP != "female" and genderIMP != "Male" and genderIMP != "Female":
                print("Invalid input ")
                genderIMP = input("Enter the gender ")
            email_cont = input("Email: ")
            while "@" not in email_cont:
                print("Invalid input ")
                email_cont = input("Email: ")
            mob_num = input("Mobile no. : ")
            fax_cont = input("Fax : ")
            type_emp = input("Enter the type (Administrative or Academic) ")
            while type_emp != "Administrative" and type_emp != "Academic" and type_emp != "administrative" and type_emp != "academic":
                print("Invalid input ")
                type_emp = input("Enter the type (Administrative or Academic) ")
            stat = input("Enter the status ( full-time, part-time, and left-university ) ")
            while stat != "full-time" and stat != "full time" and stat != "part-time" and stat != "part time" and stat != "left-university" and stat != "left university":
                print("Invalid input ")
                stat = input("Enter the status ( full-time, part-time, and left-university ) ")
            depart = input("Department: ")
            start_date = input("Starting date: ")
            while "/" not in start_date:
                print("Invalid input ")
                start_date = input("Starting date: ")
            sal = 0
            try:
                sal = int(input("Salary: "))
            except ValueError:
                print("Invalid input ")
                sal = int(input("Salary: "))
            health_insurance = input("health insurance ( True or False ) ")
            while health_insurance != "True" and health_insurance != "False":
                print("Invalid input ")
                health_insurance = input("health insurance ( True or False ) ")
            employeeList.append(
                Employee(emp_id, name1, name2, name3, BirthDate, mar_status, numberOfChild, genderIMP, email_cont,
                         mob_num, fax_cont, type_emp, stat, depart, start_date, sal, health_insurance))
            print("Employee added successfully ")

    if choice == 2:
        a = """
                            1. First Name
                            2. Middle Name
                            3. Last Name
                            4. Date of Birth
                            5. Marital Status
                            6. Number of Children
                            7. Gender
                            8. Email
                            9. Mobile Number
                            10. Fax
                            11. Type ( academic or administrative )
                            12. Status (full-time, part-time, and left-university )
                            13. Department
                            14. Starting Date
                            15. Basic Salary
                            16. Health Insurance 
                            17. press 0 to exit
                """
        updated_id = int(input("ID: "))
        check = 0
        for i in employeeList:
            if updated_id == i.emp_id:
                emp_found = i
                check = 1

        if check == 0:
            print("Employee does not exist")

        else:
            ch = -1
            while ch != "0":
                print(a)
                ch = input("Enter which attribute to update ")
                if ch == "First Name" or ch == "1":
                    newName = input("First Name: ")
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.first_name = newName
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name)
                            print("First Name updated successfully ")
                if ch == "Middle Name" or ch == "2":
                    newName = input("Middle Name: ")
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.middle_name = newName
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name)
                            print("Middle Name updated successfully ")
                if ch == "Last Name" or ch == "3":
                    newName = input("Last Name: ")
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.last_name = newName
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name)
                            print("Last Name updated successfully ")
                if ch == "Date of Birth" or ch == "4":
                    newDate = input("Date of Birth: ")
                    while "/" not in newDate:
                        print("Invalid input ")
                        newDate = input("Enter the date of birth ")
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.date_of_birth = newDate
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name, i.date_of_birth)
                            print("Date of Birth updated successfully")
                if ch == "Marital Status" or ch == "5":
                    newMarStat = input("Marital Status: ")
                    while newMarStat != "Single" and newMarStat != "Maried":
                        print("Invalid input ")
                        newMarStat = input("Enter the martial status ")
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.martial_status = newMarStat
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name, i.martial_status)
                            print("Marital Status updated successfully")
                if ch == "Number of Children" or ch == "6":
                    try:
                        newMarStat = int(input("Number of Children: "))
                    except ValueError:
                        print("Invalid input ")
                        newMarStat = int(input("Number of Children: "))
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.number_of_children = newMarStat
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name, i.number_of_children)
                            print("Number of Children updated successfully")
                if ch == "Gender" or ch == "7":
                    newMarStat = input("Gender: ")
                    while newMarStat != "male" and newMarStat != "female" and newMarStat != "Male" and newMarStat != "Female":
                        print("Invalid input ")
                        newMarStat = input("Enter the gender ")
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.gender = newMarStat
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name, i.gender)
                            print("Gender updated successfully")
                if ch == "Email" or ch == "8":
                    newMarStat = input("Email ")
                    while "@" not in newMarStat:
                        print("Invalid input ")
                        newMarStat = input("Email: ")
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.email = newMarStat
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name, i.email)
                            print("Email Status updated successfully")
                if ch == "Mobile Number" or ch == "9":
                    newMarStat = input("Mobile Number ")
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.mobile = newMarStat
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name, i.mobile)
                            print("Mobile Number updated successfully")
                if ch == "Fax" or ch == "10":
                    newMarStat = input("Fax: ")
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.fax = newMarStat
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name, i.fax)
                            print("Fax updated successfully")

                if ch == "Type" or ch == "11":
                    newMarStat = input("Type ( academic or administrative ): ")
                    while newMarStat != "Administrative" and newMarStat != "Academic" and newMarStat != "administrative" and newMarStat != "academic":
                        print("Invalid input ")
                        newMarStat = input("Enter the type (Administrative or Academic) ")
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.type = newMarStat
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name, i.type)
                            print("Type updated successfully")
                if ch == "Status" or ch == "12":
                    newMarStat = input("Status (full-time, part-time, and left-university ): ")
                    while newMarStat != "full-time" and newMarStat != "full time" and newMarStat != "part-time" and newMarStat != "part time" and newMarStat != "left-university" and newMarStat != "left university":
                        print("Invalid input ")
                        newMarStat = input("Enter the status ( full-time, part-time, and left-university ) ")
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.status = newMarStat
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name, i.status)
                            print("Status updated successfully")
                if ch == "Department" or ch == "13":
                    newMarStat = input("Department: ")
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.department = newMarStat
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name, i.department)
                            print("Department updated successfully")
                if ch == "Starting Date" or ch == "14":
                    newMarStat = input("Starting Date: ")
                    while "/" not in newMarStat:
                        print("Invalid input ")
                        newMarStat = input("Starting date: ")
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.starting_date = newMarStat
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name, i.starting_date)
                            print("Starting Date updated successfully")
                if ch == "Basic Salary" or ch == "15":
                    try:
                        newMarStat = int(input("Basic Salary: "))
                    except ValueError:
                        print("Invalid input ")
                        newMarStat = int(input("Basic Salary: "))
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.salary = newMarStat
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name, i.salary)
                            print("Basic Salary updated successfully")
                if ch == "Health Insurance" or ch == "16":
                    newMarStat = bool(input("Health Insurance: "))
                    while newMarStat != "True" and newMarStat != "False":
                        print("Invalid input ")
                        newMarStat = bool(input("Health Insurance: "))
                    for i in employeeList:
                        if i.emp_id == updated_id:
                            i.health_insurance = newMarStat
                            print(i.emp_id, i.first_name, i.middle_name, i.last_name, i.health_insurance)
                            print("Health Insurance updated successfully")
    if choice == 3:
        ch1 = 0
        ch2 = 0
        numOfDate = 0
        try:
            emp_id_1 = int(input("Enter the student ID "))
        except ValueError:
            print("Invalid input ")
            emp_id_1 = int(input("Enter the student ID "))
        for i in employeeList:
            if i.emp_id == emp_id_1:
                ch2 = 1
                if (i.status != "left-university") and (i.type == "Administrative"):
                    entYear = input("Enter the year: ")
                    try:
                        numOfDate = int(entYear)
                    except ValueError:
                        print("Invalid date")
                        entYear = input("Enter the year: ")
                    while "/" in entYear:
                        print("Invalid input ")
                        entYear = input("Enter the year: ")
                    try:
                        entVac = int(input("Enter the number of vacation days: "))
                    except ValueError:
                        print("Invalid input ")
                        entVac = int(input("Enter the number of vacation days: "))
                    for j in vacationList:
                        if j.get("year") == entYear and j.get("ID") == emp_id_1:
                            j["number_of_vacation"] = entVac
                            ch1 = 1
                            print("This record is updated ")
                    if ch1 == 0:
                        AddedDictionary = {
                            "ID": emp_id_1,
                            "year": entYear,
                            "number_of_vacation": entVac
                        }
                        vacationList.append(AddedDictionary)
                        print("This record is added to the file ")
                else:
                    print("you can't update the number of vacation days ")
                    break
        if ch2 == 0:
            print("There is no employee with this ID ")
        for j in vacationList:
            print(j.get("ID"), j.get("year"), j.get("number_of_vacation"))
    if choice == 4:
        ch1 = 0
        try:
            emp_id_2 = int(input("Enter the employee ID: "))
        except ValueError:
            print("Invalid input ")
            emp_id_2 = int(input("Enter the employee ID: "))
        ch2 = 0
        for i in employeeList:
            if i.emp_id == emp_id_2:
                ch1 = 1
                if (i.status != "left-university") and (i.type == "Academic"):
                    entYear_2 = input("Enter the year: ")
                    while "/" in entYear_2:
                        print("Invalid input ")
                        entYear_2 = input("Enter the year: ")
                    try:
                        entSem = int(input("Enter the semester (1 or 2 or 3): "))
                        while entSem != 1 and entSem != 2 and entSem != 3:
                            print("Invalid input ")
                            entSem = int(input("Enter the semester (1 or 2 or 3): "))
                    except ValueError:
                        print("Invalid input ")
                        entSem = int(input("Enter the semester (1 or 2 or 3): "))
                    entCourse = input("Enter the courses: ")
                    for j in academicList:
                        if j.get("year") == entYear_2 and j.get("semester") == entSem:
                            j["courses"] = entCourse
                            print("This record is updated ")
                            ch2 = 1
                    if ch2 == 0:
                        AddedDictionaryAcademic = {
                            "ID": emp_id_2,
                            "semester": entSem,
                            "year": entYear_2,
                            "courses": entCourse
                        }
                        print("This record is added")
                        academicList.append(AddedDictionaryAcademic)
                if i.status == "left-university":
                    print("you can't update the information for this employee ")
                    break
                if i.type == "Administrative":
                    print("you can't update the administrative employee information")
                    break
        if ch1 == 0:
            print("There is no employee with this ID ")
    if choice == 5:
        counter_academic = 0
        counter_administrative = 0
        counter_full_time = 0
        counter_Male = 0
        counter_Female = 0
        for i in employeeList:
            if i.type == "Academic" or i.type == "Academic " or i.type == " Academic":
                counter_academic += 1
            if i.type == "Administrative" or i.type == "Administrative " or i.type == " Administrative":
                counter_administrative += 1
            if i.status == "Full-time" or i.status == " Full-time" or i.status == "Full-time " or \
                    i.status == "full-time":
                counter_full_time += 1
            if i.gender == "Male" or i.gender == "Male " or i.gender == " Male" or i.gender == "male":
                counter_Male += 1
            counter_Female = len(employeeList) - counter_Male
        b = """
    =====================================================
    =              Employee’s statistics                =
    =====================================================
        """
        print(b)
        print(f"Number of academic employees: {counter_academic}")
        print(f"Number of administrative employees: {counter_administrative}")
        print(f"Percent of Full-time employees: {counter_full_time}")
        print(f"Number of Male employees: {counter_Male}")
        print(f"Number of Female employees: {counter_Female}")
    if choice == 6:
        b = """
    =====================================================
    =                 Salary statistics                 =
    =====================================================
                """
        final_salary = 0
        sum_for_avg = 0
        sum_for_avg_admin = 0
        counter_for_avg = 0
        counter_for_avg_admin = 0
        all_salaries = 0
        salaryList.clear()
        salaryEnt = int(
            input("Enter a number to print all the employees who have salaries greater than the entered number: "))
        for i in employeeList:
            if i.type == "Academic" or i.type == "Academic " or i.type == " Academic":
                counter_for_avg += 1
                if i.martial_status == "Maried" and i.health_insurance is True:
                    final_salary = i.salary + 20 + 15 * i.number_of_children - 12 * (1 + (1 + i.number_of_children))
                    salaryDict = {
                        "First": i.first_name,
                        "Middle": i.middle_name,
                        "Last": i.last_name,
                        "Final_Salary": final_salary
                    }
                    salaryList.append(salaryDict)
                    sum_for_avg += final_salary
                else:
                    final_salary = i.salary + 15 * i.number_of_children
                    salaryDict = {
                        "First": i.first_name,
                        "Middle": i.middle_name,
                        "Last": i.last_name,
                        "Final_Salary": final_salary
                    }
                    salaryList.append(salaryDict)
                    sum_for_avg += final_salary
            if i.type == "Administrative" or i.type == "Administrative " or i.type == " Administrative":
                counter_for_avg_admin += 1
                if i.martial_status == "Maried" and i.health_insurance is True:
                    final_salary = i.salary + 20 + 15 * i.number_of_children - 12 * (1 + (1 + i.number_of_children))
                    salaryDict = {
                        "First": i.first_name,
                        "Middle": i.middle_name,
                        "Last": i.last_name,
                        "Final_Salary": final_salary
                    }
                    salaryList.append(salaryDict)
                    sum_for_avg_admin += final_salary
                else:
                    final_salary = i.salary + 15 * i.number_of_children
                    salaryDict = {
                        "First": i.first_name,
                        "Middle": i.middle_name,
                        "Last": i.last_name,
                        "Final_Salary": final_salary
                    }
                    salaryList.append(salaryDict)
                    sum_for_avg_admin += final_salary

        avg_academic = sum_for_avg / counter_for_avg
        avg_administrative = sum_for_avg_admin / counter_for_avg_admin
        print(b)
        print(f"Average academic employees’ salary: {avg_academic}")
        print(f"Average administrative employees’ salary: {avg_administrative}")
        for i in salaryList:
            if i["Final_Salary"] > salaryEnt:
                print(i["First"], i["Middle"], i["Last"], i["Final_Salary"])
    if choice == 7:
        b = """
    =====================================================
    =               Retirement information              =
    =====================================================
             """
        today = date.today()
        numForRet = int(
            input("Enter a number to print all employees that have remain years of service less than this number: "))
        print(b)
        for i in employeeList:
            word1 = re.split('/', i.starting_date)
            month_of_starting = int(word1[0])
            year_of_starting = int(word1[1])
            word2 = re.split('/', i.date_of_birth)
            month_of_birth = int(word2[1])
            year_of_birth = int(word2[2])
            age_of_emp = today.year - year_of_birth
            # if today.month - month_of_birth >= 0:
            # age_of_emp += 1
            num_of_working_years = today.year - year_of_starting
            num_of_working_mon = today.month - month_of_starting
            if numForRet == 0:
                print("No employees found ")
            if numForRet > (65 - age_of_emp):
                if 65 - age_of_emp == 1:
                    print(i.first_name, i.middle_name, i.last_name, f": {65 - age_of_emp} year left for retirement")
                else:
                    print(i.first_name, i.middle_name, i.last_name, f": {65 - age_of_emp} years left for retirement")
    if choice == 8:
        b = """
    =====================================================
    =                 Courses statistics                =
    =====================================================
                     """
        print(b)
        arr = []
        arr2 = []
        courses_2 = []
        numOfEmp = []
        coursesTaught = []
        print("Course:     Number of times offered:")
        for i in academicList:
            arr = i["courses"].split(" ")
            for j in range(0, len(arr)):
                courses.append(arr[j].strip())
                courses[j].replace(" \n", " ")
        for i in range(0, len(courses)):
            numOfCourses = find_num_of_courses(courses, courses[i])
            courses[i].replace(" \n", " ")
            numberOfTimes = {
                "course": courses[i].strip(),
                "Number_of_times": numOfCourses
            }
            numberOfTimesDic.append(numberOfTimes)
        newSet = set()
        newList = []
        for i in numberOfTimesDic:
            tup = tuple(i.items())
            if tup not in newSet:
                newSet.add(tup)
                newList.append(i)
        for i in newList:
            print(i["course"], "            ", i["Number_of_times"])
        for i in employeeList:
            for j in academicList:
                if i.emp_id == j["ID"]:
                    arr2 = j["courses"].split(" ")
                    for k in range(0, len(arr2)):
                        courses_2.append(arr2[k].strip())
                        courses_2[k].replace(" \n", " ")
                    for p in range(0, len(courses_2)):
                        newDicc = {
                            "ID": i.emp_id,
                            "course": courses_2[p]
                        }
                        numOfEmp.append(newDicc)
        print("Course:    Number of academic taught:")
        newSet1 = set()
        newList1 = []
        for i in numOfEmp:
            tup1 = tuple(i.items())
            if tup1 not in newSet1:
                newSet1.add(tup1)
                newList1.append(i)
        for i in newList1:
            numm = find_num_of_emp_for_course(newList1, i["course"])
            DicForEmpCourse = {
                "course": i["course"],
                "number_of_taught": numm
            }
            coursesTaught.append(DicForEmpCourse)

        newSet2 = set()
        newList2 = []
        for i in coursesTaught:
            tup2 = tuple(i.items())
            if tup2 not in newSet2:
                newSet2.add(tup2)
                newList2.append(i)
        for i in newList2:
            print(i["course"], "            ", i["number_of_taught"])
    if choice == 9:
        b = """
    =====================================================
    =        Administrative employees’ statistics       =
    =====================================================
                 """
        print(b)
        today = date.today()
        print("ID:        vacations:     average:")
        for i in employeeList:
            sum_for_vacation = 0
            for j in vacationList:
                if i.emp_id == j["ID"]:
                    sum_for_vacation += j["number_of_vacation"]
            vacDic = {
                "emp_id": i.emp_id,
                "num_of_vac": sum_for_vacation
            }
            vacListDic.append(vacDic)
        for j in vacListDic:
            num_of_working_years = 0
            for i in employeeList:
                if i.emp_id == j["emp_id"]:
                    word1 = re.split('/', i.starting_date)
                    year_of_starting = int(word1[1])
                    num_of_working_years = today.year - year_of_starting
            avg_for_vacation = j["num_of_vac"] / num_of_working_years
            if j["num_of_vac"] < 10:
                print(j["emp_id"], "     ", j["num_of_vac"], "           ", avg_for_vacation)
            else:
                print(j["emp_id"], "    ", j["num_of_vac"], "           ", avg_for_vacation)

    if choice == 10:
        b = """
    =====================================================
    =           Academic employees’ statistics          =
    =====================================================
                         """
        print(b)
        counter_for_courses_emp = 0
        counterSemester = 0
        print("ID:          number of courses:         %course per semester")
        for i in employeeList:
            if i.type == "Academic":
                counter_for_courses_emp = 0
                counterSemester = 0
                for j in academicList:
                    if i.emp_id == j["ID"]:
                        counter_for_courses_emp += find_num_of_courses_for_emp(j["courses"])
                        counterSemester += 1
                if counterSemester != 0:
                    avg_for_course_sem = counter_for_courses_emp / counterSemester
                else:
                    avg_for_course_sem = 0
                print(i.emp_id, "              ", counter_for_courses_emp, "                      ",
                      round(avg_for_course_sem, 2))
    if choice == 0:
        break
    if choice == 11:
        for i in range(0,len(employeeList)):
            print(employeeList[i].emp_id)
