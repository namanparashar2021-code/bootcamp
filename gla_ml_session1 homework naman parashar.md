marks = [ 45, 60, 72, 38, 90]
total = 0
for i in range(len(marks) - 1):
  total += marks[i]

average = total / len(marks)
if average > 50:
  print("Class passed")
else:
  print("Class failed")

print("Average: ", average)

import pandas as pd

data = {
    "student_id": [101,102,103,104,105,106],
    "attendance_percent": [92, 67, 81, 45, 74, 88],
    "assignment_score": [18, 12, 15, 8, 14, 19],
    "quiz_score": [72, 48, 65, 30, 55, 80],
    "lab_completed": [True, False, True, False, True, True]
}

df = pd.DataFrame(data)

df

df.shape

df.head()

df.info()

df.describe()

df['total_score'] = df['assignment_score'] + df['quiz_score']


df

df['eligible'] = (
    (df['attendance_percent'] >= 75) &
    (df['total_score'] >= 70) &
    (df['lab_completed'])
)

df

eligible_students = df[df["eligible"] == True]

eligible_students

plt.figure(figsize=(8, 5))
sns.histplot(df['attendance_percent'], bins=5, kde=True)
plt.title('Distribution of Attendance Percentage')
plt.xlabel('Attendance Percentage')
plt.ylabel('Number of Students')
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()

plt.figure(figsize=(8, 5))
sns.histplot(df['total_score'], bins=5, kde=True)
plt.title('Distribution of Total Score (Assignment + Quiz)')
plt.xlabel('Total Score')
plt.ylabel('Number of Students')
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()

def assign_grade(score):
    if score >= 90:
        return 'A'
    elif score >= 80:
        return 'B'
    elif score >= 70:
        return 'C'
    elif score >= 60:
        return 'D'
    else:
        return 'F'

df['grade_category'] = df['total_score'].apply(assign_grade)


def assign_attendance_status(percent):
    if percent >= 90:
        return 'Excellent'
    elif percent >= 75:
        return 'Good'
    elif percent >= 60:
        return 'Average'
    else:
        return 'Poor'

df['attendance_status'] = df['attendance_percent'].apply(assign_attendance_status)


display(df)

plt.figure(figsize=(8, 5))
sns.countplot(x='grade_category', data=df, order=['A', 'B', 'C', 'D', 'F'], palette='viridis')
plt.title('Distribution of Grade Categories')
plt.xlabel('Grade Category')
plt.ylabel('Number of Students')
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()

plt.figure(figsize=(8, 5))
sns.countplot(x='attendance_status', data=df, order=['Excellent', 'Good', 'Average', 'Poor'], palette='magma')
plt.title('Distribution of Attendance Status')
plt.xlabel('Attendance Status')
plt.ylabel('Number of Students')
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()

