# PSEUDOCODE FOR ASSIGNMENT STRESS RADAR - VERSION 1 (BASIC TRACKER)

---

## INDEX.HTML (LANDING PAGE)

```
DISPLAY page header with logo "Assignment Stress Radar"
DISPLAY college information "St Philip's College"

DISPLAY two clickable cards:
    Card 1: Student Portal
        - Icon: 📚
        - Features: Assignment tracking, Stress monitoring, Deadline alerts
        - Link to: student_app.html

    Card 2: Teacher Dashboard
        - Icon: 👩‍🏫
        - Features: Workload heatmap, Analytics
        - Link to: teacher_app.html

DISPLAY system benefits section:
    - Prevent Burnout
    - Improve Performance
    - Data-Driven Insights
    - Collaborative Planning
```

---

## STUDENT_APP.HTML (STUDENT PORTAL)

### Data Structure
```
INITIALIZE assignments = empty array from localStorage('student-assignments')
```

### On Page Load
```
WHEN page loads:
    SET minimum date for date picker to today
    CALL renderAll()
```

### Assignment Form Submission
```
WHEN user submits assignment form:
    GET subject from input field
    GET assignment title from input field
    GET due date from date picker
    GET description from input field (optional)

    CREATE new assignment object:
        - id = current timestamp
        - subject = subject input
        - assignment = assignment title input
        - dueDate = due date input
        - description = description input
        - dateAdded = current date/time

    ADD assignment to assignments array
    SAVE assignments array to localStorage
    CLEAR form inputs
    CALL renderAll()
    DISPLAY success message for 3 seconds
```

### Rendering Functions

#### renderAll()
```
FUNCTION renderAll():
    CALL updateStats()
    CALL renderUpcoming()
    CALL renderAssignments()
```

#### updateStats()
```
FUNCTION updateStats():
    CALCULATE total = count of all assignments
    CALCULATE subjects = count of unique subjects

    CALCULATE thisWeek = count of assignments due within next 7 days

    IF thisWeek >= 5:
        SET stress = "High"
    ELSE IF thisWeek >= 3:
        SET stress = "Medium"
    ELSE:
        SET stress = "Low"

    DISPLAY total on page
    DISPLAY thisWeek on page
    DISPLAY subjects on page
    DISPLAY stress on page

    CHANGE stress card color based on stress level:
        - High = Red
        - Medium = Orange
        - Low = Green
```

#### renderUpcoming()
```
FUNCTION renderUpcoming():
    FILTER assignments due within next 7 days
    SORT by due date (earliest first)

    IF no upcoming assignments:
        DISPLAY "No assignments due this week"
    ELSE:
        FOR EACH assignment in upcoming:
            CALCULATE days until due

            IF days <= 1:
                SET priority = "high" (red)
            ELSE IF days <= 3:
                SET priority = "medium" (orange)
            ELSE:
                SET priority = "low" (green)

            DISPLAY assignment card with:
                - Priority dot (colored)
                - Subject and title
                - Due date
                - Days remaining
```

#### renderAssignments()
```
FUNCTION renderAssignments():
    IF no assignments exist:
        DISPLAY empty state message
    ELSE:
        SORT assignments by due date (earliest first)

        FOR EACH assignment:
            CALCULATE days until due

            IF days < 0:
                SET badge = "Overdue" (red)
            ELSE IF days = 0:
                SET badge = "Due Today!" (red)
            ELSE IF days = 1:
                SET badge = "Due Tomorrow" (orange)
            ELSE IF days <= 3:
                SET badge = "X days left" (orange)
            ELSE:
                SET badge = "X days left" (green)

            DISPLAY assignment item with:
                - Subject and title
                - Due date
                - Date added
                - Description (if exists)
                - Badge (colored)
                - Delete button
```

### Delete Assignment
```
FUNCTION deleteAssignment(id):
    DISPLAY confirmation dialog "Are you sure?"

    IF user confirms:
        REMOVE assignment with matching id from array
        SAVE updated array to localStorage
        CALL renderAll()
```

---

## TEACHER_APP.HTML (TEACHER DASHBOARD)

### Data Structure
```
INITIALIZE studentAssignments = empty array from localStorage('student-assignments')
INITIALIZE currentMonth = current month number
INITIALIZE currentYear = current year number
```

### On Page Load
```
WHEN page loads:
    CALL renderAll()

    START auto-refresh timer (every 5 seconds):
        RELOAD studentAssignments from localStorage
        CALL renderAll()
```

### Rendering Functions

#### renderAll()
```
FUNCTION renderAll():
    CALL updateStats()
    CALL renderCalendar()
    CALL generateInsights()
```

#### updateStats()
```
FUNCTION updateStats():
    CALCULATE total = count of all assignments

    GROUP assignments by date
    COUNT days with 4+ assignments (stress days)

    COUNT assignments due on weekends (Saturday/Sunday)

    CALCULATE average assignments per day

    IF average <= 2:
        SET balanceScore = "Excellent"
    ELSE IF average <= 3:
        SET balanceScore = "Good"
    ELSE IF average <= 4:
        SET balanceScore = "Fair"
    ELSE:
        SET balanceScore = "Poor"

    DISPLAY total assignments
    DISPLAY stress days count
    DISPLAY weekend assignments count
    DISPLAY balance score
```

#### renderCalendar()
```
FUNCTION renderCalendar():
    DISPLAY current month and year

    CALCULATE first day of month
    CALCULATE total days in month

    CREATE calendar grid:
        ADD empty cells for days before month starts

        FOR day 1 to last day of month:
            GET assignments due on this day
            COUNT assignments

            CALCULATE stress level:
                IF count <= 1: stress = 0 (green)
                IF count <= 3: stress = 1 (yellow)
                IF count <= 5: stress = 2 (orange)
                IF count >= 6: stress = 3 (red)

            DISPLAY day cell with:
                - Day number
                - Assignment count
                - Background color based on stress
                - Click handler to show details
```

#### changeMonth()
```
FUNCTION changeMonth(direction):
    ADD direction to currentMonth (-1 for previous, +1 for next)

    IF currentMonth > 11:
        SET currentMonth = 0
        INCREMENT currentYear
    ELSE IF currentMonth < 0:
        SET currentMonth = 11
        DECREMENT currentYear

    CALL renderAll()
```

#### showDayDetails()
```
FUNCTION showDayDetails(date, assignments):
    OPEN modal dialog
    SET modal title to selected date

    IF no assignments:
        DISPLAY "No assignments due on this date"
    ELSE:
        CALCULATE stress level based on count

        DISPLAY stress level indicator:
            - Low (green)
            - Moderate (yellow)
            - High (orange)
            - Critical (red)

        FOR EACH assignment:
            DISPLAY assignment card with:
                - Subject
                - Assignment title
                - Description (if exists)
```

#### closeModal()
```
FUNCTION closeModal():
    HIDE modal dialog
```

#### generateInsights()
```
FUNCTION generateInsights():
    IF no student data:
        DISPLAY "No student data available"
        EXIT function

    INITIALIZE insights = empty array

    // Check for critical workload days
    GROUP assignments by date
    COUNT days with 4+ assignments

    IF critical days > 0:
        ADD insight:
            - Type: danger (red)
            - Title: "Critical Workload Alert"
            - Text: "X days have 4+ assignments"
            - Recommendation: "Redistribute assignments"

    // Check for subject imbalance
    GROUP assignments by subject
    COUNT assignments per subject
    SORT subjects by count (highest first)

    IF top subject has 50% more than second:
        ADD insight:
            - Type: warning (orange)
            - Title: "Subject Workload Imbalance"
            - Text: "Subject X accounts for Y% of assignments"
            - Recommendation: "Coordinate with other teachers"

    // Check for weekend assignments
    COUNT assignments on Saturday/Sunday

    IF weekend count > 0:
        ADD insight:
            - Type: warning (orange)
            - Title: "Work-Life Balance Impact"
            - Text: "X assignments due on weekends"
            - Recommendation: "Move to weekdays"

    // Positive feedback
    IF no insights generated:
        ADD insight:
            - Type: success (green)
            - Title: "Excellent Workload Management"
            - Text: "Balanced distribution"
            - Recommendation: "Continue current practices"

    DISPLAY all insights on page
```

---

## DATA STORAGE

### Local Storage Structure
```
localStorage['student-assignments'] = JSON array of:
    {
        id: unique number (timestamp),
        subject: string (e.g., "Mathematics"),
        assignment: string (e.g., "Chapter 5 Quiz"),
        dueDate: string (YYYY-MM-DD format),
        description: string (optional),
        dateAdded: string (ISO timestamp)
    }
```

---

## KEY ALGORITHMS

### Calculate Stress Level
```
ALGORITHM: Calculate Stress Level
INPUT: assignmentCount (integer)
OUTPUT: stressLevel (0-3)

IF assignmentCount <= 1:
    RETURN 0 (Low - Green)
ELSE IF assignmentCount <= 3:
    RETURN 1 (Moderate - Yellow)
ELSE IF assignmentCount <= 5:
    RETURN 2 (High - Orange)
ELSE:
    RETURN 3 (Critical - Red)
```

### Calculate Days Until Due
```
ALGORITHM: Calculate Days Until Due
INPUT: dueDate (string)
OUTPUT: days (integer)

CONVERT dueDate to Date object
GET current date
CALCULATE difference in milliseconds
CONVERT milliseconds to days
ROUND up to nearest whole number
RETURN days
```

### Filter Assignments by Date Range
```
ALGORITHM: Filter Assignments by Date Range
INPUT: assignments (array), startDate (Date), endDate (Date)
OUTPUT: filtered (array)

INITIALIZE filtered = empty array

FOR EACH assignment IN assignments:
    CONVERT assignment.dueDate to Date object

    IF dueDate >= startDate AND dueDate <= endDate:
        ADD assignment to filtered

RETURN filtered
```

---

## USER INTERACTIONS

### Student Portal
```
1. Fill out assignment form (subject, title, date, description)
2. Click "Add Assignment" button
3. View assignment in "All Assignments" section
4. View upcoming assignments in "Upcoming This Week" section
5. Check stress level in statistics cards
6. Delete assignment by clicking "Delete" button
7. Confirm deletion in dialog
```

### Teacher Dashboard
```
1. View statistics in stat cards at top
2. Browse calendar to see workload heatmap
3. Click previous/next buttons to change months
4. Click on calendar day to see assignment details
5. Read workload analysis insights at bottom
6. Monitor auto-refreshing data (updates every 5 seconds)
7. Close modal by clicking X or outside modal area
```
