# 📚 Bunk Tracker - API Documentation

## Overview

The Bunk Tracker is a web application designed to help students calculate attendance requirements based on the 75% attendance rule. This documentation covers all public APIs, functions, and components available in the application.

---

## 🏗️ Application Architecture

### Core Components

1. **HTML Structure** - User interface components
2. **JavaScript Functions** - Core calculation and interaction logic
3. **CSS Styling** - Visual presentation layer

---

## 📋 Public APIs and Functions

### 1. `addSubject()`

**Purpose**: Dynamically adds a new subject entry form to the interface.

**Signature**: 
```javascript
function addSubject()
```

**Parameters**: None

**Returns**: `void`

**Description**: 
Creates a new subject form with input fields for:
- Subject Name
- Total Sessions Over Till Date
- Sessions Attended Till Date
- Remaining Number of Classes

**Usage Example**:
```javascript
// Called when user clicks "➕ Add Subject" button
addSubject();
```

**Implementation Details**:
- Increments global `subjectCount` variable
- Creates a new DOM element with class `subject`
- Appends the new form to `subjectsContainer`
- Generates unique IDs for each input field using the subject count

**DOM Elements Created**:
- `sub{n}` - Subject name input
- `sessionsOver{n}` - Total sessions input
- `sessionsAttended{n}` - Attended sessions input
- `classesLeft{n}` - Remaining classes input

---

### 2. `calculateAll()`

**Purpose**: Processes all subject data and calculates attendance requirements.

**Signature**:
```javascript
function calculateAll()
```

**Parameters**: None

**Returns**: `void`

**Description**:
Performs attendance calculations for all subjects and displays results in a table format. Calculates:
- Minimum classes that must be attended
- Maximum classes that can be bunked
- Expected final attendance percentage

**Usage Example**:
```javascript
// Called when user clicks "✅ Submit & Calculate" button
calculateAll();
```

**Calculation Logic**:
1. **Sessions Calculation**: `sessionsLeft = classesLeft * 3`
2. **Total Sessions**: `totalSessions = sessionsOver + sessionsLeft`
3. **Minimum Required**: `minSessionsToAttend = Math.ceil(0.75 * totalSessions)`
4. **Sessions to Attend**: `sessionsToAttend = minSessionsToAttend - sessionsAttended`
5. **Classes to Attend**: `mustAttendClasses = Math.ceil(sessionsToAttend / 3)`
6. **Classes Can Bunk**: `canBunkClasses = classesLeft - mustAttendClasses`
7. **Final Percentage**: `((finalAttended / totalSessions) * 100).toFixed(2)`

**Output Format**:
```
| Subject | Must Attend (Classes) | Can Bunk (Classes) | Expected Attendance (%) |
|---------|----------------------|-------------------|------------------------|
| Math    | 5                    | 2                 | 75.50%                 |
```

---

### 3. `downloadPDF()`

**Purpose**: Generates and downloads a PDF report of the attendance calculations.

**Signature**:
```javascript
function downloadPDF()
```

**Parameters**: None

**Returns**: `void`

**Dependencies**: 
- jsPDF library (loaded via CDN)

**Description**:
Creates a formatted PDF document containing all calculation results and saves it as "bunk-tracker-report.pdf".

**Usage Example**:
```javascript
// Called when user clicks "📄 Download PDF" button
downloadPDF();
```

**PDF Content Structure**:
```
Bunk Tracker Report
-------------------
Subject: [Subject Name]
Must Attend (Classes): [Number]
Can Bunk (Classes): [Number]
Expected Attendance: [Percentage]%

[Repeated for each subject]

Made by Anisha ❤️
```

---

## 🔧 Global Variables

### `subjectCount`

**Type**: `number`

**Initial Value**: `0`

**Purpose**: Tracks the number of subjects added to maintain unique IDs for form elements.

**Usage**:
```javascript
let subjectCount = 0; // Global counter
```

---

## 🎨 UI Components

### 1. Subject Form Component

**HTML Structure**:
```html
<div class="subject">
  <label>Subject Name:</label>
  <input type="text" id="sub{n}" required>
  
  <label>Total Sessions Over Till Date:</label>
  <input type="number" id="sessionsOver{n}" required>
  
  <label>Sessions Attended Till Date:</label>
  <input type="number" id="sessionsAttended{n}" required>
  
  <label>Remaining Number of Classes:</label>
  <input type="number" id="classesLeft{n}" required>
</div>
```

**CSS Classes**:
- `.subject` - Container styling with background and padding
- Input fields inherit global styling

### 2. Results Table Component

**HTML Structure**:
```html
<table id="resultTable">
  <thead>
    <tr>
      <th>Subject</th>
      <th>Must Attend (Classes)</th>
      <th>Can Bunk (Classes)</th>
      <th>Expected Attendance (%)</th>
    </tr>
  </thead>
  <tbody id="resultBody">
    <!-- Dynamic content populated by calculateAll() -->
  </tbody>
</table>
```

**Visibility**: Initially hidden (`display:none`), shown after calculations

### 3. Action Buttons

**Add Subject Button**:
```html
<button onclick="addSubject()">➕ Add Subject</button>
```

**Calculate Button**:
```html
<button onclick="calculateAll()">✅ Submit & Calculate</button>
```

**Download PDF Button**:
```html
<button onclick="downloadPDF()">📄 Download PDF</button>
```

---

## 📊 Data Flow

### Input Data Structure

For each subject, the following data is required:

```javascript
{
  subjectName: string,           // Subject identifier
  sessionsOver: number,          // Total sessions conducted so far
  sessionsAttended: number,      // Sessions actually attended
  classesLeft: number           // Remaining classes in semester
}
```

### Output Data Structure

Calculated results for each subject:

```javascript
{
  subject: string,              // Subject name
  mustAttendClasses: number,    // Minimum classes to attend
  canBunkClasses: number,       // Maximum classes that can be skipped
  finalPercentage: string       // Expected attendance percentage
}
```

---

## 🧮 Mathematical Formulas

### Core Attendance Calculation

The application uses the following mathematical approach:

1. **Session Multiplier**: Each class = 3 sessions
2. **Minimum Attendance**: 75% of total sessions
3. **Rounding**: Uses `Math.ceil()` for conservative estimates

**Formula Breakdown**:

```
Total Future Sessions = Remaining Classes × 3
Total Sessions = Sessions Over + Total Future Sessions
Required Sessions = ⌈0.75 × Total Sessions⌉
Sessions Still Needed = Required Sessions - Sessions Attended
Classes Must Attend = ⌈Sessions Still Needed ÷ 3⌉
Classes Can Bunk = Remaining Classes - Classes Must Attend
```

---

## 🚀 Usage Examples

### Basic Usage Workflow

1. **Initialize Application**:
   ```javascript
   // Application loads with one subject form pre-added
   addSubject(); // Called automatically on page load
   ```

2. **Add Multiple Subjects**:
   ```javascript
   // User can add more subjects
   addSubject(); // Adds second subject
   addSubject(); // Adds third subject
   ```

3. **Input Data Example**:
   ```
   Subject: Mathematics
   Total Sessions Over: 45
   Sessions Attended: 40
   Remaining Classes: 15
   ```

4. **Calculate Results**:
   ```javascript
   calculateAll(); // Processes all subjects and shows results
   ```

5. **Export Results**:
   ```javascript
   downloadPDF(); // Generates downloadable report
   ```

### Advanced Usage Scenarios

**Scenario 1: Student with Good Attendance**
```
Input:  Sessions Over: 30, Attended: 28, Classes Left: 10
Result: Can Bunk: 7 classes, Must Attend: 3 classes
```

**Scenario 2: Student with Poor Attendance**
```
Input:  Sessions Over: 30, Attended: 20, Classes Left: 10
Result: Can Bunk: 0 classes, Must Attend: 10 classes
```

---

## 🔍 Error Handling

### Input Validation

- All input fields are marked as `required`
- Number inputs automatically validate for numeric values
- Application assumes valid positive integers for calculations

### Edge Cases Handled

1. **Negative Bunk Classes**: If calculated bunk classes < 0, sets to 0
2. **Division by Zero**: Avoided by ensuring total sessions > 0
3. **Rounding**: Uses `Math.ceil()` for conservative attendance requirements

---

## 🎯 Integration Guidelines

### Adding New Features

To extend the application:

1. **New Calculation Method**:
   ```javascript
   function customCalculation(attendanceThreshold) {
     // Custom logic here
     const minRequired = Math.ceil(attendanceThreshold * totalSessions);
     // Return results
   }
   ```

2. **Additional Input Fields**:
   ```javascript
   // Modify addSubject() function to include new fields
   div.innerHTML += `
     <label>New Field:</label>
     <input type="text" id="newField${subjectCount}" required>
   `;
   ```

3. **Export Formats**:
   ```javascript
   function downloadExcel() {
     // Implementation for Excel export
   }
   ```

### Styling Customization

Key CSS classes for customization:

- `.container` - Main application container
- `.subject` - Individual subject form styling
- `button` - Action button styling
- `table` - Results table styling

---

## 📱 Browser Compatibility

### Supported Browsers

- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+

### Required Features

- ES6 JavaScript support
- DOM manipulation APIs
- jsPDF library compatibility

---

## 🔧 Dependencies

### External Libraries

1. **jsPDF** (v2.5.1)
   - Source: `https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js`
   - Purpose: PDF generation functionality
   - Usage: `const { jsPDF } = window.jspdf;`

### Internal Dependencies

- No internal JavaScript modules
- Self-contained HTML file
- Inline CSS styling

---

## 🐛 Troubleshooting

### Common Issues

1. **PDF Download Not Working**:
   - Ensure jsPDF library is loaded
   - Check browser popup blocker settings

2. **Calculations Incorrect**:
   - Verify input values are positive integers
   - Check that sessions attended ≤ sessions over

3. **Form Not Submitting**:
   - Ensure all required fields are filled
   - Check JavaScript console for errors

### Debug Mode

To enable debugging, add to browser console:

```javascript
// Log all subject data
for (let i = 0; i < subjectCount; i++) {
  console.log({
    subject: document.getElementById(`sub${i}`).value,
    sessionsOver: document.getElementById(`sessionsOver${i}`).value,
    sessionsAttended: document.getElementById(`sessionsAttended${i}`).value,
    classesLeft: document.getElementById(`classesLeft${i}`).value
  });
}
```

---

## 📄 License and Credits

**Created by**: Anisha  
**License**: Not specified  
**Repository**: [GitHub Link](https://anishahkandachar2002.github.io/bunktracker/)

---

*This documentation covers all public APIs and components as of the current version. For updates or additional features, please refer to the source code or contact the maintainer.*