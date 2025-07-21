# 🚀 Bunk Tracker - Quick Reference Guide

## 📋 Essential Functions

### Core JavaScript Functions

```javascript
// Add new subject form
addSubject()

// Calculate attendance for all subjects
calculateAll()

// Generate and download PDF report
downloadPDF()
```

### Global Variables

```javascript
let subjectCount = 0; // Tracks number of subjects added
```

---

## 🏗️ HTML Structure Reference

### Main Container
```html
<div class="container">
  <h2>📘 Bunk Tracker - Maintain 75% Attendance</h2>
  <div id="subjectsContainer"></div>
  <!-- Action buttons -->
  <table id="resultTable" style="display:none;"></table>
</div>
```

### Subject Form Template
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

### Action Buttons
```html
<button onclick="addSubject()">➕ Add Subject</button>
<button onclick="calculateAll()">✅ Submit & Calculate</button>
<button onclick="downloadPDF()">📄 Download PDF</button>
```

---

## 🧮 Calculation Formula

### Core Logic
```javascript
const sessionsLeft = classesLeft * 3;
const totalSessions = sessionsOver + sessionsLeft;
const minSessionsToAttend = Math.ceil(0.75 * totalSessions);
const sessionsToAttend = minSessionsToAttend - sessionsAttended;
const mustAttendClasses = Math.ceil(sessionsToAttend / 3);
const canBunkClasses = classesLeft - mustAttendClasses;
const finalPercentage = ((finalAttended / totalSessions) * 100).toFixed(2);
```

### Key Constants
- **Attendance Threshold**: 75% (0.75)
- **Sessions per Class**: 3
- **Rounding Method**: `Math.ceil()` for conservative estimates

---

## 🎨 CSS Classes Quick Reference

### Layout Classes
```css
.container      /* Main app wrapper */
.subject        /* Subject form container */
.footer         /* Footer attribution */
```

### Element Styling
```css
button          /* All buttons */
input           /* All input fields */
label           /* All form labels */
table           /* Results table */
th, td          /* Table cells */
```

### Color Scheme
```css
/* Primary Colors */
#007bff         /* Button background */
#0056b3         /* Button hover */
#004080         /* Header text */

/* Backgrounds */
#e6f2ff         /* Page background */
white           /* Container background */
#f0f8ff         /* Subject form background */
```

---

## 🔧 Common Code Patterns

### Adding Custom Fields
```javascript
function addSubject() {
  const container = document.getElementById('subjectsContainer');
  const div = document.createElement('div');
  div.className = 'subject';
  div.innerHTML = `
    <!-- Your custom fields here -->
    <label>Custom Field:</label>
    <input type="text" id="custom${subjectCount}" required>
  `;
  container.appendChild(div);
  subjectCount++;
}
```

### Input Validation
```javascript
function validateForm() {
  for (let i = 0; i < subjectCount; i++) {
    const attended = parseInt(document.getElementById(`sessionsAttended${i}`).value);
    const total = parseInt(document.getElementById(`sessionsOver${i}`).value);
    
    if (attended > total) {
      alert('Sessions attended cannot exceed total sessions');
      return false;
    }
  }
  return true;
}
```

### Custom Calculations
```javascript
function customAttendanceCalculation(threshold = 0.75) {
  // Your custom logic here
  const minRequired = Math.ceil(threshold * totalSessions);
  return minRequired;
}
```

---

## 📱 Responsive Breakpoints

```css
/* Desktop: > 768px (default styles) */
/* Tablet: 768px - 480px */
@media (max-width: 768px) {
  .container { padding: 15px; }
}

/* Mobile: < 480px */
@media (max-width: 480px) {
  button { width: 100%; margin: 5px 0; }
  table { font-size: 12px; }
}
```

---

## 🔍 Debugging Snippets

### Log All Subject Data
```javascript
for (let i = 0; i < subjectCount; i++) {
  console.log({
    subject: document.getElementById(`sub${i}`).value,
    sessionsOver: document.getElementById(`sessionsOver${i}`).value,
    sessionsAttended: document.getElementById(`sessionsAttended${i}`).value,
    classesLeft: document.getElementById(`classesLeft${i}`).value
  });
}
```

### Check PDF Library
```javascript
if (typeof window.jspdf !== 'undefined') {
  console.log('jsPDF loaded successfully');
} else {
  console.error('jsPDF not loaded');
}
```

### Validate Calculations
```javascript
function debugCalculation(subjectIndex) {
  const i = subjectIndex;
  const sessionsOver = parseInt(document.getElementById(`sessionsOver${i}`).value);
  const sessionsAttended = parseInt(document.getElementById(`sessionsAttended${i}`).value);
  const classesLeft = parseInt(document.getElementById(`classesLeft${i}`).value);
  
  console.log('Input:', { sessionsOver, sessionsAttended, classesLeft });
  
  const sessionsLeft = classesLeft * 3;
  const totalSessions = sessionsOver + sessionsLeft;
  const minSessionsToAttend = Math.ceil(0.75 * totalSessions);
  
  console.log('Calculated:', { sessionsLeft, totalSessions, minSessionsToAttend });
}
```

---

## 🚨 Common Issues & Solutions

### Issue: PDF not downloading
```javascript
// Check if jsPDF is loaded
if (!window.jspdf) {
  console.error('jsPDF library not loaded');
}

// Ensure function is called after calculation
if (subjectCount === 0) {
  alert('Please add subjects and calculate first');
  return;
}
```

### Issue: Table not showing
```javascript
// Force table to display
const resultTable = document.getElementById("resultTable");
resultTable.style.display = "table";
resultTable.style.visibility = "visible";
```

### Issue: Form validation failing
```javascript
// Check required fields
const requiredFields = ['sub', 'sessionsOver', 'sessionsAttended', 'classesLeft'];
for (let i = 0; i < subjectCount; i++) {
  requiredFields.forEach(field => {
    const element = document.getElementById(`${field}${i}`);
    if (!element.value) {
      console.error(`Missing value for ${field}${i}`);
    }
  });
}
```

---

## 📊 Data Structures

### Input Data Object
```javascript
const subjectData = {
  name: string,           // Subject name
  sessionsOver: number,   // Total sessions conducted
  sessionsAttended: number, // Sessions actually attended
  classesLeft: number     // Remaining classes
};
```

### Output Data Object
```javascript
const calculationResult = {
  subject: string,              // Subject name
  mustAttendClasses: number,    // Minimum classes to attend
  canBunkClasses: number,       // Maximum classes that can be skipped
  finalPercentage: string       // Expected attendance percentage
};
```

---

## 🔗 External Dependencies

### jsPDF Library
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
```

### Usage
```javascript
const { jsPDF } = window.jspdf;
const doc = new jsPDF();
doc.text("Content", x, y);
doc.save("filename.pdf");
```

---

## 🎯 Event Handlers

### Button Events
```javascript
// Inline event handlers
onclick="addSubject()"
onclick="calculateAll()"
onclick="downloadPDF()"
```

### Alternative Event Binding
```javascript
// Modern event listeners (alternative approach)
document.getElementById('addBtn').addEventListener('click', addSubject);
document.getElementById('calcBtn').addEventListener('click', calculateAll);
document.getElementById('pdfBtn').addEventListener('click', downloadPDF);
```

---

## 🔄 Application Flow

```
1. Page Load → addSubject() called automatically
2. User fills form → Validation on input
3. User clicks "Calculate" → calculateAll() processes data
4. Results displayed → Table becomes visible
5. User clicks "PDF" → downloadPDF() generates report
```

---

## 📝 Customization Examples

### Change Attendance Threshold
```javascript
// Modify in calculateAll() function
const minSessionsToAttend = Math.ceil(0.80 * totalSessions); // 80% instead of 75%
```

### Add New Button
```html
<button onclick="clearAll()">🗑️ Clear All</button>
```

```javascript
function clearAll() {
  document.getElementById('subjectsContainer').innerHTML = '';
  document.getElementById('resultTable').style.display = 'none';
  subjectCount = 0;
  addSubject(); // Add one empty form
}
```

### Custom Styling
```css
/* Dark theme example */
body { background-color: #2d3748; color: white; }
.container { background: #4a5568; }
.subject { background: #2d3748; border-color: #4a5568; }
button { background-color: #38a169; }
```

---

## 🔍 Testing Commands

### Browser Console Tests
```javascript
// Test subject addition
addSubject();
console.log('Subject count:', subjectCount);

// Test calculation with sample data
document.getElementById('sub0').value = 'Math';
document.getElementById('sessionsOver0').value = '30';
document.getElementById('sessionsAttended0').value = '25';
document.getElementById('classesLeft0').value = '10';
calculateAll();

// Test PDF generation
downloadPDF();
```

---

*This quick reference provides essential information for working with the Bunk Tracker application. For detailed documentation, refer to API_DOCUMENTATION.md and COMPONENT_GUIDE.md.*