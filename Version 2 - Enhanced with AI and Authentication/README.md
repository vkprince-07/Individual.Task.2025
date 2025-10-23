# Version 2 - Enhanced with AI and Authentication

## New Features Added

### 1. **Authentication System** 🔐
- **Sign-in required** for all users before accessing the website
- Separate login credentials for students and teachers
- Session-based authentication using localStorage
- Automatic redirection to login if not authenticated

**Demo Accounts:**
- **Student:** username: `student` | password: `student123`
- **Teacher:** username: `teacher` | password: `teacher123`

### 2. **AI Suggestion Feature for Teachers** 🤖
- **Smart Assignment Scheduler** with AI-powered date recommendations
- Analyzes student workload and suggests optimal due dates
- Provides multiple alternative dates with scoring system (0-100)
- Considers factors like:
  - Existing assignments on target date
  - Weekly workload distribution
  - Weekend penalties
  - Subject clustering
  - Mid-week vs. weekend timing

**AI Insights Include:**
- Critical risk warnings for overloaded days
- Weekly workload analysis
- Weekend scheduling alerts
- Optimal alternative date suggestions with reasoning

### 3. **Class Selection for Teachers** 🎓
- Dropdown menu to filter data by specific class
- Options include:
  - All Classes (default)
  - Class 10A, 10B
  - Class 11A, 11B
  - Class 12A, 12B
- Calendar, statistics, and AI suggestions automatically filter based on selected class

### 4. **Removed Cross-Dashboard Navigation** 🚫
- Students can NO LONGER navigate to teacher dashboard
- Teachers can NO LONGER navigate to student portal
- Navigation links removed from both dashboards
- Only **Logout** button available in navigation
- Must sign in with correct role to access respective dashboard

---

## Files Included

1. **login.html** - Sign-in page with role selection
2. **index.html** - Landing page (redirects to login)
3. **student_app.html** - Student portal with authentication
4. **teacher_app.html** - Teacher dashboard with AI, classes, and authentication
5. **pseudocode.md** - Documentation (carried over from Version 1)

---

## How to Use

### For Students:
1. Open `index.html` or go directly to `login.html`
2. Select role: **Student**
3. Enter credentials: `student` / `student123`
4. Access student portal to add assignments

### For Teachers:
1. Open `index.html` or go directly to `login.html`
2. Select role: **Teacher**
3. Enter credentials: `teacher` / `teacher123`
4. Select a class from dropdown (or view all)
5. Use **Smart Assignment Scheduler** to get AI suggestions for due dates
6. View workload heatmap filtered by selected class

---

## Key Differences from Version 1

| Feature | Version 1 | Version 2 |
|---------|-----------|-----------|
| Authentication | ❌ None | ✅ Required sign-in |
| Navigation | ✅ Can switch dashboards | ❌ Role-locked access |
| AI Suggestions | ❌ Not available | ✅ Full AI scheduler |
| Class Filtering | ❌ Not available | ✅ Teacher can filter by class |
| User Badge | ❌ None | ✅ Shows username |
| Logout | ❌ None | ✅ Available on all pages |

---

## Technical Implementation

### Authentication Flow:
```
1. User visits any page
2. JavaScript checks localStorage for 'user-session'
3. If no session → redirect to login.html
4. If wrong role → redirect to login.html
5. If valid session → display page content
```

### Class Filtering:
```
1. Teacher selects class from dropdown
2. selectedClass variable updated
3. All data (calendar, stats, AI) filtered by class
4. renderAll() refreshes all components with filtered data
```

### AI Scoring Algorithm:
```
Start with score = 100
- Subtract 15 points per existing assignment
- Subtract 30 for weekends
- Subtract 10 for Fridays
- Subtract 5 for Mondays
- Subtract points for heavy weeks (6-8+ assignments)
- Subtract points for subject clustering

Return final score (0-100)
Only suggest dates with score > 60
```

---

## Storage Structure

**localStorage Keys:**
- `user-session`: Stores current user's role and username
- `student-assignments`: Array of all assignment objects

**Assignment Object (for class filtering):**
```javascript
{
    id: timestamp,
    subject: "Mathematics",
    assignment: "Chapter 5 Quiz",
    dueDate: "2024-11-15",
    description: "Optional description",
    dateAdded: "2024-10-17T08:00:00.000Z",
    class: "class-10a"  // NEW in Version 2
}
```

---

## Future Enhancements (Not Implemented)

- Real backend database instead of localStorage
- Multiple teacher accounts with different class permissions
- Student class assignment (currently classes are teacher-side only)
- Password encryption
- Remember me functionality
- Email-based password reset

---

**Version 2 is production-ready with enhanced security and advanced AI features!** 🚀
