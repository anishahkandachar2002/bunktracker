# 🎨 Bunk Tracker - Component Guide

## Overview

This guide provides detailed documentation for all UI components in the Bunk Tracker application, including their properties, styling, events, and customization options.

---

## 🏗️ Component Hierarchy

```
Application Root
├── Container (.container)
│   ├── Header (h2)
│   ├── Subjects Container (#subjectsContainer)
│   │   └── Subject Components (.subject) [Dynamic]
│   ├── Action Buttons
│   │   ├── Add Subject Button
│   │   ├── Calculate Button
│   │   └── Download PDF Button
│   └── Results Table (#resultTable)
│       ├── Table Header
│       └── Table Body (#resultBody) [Dynamic]
└── Footer (.footer)
```

---

## 📦 Core Components

### 1. Application Container

**Element**: `<div class="container">`

**Purpose**: Main wrapper for the entire application

**Properties**:
```css
.container {
  max-width: 800px;
  margin: auto;
  background: white;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 0 25px rgba(0, 0, 0, 0.1);
}
```

**Responsive Behavior**:
- Centers content on the page
- Constrains maximum width to 800px
- Provides consistent padding and styling

**Usage**:
```html
<div class="container">
  <!-- All application content -->
</div>
```

---

### 2. Subject Form Component

**Element**: `<div class="subject">`

**Purpose**: Individual subject data entry form

**Dynamic Generation**: Created via `addSubject()` function

**Properties**:
```css
.subject {
  margin-bottom: 25px;
  padding: 20px;
  background: #f0f8ff;
  border: 1px solid #dcdcdc;
  border-radius: 10px;
}
```

**Structure**:
```html
<div class="subject">
  <!-- Subject Name Field -->
  <label>Subject Name:</label>
  <input type="text" id="sub{n}" required>
  
  <!-- Total Sessions Field -->
  <label>Total Sessions Over Till Date:</label>
  <input type="number" id="sessionsOver{n}" required>
  
  <!-- Attended Sessions Field -->
  <label>Sessions Attended Till Date:</label>
  <input type="number" id="sessionsAttended{n}" required>
  
  <!-- Remaining Classes Field -->
  <label>Remaining Number of Classes:</label>
  <input type="number" id="classesLeft{n}" required>
</div>
```

**Field Specifications**:

| Field | ID Pattern | Type | Required | Purpose |
|-------|------------|------|----------|---------|
| Subject Name | `sub{n}` | text | Yes | Subject identifier |
| Total Sessions | `sessionsOver{n}` | number | Yes | Sessions conducted to date |
| Attended Sessions | `sessionsAttended{n}` | number | Yes | Sessions actually attended |
| Remaining Classes | `classesLeft{n}` | number | Yes | Future classes in semester |

**Validation Rules**:
- All fields are required
- Numeric fields accept positive integers only
- Sessions attended should not exceed total sessions

---

### 3. Input Field Component

**Element**: `<input>` (various types)

**Base Styling**:
```css
input {
  width: 100%;
  padding: 10px;
  margin-top: 5px;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-sizing: border-box;
}
```

**Types Used**:
1. **Text Input** (`type="text"`)
   - Used for subject names
   - Accepts any string value

2. **Number Input** (`type="number"`)
   - Used for all numeric fields
   - Provides built-in validation
   - Includes spinner controls

**Accessibility Features**:
- Associated with labels via proper HTML structure
- Required attribute for validation
- Semantic input types for better mobile experience

---

### 4. Label Component

**Element**: `<label>`

**Styling**:
```css
label {
  display: block;
  margin-top: 12px;
  font-weight: bold;
  color: #333;
}
```

**Usage Pattern**:
```html
<label>Field Description:</label>
<input type="..." id="..." required>
```

**Accessibility**: Properly associated with form controls for screen readers

---

### 5. Button Components

**Base Element**: `<button>`

**Base Styling**:
```css
button {
  background-color: #007bff;
  color: white;
  padding: 12px 18px;
  margin: 10px 5px 0 0;
  border: none;
  border-radius: 8px;
  font-size: 15px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
```

#### 5.1 Add Subject Button

**HTML**:
```html
<button onclick="addSubject()">➕ Add Subject</button>
```

**Functionality**:
- Adds new subject form to the interface
- No parameters required
- Can be clicked multiple times

**Visual Indicator**: Plus emoji (➕) for intuitive action

#### 5.2 Calculate Button

**HTML**:
```html
<button onclick="calculateAll()">✅ Submit & Calculate</button>
```

**Functionality**:
- Processes all subject data
- Displays results table
- Validates input before calculation

**Visual Indicator**: Checkmark emoji (✅) for completion action

#### 5.3 Download PDF Button

**HTML**:
```html
<button onclick="downloadPDF()">📄 Download PDF</button>
```

**Functionality**:
- Generates PDF report
- Triggers browser download
- Requires calculation to be performed first

**Visual Indicator**: Document emoji (📄) for export action

**Dependencies**: Requires jsPDF library to be loaded

---

### 6. Results Table Component

**Element**: `<table id="resultTable">`

**Initial State**: Hidden (`display: none`)

**Styling**:
```css
table {
  width: 100%;
  margin-top: 25px;
  border-collapse: collapse;
}

th, td {
  padding: 14px;
  text-align: center;
  border: 1px solid #ddd;
}

th {
  background-color: #007bff;
  color: white;
}
```

**Structure**:
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
    <!-- Dynamic rows populated by calculateAll() -->
  </tbody>
</table>
```

**Dynamic Content**: Table body is populated with calculation results

**Column Definitions**:

| Column | Data Type | Description |
|--------|-----------|-------------|
| Subject | String | Subject name from input |
| Must Attend (Classes) | Integer | Minimum classes to attend |
| Can Bunk (Classes) | Integer | Maximum classes that can be skipped |
| Expected Attendance (%) | Decimal | Final attendance percentage |

---

### 7. Header Component

**Element**: `<h2>`

**Content**: "📘 Bunk Tracker - Maintain 75% Attendance"

**Styling**:
```css
h2 {
  text-align: center;
  color: #004080;
  margin-bottom: 25px;
}
```

**Visual Elements**:
- Book emoji (📘) for educational theme
- Centered alignment
- Blue color scheme matching application theme

---

### 8. Footer Component

**Element**: `<div class="footer">`

**Content**: "Made with ❤️ by Anisha"

**Styling**:
```css
.footer {
  text-align: center;
  margin-top: 40px;
  font-size: 14px;
  color: #555;
}
```

**Purpose**: Attribution and branding

---

## 🎨 Styling System

### Color Palette

```css
/* Primary Colors */
--primary-blue: #007bff;
--primary-blue-hover: #0056b3;
--dark-blue: #004080;

/* Background Colors */
--page-background: #e6f2ff;
--container-background: white;
--subject-background: #f0f8ff;

/* Text Colors */
--primary-text: #333;
--secondary-text: #555;
--white-text: white;

/* Border Colors */
--border-light: #ccc;
--border-medium: #ddd;
--border-dark: #dcdcdc;
```

### Typography

```css
/* Font Family */
font-family: 'Segoe UI', sans-serif;

/* Font Sizes */
--header-size: 16px; /* h2 elements */
--button-size: 15px;
--footer-size: 14px;
--body-size: inherit; /* Default browser size */

/* Font Weights */
--label-weight: bold;
--normal-weight: normal;
```

### Spacing System

```css
/* Margins */
--container-margin: auto;
--subject-margin-bottom: 25px;
--label-margin-top: 12px;
--table-margin-top: 25px;
--footer-margin-top: 40px;

/* Padding */
--container-padding: 30px;
--subject-padding: 20px;
--input-padding: 10px;
--button-padding: 12px 18px;
--cell-padding: 14px;
```

### Border Radius

```css
/* Rounded Corners */
--container-radius: 15px;
--subject-radius: 10px;
--input-radius: 8px;
--button-radius: 8px;
```

---

## 🔄 Component Lifecycle

### 1. Application Initialization

```javascript
// Page load sequence
document.addEventListener('DOMContentLoaded', function() {
  addSubject(); // Adds first subject form automatically
});
```

### 2. Subject Component Creation

```javascript
function addSubject() {
  // 1. Get container reference
  const container = document.getElementById('subjectsContainer');
  
  // 2. Create new div element
  const div = document.createElement('div');
  div.className = 'subject';
  
  // 3. Set innerHTML with form fields
  div.innerHTML = `...`;
  
  // 4. Append to container
  container.appendChild(div);
  
  // 5. Increment counter
  subjectCount++;
}
```

### 3. Results Table Population

```javascript
function calculateAll() {
  // 1. Get table references
  const resultTable = document.getElementById("resultTable");
  const resultBody = document.getElementById("resultBody");
  
  // 2. Clear existing content
  resultBody.innerHTML = "";
  
  // 3. Process each subject
  for (let i = 0; i < subjectCount; i++) {
    // Calculate and add row
  }
  
  // 4. Show table
  resultTable.style.display = "table";
}
```

---

## 🎯 Event Handling

### Button Click Events

All buttons use inline `onclick` handlers:

```html
<button onclick="functionName()">Button Text</button>
```

**Available Events**:
- `onclick="addSubject()"` - Adds new subject form
- `onclick="calculateAll()"` - Processes calculations
- `onclick="downloadPDF()"` - Generates PDF report

### Form Validation Events

HTML5 validation is triggered on:
- Form submission attempts
- Field blur events (when user leaves field)
- Real-time for number inputs

---

## 🔧 Customization Guide

### Adding Custom Styling

1. **Override Existing Styles**:
```css
/* Custom button colors */
button {
  background-color: #28a745; /* Green theme */
}

button:hover {
  background-color: #218838;
}
```

2. **Add New Component Variants**:
```css
/* Warning button variant */
.button-warning {
  background-color: #ffc107;
  color: #212529;
}
```

3. **Responsive Design**:
```css
/* Mobile-first responsive design */
@media (max-width: 768px) {
  .container {
    padding: 15px;
    margin: 10px;
  }
  
  .subject {
    padding: 15px;
  }
}
```

### Adding New Input Fields

To add a new field to the subject form:

```javascript
function addSubject() {
  // ... existing code ...
  div.innerHTML = `
    <!-- Existing fields -->
    
    <!-- New field -->
    <label>New Field Label:</label>
    <input type="text" id="newField${subjectCount}" required>
  `;
  // ... rest of function
}
```

### Custom Validation

Add custom validation to inputs:

```javascript
function validateInput(inputId, validationRule) {
  const input = document.getElementById(inputId);
  const value = input.value;
  
  if (!validationRule(value)) {
    input.style.borderColor = 'red';
    return false;
  }
  
  input.style.borderColor = '#ccc';
  return true;
}

// Usage example
function customValidation() {
  return validateInput('sessionsAttended0', (val) => val >= 0 && val <= 100);
}
```

---

## 📱 Responsive Design

### Breakpoints

The application uses a mobile-first approach with these considerations:

**Desktop (> 768px)**:
- Full width container (max 800px)
- Side-by-side button layout
- Full table display

**Tablet (768px - 480px)**:
- Reduced padding
- Stacked button layout
- Scrollable table

**Mobile (< 480px)**:
- Minimal padding
- Full-width buttons
- Simplified table layout

### Mobile Optimizations

```css
@media (max-width: 480px) {
  .container {
    padding: 15px;
    margin: 5px;
  }
  
  button {
    width: 100%;
    margin: 5px 0;
  }
  
  table {
    font-size: 12px;
  }
  
  th, td {
    padding: 8px;
  }
}
```

---

## 🔍 Accessibility Features

### Semantic HTML

- Proper heading hierarchy (`h2` for main title)
- Table headers with `th` elements
- Form labels associated with inputs
- Button elements for interactive actions

### ARIA Considerations

Future improvements could include:

```html
<!-- Enhanced accessibility -->
<table id="resultTable" role="table" aria-label="Attendance calculation results">
  <thead>
    <tr role="row">
      <th role="columnheader" aria-sort="none">Subject</th>
      <!-- ... other headers -->
    </tr>
  </thead>
</table>

<!-- Form fieldsets -->
<fieldset>
  <legend>Subject Information</legend>
  <!-- Subject form fields -->
</fieldset>
```

### Keyboard Navigation

- All interactive elements are keyboard accessible
- Tab order follows logical flow
- Enter key submits forms
- Space/Enter activates buttons

---

## 🐛 Common Component Issues

### 1. Form Field Validation

**Issue**: Fields not validating properly
**Solution**: Ensure all required fields have `required` attribute

```html
<input type="number" id="field" required min="0">
```

### 2. Dynamic ID Conflicts

**Issue**: Duplicate IDs when adding multiple subjects
**Solution**: Use subjectCount in ID generation

```javascript
id="fieldName${subjectCount}"
```

### 3. Table Display Issues

**Issue**: Table not showing after calculation
**Solution**: Verify table display property is set correctly

```javascript
resultTable.style.display = "table";
```

### 4. PDF Generation Failures

**Issue**: PDF download not working
**Solution**: Check jsPDF library loading and browser compatibility

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
```

---

## 📚 Component Testing

### Manual Testing Checklist

1. **Subject Form Component**:
   - [ ] Add button creates new form
   - [ ] All fields are required
   - [ ] Number inputs only accept numbers
   - [ ] Form styling is consistent

2. **Calculation Component**:
   - [ ] Calculate button processes all subjects
   - [ ] Results table appears
   - [ ] Calculations are mathematically correct
   - [ ] Edge cases handled (negative values)

3. **PDF Component**:
   - [ ] PDF downloads successfully
   - [ ] PDF contains all subject data
   - [ ] PDF formatting is readable
   - [ ] Filename is correct

4. **Responsive Design**:
   - [ ] Mobile layout works correctly
   - [ ] Buttons are accessible on touch devices
   - [ ] Table scrolls horizontally if needed
   - [ ] Text remains readable at all sizes

---

*This component guide provides comprehensive documentation for all UI elements in the Bunk Tracker application. Use this as a reference for customization, debugging, and extending the application's functionality.*