# Assignment Stress Radar 🎯

## Overview

**Assignment Stress Radar** is an intelligent assignment scheduling system designed for St Philip's College to prevent academic burnout and optimize student learning outcomes through data-driven workload management.

### The Problem
Teachers often don't realize when students are overloaded with deadlines from multiple subjects, leading to:
- Academic burnout and decreased performance
- Uneven stress distribution across the school year
- Poor coordination between different subject areas
- Students struggling to manage multiple deadlines simultaneously

### The Solution
Our system provides:
- **Real-time workload visualization** for teachers
- **AI-powered scheduling suggestions** to prevent overload
- **Student stress tracking** across all subjects
- **Collaborative planning tools** for balanced assignment distribution

## Features

### 🎓 Student Portal (`student_app.html`)
- **Assignment Input**: Easy-to-use form for entering assignment details
- **Stress Monitoring**: Visual indicators of daily workload levels
- **Statistics Dashboard**: Personal analytics and upcoming deadlines
- **Modern Interface**: Clean, St Philip's-inspired design

### 👩‍🏫 Teacher Dashboard (`teacher_app.html`)
- **Smart Scheduler**: AI-powered assignment date recommendations
- **Workload Heatmap**: Visual calendar showing student stress patterns
- **Intelligent Suggestions**: Context-aware scheduling advice
- **Real-time Analytics**: Live insights into student workload distribution

### 🚀 Main Launcher (`index.html`)
- **Professional Interface**: Clean entry point to both applications
- **System Overview**: Clear explanation of benefits and features
- **Easy Navigation**: Quick access to student and teacher portals

## Technology Stack

- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **Storage**: LocalStorage for cross-application data sharing
- **Design**: Responsive, mobile-first approach
- **AI Engine**: Custom algorithms for workload analysis and scheduling optimization

## AI-Powered Features

### Intelligent Scheduling Algorithm
Our AI considers multiple factors when suggesting assignment dates:

1. **Workload Distribution**: Analyzes existing assignments on target dates
2. **Weekly Balance**: Ensures reasonable assignment spread across weeks
3. **Subject Clustering**: Prevents same-subject assignment bunching
4. **Weekend Impact**: Discourages weekend assignments for better work-life balance
5. **Exam Period Detection**: Identifies high-stress periods automatically
6. **Assignment Type Analysis**: Considers whether assignments are tests, projects, or homework

### Smart Scoring System
Each potential assignment date receives a score (0-100) based on:
- Number of competing assignments (-15 points each)
- Weekend scheduling (-30 points)
- Weekly overload penalties (-10 to -20 points)
- Subject clustering penalties (-8 points per nearby same-subject assignment)
- Optimal day bonuses (Tuesday-Thursday preferred)

## Installation & Setup

### Quick Start
1. Download all files to a folder
2. Open `index.html` in a web browser
3. Choose Student Portal or Teacher Dashboard
4. Start using immediately - no installation required!

### File Structure
```
├── index.html          # Main launcher page
├── student_app.html     # Student assignment portal
├── teacher_app.html     # Teacher scheduling dashboard
└── README.md           # This documentation
```

### Browser Requirements
- Modern web browser (Chrome, Firefox, Safari, Edge)
- JavaScript enabled
- LocalStorage support

## How to Use

### For Students
1. Open the **Student Portal** from the main launcher
2. Fill in assignment details:
   - Subject name
   - Assignment title
   - Due date
   - Optional description
3. View your stress level indicators and upcoming deadlines
4. Monitor your workload balance in the statistics section

### For Teachers
1. Open the **Teacher Dashboard** from the main launcher
2. Use the Smart Assignment Scheduler:
   - Enter subject and assignment name
   - Select your preferred due date
   - Get AI-powered recommendations
3. Review the Student Workload Heatmap to see stress patterns
4. Analyze AI insights for optimal scheduling decisions

## Data Management

### Cross-Application Sharing
- Student data automatically appears in teacher dashboard
- Real-time synchronization using browser LocalStorage
- No external servers or accounts required
- Data persists between browser sessions

### Privacy & Security
- All data stored locally on user's device
- No personal information transmitted externally
- No account registration required
- Complete user control over data

## Key Benefits

### For Students
- ✅ **Stress Reduction**: Visual workload tracking prevents overcommitment
- ✅ **Better Planning**: Clear view of upcoming deadlines
- ✅ **Performance Improvement**: Balanced workload leads to better results

### For Teachers
- ✅ **Informed Decisions**: Data-driven assignment scheduling
- ✅ **Student Wellbeing**: Prevent academic burnout through balance
- ✅ **Collaborative Planning**: Awareness of cross-subject assignments

### For Schools
- ✅ **Improved Outcomes**: Better student performance and satisfaction
- ✅ **Reduced Stress**: Healthier academic environment
- ✅ **Data Insights**: Understanding of workload patterns

## Technical Details

### AI Algorithm Highlights

**Stress Level Calculation**:
```
Level 0 (Low): 0-1 assignments per day
Level 1 (Moderate): 2-3 assignments per day
Level 2 (High): 4-5 assignments per day
Level 3 (Critical): 6+ assignments per day
```

**Optimal Scheduling Factors**:
- Weekday preference (Tuesday-Thursday optimal)
- Weekly distribution balance (max 8 assignments per week)
- Subject spacing (3+ day gaps between same-subject assignments)
- Assignment type conflicts (avoid multiple tests same day)

### Performance Features
- Responsive design for all device sizes
- Real-time data updates every 5 seconds
- Smooth animations and modern UI components
- Accessibility-focused design principles

## Customization

### Colors & Branding
The system uses St Philip's College brand colors:
- Primary: `#e53e3e` (College red)
- Secondary: `#667eea` (Accent blue)
- Background: `#f5f7fa` (Light gray)

### Configuration Options
- Stress level thresholds can be adjusted in JavaScript
- Calendar view can be modified for different academic calendars
- Suggestion algorithms can be fine-tuned for specific needs

## Future Enhancements

### Planned Features
- 📧 **Email Integration**: Automatic reminder notifications
- 📊 **Advanced Analytics**: Detailed performance metrics
- 🔄 **Subject Coordination**: Direct teacher-to-teacher communication
- 📱 **Mobile App**: Native iOS/Android applications
- 🏫 **School Integration**: LMS and student information system connectivity

### Scalability
- Multi-school deployment capability
- Advanced user role management
- Cloud-based data synchronization
- Integration with existing school systems

## Support

### Getting Help
- Review this documentation for common questions
- Check browser console for any error messages
- Ensure JavaScript is enabled in browser settings
- Try refreshing the page if data doesn't appear

### Troubleshooting
- **Data not showing**: Check that both student and teacher apps are using the same browser
- **Suggestions not working**: Ensure valid dates are entered in the form
- **Layout issues**: Try different browser or check screen resolution

## Credits

**Developed for St Philip's College**
*Excellence in Education • Student Wellbeing First*

This system demonstrates the power of technology in supporting educational excellence while prioritizing student mental health and academic success.

---

**Assignment Stress Radar** - Making academic life better, one assignment at a time. 🎯
