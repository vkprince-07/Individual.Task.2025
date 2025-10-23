# Version 2 - Enhanced Features Flowcharts

This folder contains flowcharts for the new algorithms and features added in Version 2 of the Assignment Stress Radar application.

## 📊 Flowchart Files

### 1. Authentication System (`1_authentication_system.mermaid`)
**Purpose:** User login and session management

**Key Features:**
- Login page with role selection (student/teacher)
- Credential validation against demo accounts
- Session creation and storage in localStorage
- Auto-redirect based on user role
- Logout functionality with session cleanup
- Auth checks on each page load

**Demo Accounts:**
- Student: `student` / `student123`
- Teacher: `teacher` / `teacher123`

---

### 2. AI Suggestion Algorithm (`2_ai_suggestion_algorithm.mermaid`)
**Purpose:** Intelligent assignment scheduling recommendations for teachers

**Key Features:**
- Analyzes student workload on desired date
- Calculates stress levels (Low, Moderate, High, Critical)
- Weekly workload analysis
- Weekend assignment detection
- Alternative date suggestions with scoring system

**Scoring Algorithm:**
- Starts at 100 points
- Penalties for: existing assignments (-15 each), weekends (-30), week overload (-20), subject clustering (-8)
- Only suggests alternatives with score > 60
- Provides top 3 alternatives with reasons

**Stress Levels:**
- 0-1 assignments: ✅ Low (Optimal)
- 2-3 assignments: ℹ️ Moderate
- 4-5 assignments: ⚠️ High (25% performance drop)
- 6+ assignments: 🚨 Critical (Significant impact)

---

### 3. Class Code Management (`3_class_code_management.mermaid`)
**Purpose:** Teacher class code generation and student-teacher linking

**Key Features:**
- Teachers generate unique class codes
- Format: `CLASSNAME-RANDOM6` (e.g., `10A-MATHEMATICS-A3F9K2`)
- Students enter class codes when adding assignments
- Teachers only see assignments from their class codes
- Copy to clipboard functionality
- Class code deletion with cascade effects

**Filtering Logic:**
- "All My Classes": Shows assignments matching ANY of teacher's codes
- Specific class: Shows only that class's assignments
- Assignments without matching codes: Not visible to teacher

---

### 4. Edit Assignment (`4_edit_assignment.mermaid`)
**Purpose:** Allow students to modify assignment details after creation

**Key Features:**
- Edit button on each assignment
- Modal form with pre-filled data
- Update all fields: subject, title, due date, class code, description
- Preserves original ID and dateAdded
- Real-time update across all views (calendar, stats, lists)
- Success notification after save

**Data Preservation:**
- ✓ Preserves: `id`, `dateAdded`
- ✓ Updates: `subject`, `assignment`, `dueDate`, `classCode`, `description`

**Impact:**
- Calendar: Updates day counts and colors
- Statistics: Recalculates totals and stress
- Upcoming: Re-filters and resorts
- All Assignments: Updates badges and order

---

### 5. Timezone-Safe Date Handling (`5_timezone_safe_dates.mermaid`)
**Purpose:** Fix date shifting issues in Central Australian Time (UTC+9:30/+10:30)

**The Problem:**
```javascript
// ❌ WRONG: Date shifts one day forward
new Date('2024-10-17')  // Interprets as UTC midnight
// → Shows as 2024-10-18 in Central Australian Time
```

**The Solution:**
```javascript
// ✅ RIGHT: Stays on correct date
parseLocalDate('2024-10-17')  // Creates in local timezone
// → Shows as 2024-10-17 correctly
```

**Helper Functions:**
1. **`parseLocalDate(dateString)`** - Parse string to Date in local timezone
2. **`dateToLocalString(date)`** - Convert Date to YYYY-MM-DD string
3. **`formatDateLocal(year, month, day)`** - Format components to string
4. **`addDays(dateString, days)`** - Add/subtract days from date string
5. **`getDayOfWeek(dateString)`** - Get day of week (0-6)

**Key Principles:**
1. Store dates as YYYY-MM-DD strings
2. Parse strings in LOCAL timezone (never UTC)
3. Compare as strings, not Date objects
4. Convert using local components
5. Never use `.toISOString()` for dates

---

## 📁 localStorage Structure

### `user-session`
```json
{
  "role": "student" | "teacher",
  "username": "student",
  "loginTime": "2024-10-17T10:30:00.000Z"
}
```

### `student-assignments`
```json
[
  {
    "id": 1729161234567,
    "subject": "Mathematics",
    "assignment": "Chapter 5 Quiz",
    "dueDate": "2024-10-25",
    "classCode": "10A-MATHEMATICS-A3F9K2",
    "description": "Includes word problems",
    "dateAdded": "2024-10-17T10:30:00.000Z"
  }
]
```

### `teacher-classes`
```json
[
  {
    "code": "10A-MATHEMATICS-A3F9K2",
    "name": "10A Mathematics",
    "createdAt": "2024-10-17T09:00:00.000Z"
  }
]
```

---

## 🔄 Data Flow Summary

1. **Login** → Creates session → Redirects to portal
2. **Student adds assignment** → Includes class code → Saved to localStorage
3. **Teacher views calendar** → Filters by class codes → Shows only their students
4. **Teacher uses AI** → Analyzes workload → Suggests optimal dates
5. **Student edits assignment** → Updates localStorage → Refreshes all views
6. **All date operations** → Use helper functions → No timezone issues

---

## 🎨 Viewing Flowcharts

These `.mermaid` files can be viewed in:
- **Visual Studio Code** with Mermaid extensions
- **GitHub** (renders Mermaid natively)
- **Online Mermaid Editor** at https://mermaid.live/
- **HTML viewers** (create HTML file with Mermaid.js library)

---

## 🆕 What's New in Version 2?

Compared to Version 1, Version 2 adds:

✅ **Authentication System** - Secure login for students and teachers
✅ **AI Scheduling** - Intelligent assignment date recommendations
✅ **Class Codes** - Link students to specific teachers
✅ **Edit Functionality** - Modify assignments after creation
✅ **Timezone Safety** - Works correctly in all timezones
✅ **Student Calendar** - Visual workload view for students
✅ **Teacher Filtering** - See only your students' assignments

---

## 📚 Technical Implementation

All features are implemented in:
- `index.html` - Login page
- `student_app.html` - Student portal with calendar and edit
- `teacher_app.html` - Teacher portal with AI and class management

Each file contains:
- HTML structure
- CSS styling (embedded)
- JavaScript functionality (embedded)
- Helper functions for date handling

No external dependencies or frameworks - pure HTML/CSS/JavaScript!

---

## 🐛 Debug Tools

`debug.html` - Date debugging tool showing:
- Current date in multiple formats
- All assignments in localStorage
- Date format conversion tests
- Clear data functionality

---

*Created for St Philip's College Digital Technology Course*
*Version 2 - October 2024*
