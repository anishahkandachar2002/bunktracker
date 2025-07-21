# 📚 Bunk Tracker - Complete Documentation Index

## 🎯 Overview

The **Bunk Tracker** is a web-based attendance calculator that helps students determine how many classes they can safely skip while maintaining the mandatory 75% attendance requirement. This documentation suite provides comprehensive coverage of all APIs, components, and usage patterns.

---

## 📖 Documentation Structure

### 📋 [API Documentation](./API_DOCUMENTATION.md)
**Comprehensive API Reference**
- Complete function signatures and parameters
- Detailed mathematical formulas and calculations
- Data structures and flow diagrams
- Integration guidelines and examples
- Error handling and troubleshooting

**Best for**: Developers implementing features, understanding core logic, integration planning

### 🎨 [Component Guide](./COMPONENT_GUIDE.md)
**UI Components and Styling Reference**
- Detailed component hierarchy and structure
- CSS styling system and customization options
- Responsive design patterns and breakpoints
- Accessibility features and best practices
- Component lifecycle and event handling

**Best for**: UI/UX developers, designers, front-end customization

### 🚀 [Quick Reference](./QUICK_REFERENCE.md)
**Essential Information at a Glance**
- Core function signatures and usage
- Common code patterns and snippets
- Debugging commands and troubleshooting
- Customization examples and modifications
- Testing procedures and validation

**Best for**: Experienced developers, quick lookups, debugging sessions

---

## 🏗️ Application Architecture Overview

### Technology Stack
- **Frontend**: HTML5, CSS3, Vanilla JavaScript
- **PDF Generation**: jsPDF library (v2.5.1)
- **Styling**: Custom CSS with responsive design
- **Deployment**: Static web application

### Core Components
```
Bunk Tracker Application
├── User Interface Layer
│   ├── Subject Forms (Dynamic)
│   ├── Action Buttons
│   └── Results Display
├── Calculation Engine
│   ├── Attendance Mathematics
│   ├── Validation Logic
│   └── Result Processing
└── Export System
    └── PDF Generation
```

### Key Features
- ✅ **Dynamic Form Management** - Add/remove subjects on demand
- 🧮 **Real-time Calculations** - Instant attendance requirement computation
- 📊 **Visual Results Display** - Clear tabular presentation of results
- 📄 **PDF Export** - Downloadable reports for record keeping
- 📱 **Responsive Design** - Works on desktop, tablet, and mobile devices

---

## 🚀 Getting Started

### For Users
1. **Open the Application**: Load `index.html` in a web browser
2. **Add Subjects**: Use the "➕ Add Subject" button to create forms
3. **Input Data**: Fill in attendance information for each subject
4. **Calculate**: Click "✅ Submit & Calculate" to see results
5. **Export**: Use "📄 Download PDF" to save your report

### For Developers
1. **Read the API Documentation**: Start with [API_DOCUMENTATION.md](./API_DOCUMENTATION.md)
2. **Understand Components**: Review [COMPONENT_GUIDE.md](./COMPONENT_GUIDE.md)
3. **Quick Reference**: Bookmark [QUICK_REFERENCE.md](./QUICK_REFERENCE.md)
4. **Explore the Code**: Examine `index.html` for implementation details

---

## 🔧 Core Functions Reference

### Public API Functions

| Function | Purpose | Parameters | Returns |
|----------|---------|------------|---------|
| `addSubject()` | Creates new subject form | None | `void` |
| `calculateAll()` | Processes attendance calculations | None | `void` |
| `downloadPDF()` | Generates PDF report | None | `void` |

### Global Variables

| Variable | Type | Purpose | Initial Value |
|----------|------|---------|---------------|
| `subjectCount` | `number` | Tracks subject forms | `0` |

---

## 📊 Mathematical Foundation

### Core Formula
The application calculates attendance requirements using this logic:

```
Given:
- Sessions Over (S₀): Total sessions conducted to date
- Sessions Attended (Sₐ): Sessions actually attended
- Classes Left (C): Remaining classes in semester

Calculate:
- Sessions Left (Sₗ) = C × 3
- Total Sessions (Sₜ) = S₀ + Sₗ  
- Required Sessions (Sᵣ) = ⌈0.75 × Sₜ⌉
- Must Attend Classes = ⌈(Sᵣ - Sₐ) ÷ 3⌉
- Can Bunk Classes = C - Must Attend Classes
```

### Key Assumptions
- **75% Minimum Attendance**: Industry standard requirement
- **3 Sessions per Class**: Each class counts as 3 attendance sessions
- **Conservative Rounding**: Uses `Math.ceil()` for safety margins

---

## 🎨 Styling and Theming

### Color Palette
```css
Primary Blue:    #007bff
Hover Blue:      #0056b3
Dark Blue:       #004080
Light Blue:      #e6f2ff
Background:      #f0f8ff
Text Dark:       #333
Text Light:      #555
```

### Component Classes
```css
.container       /* Main application wrapper */
.subject         /* Individual subject forms */
.footer          /* Attribution footer */
button           /* All interactive buttons */
input            /* Form input fields */
table            /* Results display table */
```

---

## 🔍 Common Use Cases

### Student Scenarios

1. **Good Attendance Student**
   ```
   Input:  30 sessions over, 28 attended, 10 classes left
   Result: Can bunk 7 classes, must attend 3
   ```

2. **Poor Attendance Student**
   ```
   Input:  30 sessions over, 20 attended, 10 classes left
   Result: Can bunk 0 classes, must attend 10
   ```

3. **Borderline Student**
   ```
   Input:  40 sessions over, 30 attended, 8 classes left
   Result: Can bunk 5 classes, must attend 3
   ```

### Developer Scenarios

1. **Adding Custom Validation**
   - Modify `calculateAll()` function
   - Add validation before processing
   - Display custom error messages

2. **Changing Attendance Threshold**
   - Update the 0.75 constant in calculations
   - Modify display text accordingly
   - Update documentation

3. **Adding New Export Formats**
   - Create new export functions
   - Add corresponding buttons
   - Implement format-specific logic

---

## 🐛 Troubleshooting Guide

### Common Issues

| Issue | Symptoms | Solution | Reference |
|-------|----------|----------|-----------|
| PDF not downloading | Button click has no effect | Check jsPDF library loading | [Quick Reference](./QUICK_REFERENCE.md#common-issues--solutions) |
| Calculations incorrect | Wrong attendance percentages | Verify input validation | [API Documentation](./API_DOCUMENTATION.md#error-handling) |
| Table not showing | Results don't appear | Check table display property | [Component Guide](./COMPONENT_GUIDE.md#common-component-issues) |
| Mobile layout broken | Poor mobile experience | Review responsive CSS | [Component Guide](./COMPONENT_GUIDE.md#responsive-design) |

### Debug Commands

```javascript
// Check application state
console.log('Subject count:', subjectCount);

// Validate all inputs
for (let i = 0; i < subjectCount; i++) {
  console.log(`Subject ${i}:`, {
    name: document.getElementById(`sub${i}`).value,
    sessionsOver: document.getElementById(`sessionsOver${i}`).value,
    sessionsAttended: document.getElementById(`sessionsAttended${i}`).value,
    classesLeft: document.getElementById(`classesLeft${i}`).value
  });
}

// Test PDF library
console.log('jsPDF available:', typeof window.jspdf !== 'undefined');
```

---

## 🔧 Extension Points

### Adding New Features

1. **Data Persistence**
   ```javascript
   // Save to localStorage
   function saveData() {
     const data = collectAllSubjectData();
     localStorage.setItem('bunkTrackerData', JSON.stringify(data));
   }
   ```

2. **Multiple Attendance Thresholds**
   ```javascript
   function calculateWithThreshold(threshold) {
     const minRequired = Math.ceil(threshold * totalSessions);
     // Rest of calculation logic
   }
   ```

3. **Subject Templates**
   ```javascript
   function addSubjectTemplate(templateName) {
     const templates = {
       'engineering': { sessionsPerClass: 3, defaultThreshold: 0.75 },
       'medical': { sessionsPerClass: 4, defaultThreshold: 0.80 }
     };
     // Apply template logic
   }
   ```

### Customization Options

1. **Theme Variations**
   - Dark mode implementation
   - Custom color schemes
   - Alternative layouts

2. **Calculation Methods**
   - Different attendance thresholds
   - Custom session multipliers
   - Alternative rounding strategies

3. **Export Formats**
   - Excel spreadsheets
   - CSV files
   - Email integration

---

## 📱 Browser Compatibility

### Supported Browsers
- **Chrome**: 60+ ✅
- **Firefox**: 55+ ✅
- **Safari**: 12+ ✅
- **Edge**: 79+ ✅

### Required Features
- ES6 JavaScript support
- CSS3 flexbox and grid
- HTML5 form validation
- File download APIs

### Progressive Enhancement
- Core functionality works without JavaScript
- CSS provides fallback styling
- HTML forms provide basic validation

---

## 📄 File Structure

```
bunk-tracker/
├── index.html                 # Main application file
├── README.md                  # Project overview
├── s1.png                     # Screenshot 1
├── s2.png                     # Screenshot 2
└── documentation/
    ├── DOCUMENTATION_INDEX.md # This file
    ├── API_DOCUMENTATION.md   # Complete API reference
    ├── COMPONENT_GUIDE.md     # UI component details
    └── QUICK_REFERENCE.md     # Developer quick reference
```

---

## 🤝 Contributing Guidelines

### Code Style
- Use meaningful variable names
- Add comments for complex calculations
- Follow existing indentation patterns
- Test changes across browsers

### Documentation Updates
- Update relevant documentation files
- Include code examples for new features
- Maintain consistent formatting
- Add troubleshooting entries for new issues

### Testing Checklist
- [ ] All functions work as expected
- [ ] Calculations are mathematically correct
- [ ] UI responds properly on all devices
- [ ] PDF generation works in all browsers
- [ ] No console errors or warnings

---

## 📞 Support and Resources

### Documentation Navigation
- **Need API details?** → [API_DOCUMENTATION.md](./API_DOCUMENTATION.md)
- **Working with UI?** → [COMPONENT_GUIDE.md](./COMPONENT_GUIDE.md)
- **Quick lookup?** → [QUICK_REFERENCE.md](./QUICK_REFERENCE.md)
- **Getting started?** → Continue reading this file

### External Resources
- [jsPDF Documentation](https://raw.githack.com/MrRio/jsPDF/master/docs/)
- [MDN Web Docs - JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- [CSS-Tricks - Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

### Project Information
- **Author**: Anisha
- **License**: Not specified
- **Repository**: [GitHub](https://anishahkandachar2002.github.io/bunktracker/)
- **Live Demo**: [Demo Link](https://anishahkandachar2002.github.io/bunktracker/)

---

## 📈 Version History

### Current Version (Latest)
- ✅ Core attendance calculation functionality
- ✅ Dynamic subject form management
- ✅ PDF export capability
- ✅ Responsive design implementation
- ✅ Comprehensive documentation suite

### Potential Future Enhancements
- 🔄 Data persistence with localStorage
- 📊 Advanced analytics and charts
- 🎨 Theme customization options
- 📧 Email integration for reports
- 🔐 User accounts and data sync

---

*This documentation index provides a complete overview of the Bunk Tracker application. Use the linked documents for detailed information on specific aspects of the system. For questions or contributions, please refer to the project repository.*