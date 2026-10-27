# python-activity-based-3. Algorithm
Eligibility criteria (example rules):
Aggregate marks must be at least 75%.
Every subject mark must be at least 60%.
Attendance must be at least 75%.
Annual family income must be ₹2,50,000 or less.
flowchart TD
    A([Start]) --> B[/Input student details/]
    B --> C[Calculate aggregate marks]
    C --> D{All eligibility rules satisfied?}
    D -- Yes --> E[Add to eligible list]
    D -- No --> F[Reject applicant]
    E --> G[Rank eligible students]
    F --> G
    G --> H[/Display results/]
    H --> I([Stop])
   # University Scholarship Allocation System

MIN_AGGREGATE = 75
MIN_SUBJECT_MARK = 60
MIN_ATTENDANCE = 75
MAX_INCOME = 250000

applicants = []
eligible = []
rejected = []

n = int(input("Enter number of applicants: "))

for i in range(n):
    print("\nApplicant", i + 1)

    app_no = int(input("Application number: "))
    name = input("Student name: ")

    marks = []
    for j in range(5):
        mark = float(input("Enter mark for subject " +
                           str(j + 1) + ": "))
        marks.append(mark)

    attendance = float(input("Enter attendance percentage: "))
    income = float(input("Enter annual family income: "))

    aggregate = sum(marks) / len(marks)

    reasons = []

    if aggregate < MIN_AGGREGATE:
        reasons.append("Aggregate below 75%")

    if min(marks) < MIN_SUBJECT_MARK:
        reasons.append("Subject mark below 60%")

    if attendance < MIN_ATTENDANCE:
        reasons.append("Attendance below 75%")

    if income > MAX_INCOME:
        reasons.append("Income above Rs. 250000")

    student = [app_no, name, aggregate, attendance, income]

    if len(reasons) == 0:
        eligible.append(student)
    else:
        rejected.append([name, reasons])

# Rank by aggregate, attendance, income, application number
eligible.sort(key=lambda s: (-s[2], -s[3], s[4], s[0]))

print("\n--- SCHOLARSHIP RANK LIST ---")

if len(eligible) == 0:
    print("No eligible applicants.")
else:
    rank = 1
    for s in eligible:
        print("Rank:", rank,
              "| Application No:", s[0],
              "| Name:", s[1],
              "| Aggregate:", round(s[2], 2), "%",
              "| Attendance:", s[3], "%",
              "| Income: Rs.", s[4])
        rank += 1

print("\n--- NOT ELIGIBLE APPLICANTS ---")

if len(rejected) == 0:
    print("No rejected applicants.")
else:
    for student in rejected:
        print("Name:", student[0],
              "| Reason:", ", ".join(student[1])) 
Enter number of applicants: 4

--- SCHOLARSHIP RANK LIST ---
Rank: 1 | Application No: 101 | Name: Asha | Aggregate: 90.0 % | Attendance: 90.0 % | Income: Rs. 200000.0
Rank: 2 | Application No: 102 | Name: Ravi | Aggregate: 84.0 % | Attendance: 95.0 % | Income: Rs. 180000.0
Rank: 3 | Application No: 103 | Name: Priya | Aggregate: 76.0 % | Attendance: 80.0 % | Income: Rs. 250000.0

--- NOT ELIGIBLE APPLICANTS ---
Name: Kumar | Reason: Subject mark below 60%

              
