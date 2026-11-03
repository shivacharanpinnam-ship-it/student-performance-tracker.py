# student-performance-tracker.py

# ==========================================
# PROJECT: STUDENT PERFORMANCE ANALYZER
# LANGUAGE: PYTHON
# ==========================================

def calculate_total(marks):
    return sum(marks)


def calculate_average(marks):
    return sum(marks) / len(marks)


def calculate_grade(average):
    if average >= 90:
        return "A+"
    elif average >= 80:
        return "A"
    elif average >= 70:
        return "B"
    elif average >= 60:
        return "C"
    elif average >= 50:
        return "D"
    else:
        return "F"


def calculate_result(marks):
    if all(mark >= 35 for mark in marks):
        return "PASS"
    else:
        return "FAIL"


def get_valid_marks(subject):
    while True:
        try:
            mark = float(input(f"Enter marks in {subject} (0-100): "))

            if 0 <= mark <= 100:
                return mark

            print("Please enter marks between 0 and 100.")

        except ValueError:
            print("Invalid input! Enter a number.")


def add_student(students):
    print("\n----- ADD STUDENT -----")

    name = input("Enter student name: ").strip()

    if not name:
        print("Student name cannot be empty.")
        return

    subjects = ["Mathematics", "Physics", "Chemistry",
                "Programming", "English"]

    marks = []

    for subject in subjects:
        mark = get_valid_marks(subject)
        marks.append(mark)

    total = calculate_total(marks)
    average = calculate_average(marks)
    grade = calculate_grade(average)
    result = calculate_result(marks)

    student = {
        "name": name,
        "marks": marks,
        "total": total,
        "average": average,
        "grade": grade,
        "result": result
    }

    students.append(student)

    print("\nStudent added successfully!")


def display_students(students):
    print("\n========== STUDENT REPORT ==========")

    if not students:
        print("No student records available.")
        return

    for student in students:
        print("\nStudent Name:", student["name"])
        print("Marks:", student["marks"])
        print("Total Marks:", student["total"], "/ 500")
        print("Average:", round(student["average"], 2), "%")
        print("Grade:", student["grade"])
        print("Result:", student["result"])

    print("\n====================================")


def display_topper(students):
    if not students:
        print("\nNo student records available.")
        return

    topper = max(students, key=lambda student: student["average"])

    print("\n========== CLASS TOPPER ==========")
    print("Name:", topper["name"])
    print("Average:", round(topper["average"], 2), "%")
    print("Grade:", topper["grade"])
    print("==================================")


def display_class_statistics(students):
    if not students:
        print("\nNo student records available.")
        return

    averages = [student["average"] for student in students]

    passed = sum(1 for student in students
                 if student["result"] == "PASS")

    failed = len(students) - passed

    print("\n======= CLASS STATISTICS =======")
    print("Total Students:", len(students))
    print("Passed Students:", passed)
    print("Failed Students:", failed)
    print("Class Average:", round(sum(averages) / len(averages), 2))
    print("================================")


def main():
    students = []

    while True:
        print("\n================================")
        print("   STUDENT PERFORMANCE ANALYZER")
        print("================================")
        print("1. Add Student")
        print("2. View Student Reports")
        print("3. Find Class Topper")
        print("4. View Class Statistics")
        print("5. Exit")

        choice = input("\nEnter your choice (1-5): ").strip()

        if choice == "1":
            add_student(students)

        elif choice == "2":
            display_students(students)

        elif choice == "3":
            display_topper(students)

        elif choice == "4":
            display_class_statistics(students)

        elif choice == "5":
            print("\nThank you for using Student Performance Analyzer!")
            break

        else:
            print("\nInvalid choice! Please select 1 to 5.")


if __name__ == "__main__":
    main()

# ==========================================
# END OF PROJECT
# ==========================================
