# React.js Assignment
# Student Directory Dashboard

**Course:** React.js  
**Submission:** GitHub Repository Link

---

# Clone the Starter Project

```bash
git clone https://arifulatwork-admin@bitbucket.org/arifulatwork-admin/react-js.git
```

---

# API

Use the following free API:

```
https://jsonplaceholder.typicode.com/users
```

The API returns a list of users with the following information:

- id
- name
- username
- email
- phone
- website
- company
- address

---

# Project Objective

Build a **Student Directory Dashboard** using React.js.

The application should demonstrate your understanding of:

- useState
- useEffect
- Fetch API
- Events
- Forms
- Input Handling
- Arrays
- map()
- filter()
- Conditional Rendering
- Props
- Lifting State Up
- Multiple State Variables

---

# Rules

- Do **not** hard-code student data.
- Fetch all students from the API.
- Use React functional components.
- Use Hooks only.
- Keep your code clean and organized.
- Comment your code where necessary.
- Follow the folder structure below.

---

# Part 1 — Fetch Students

When the application loads:

- Fetch student data from the API.
- Store the data inside React state.
- Use `useEffect()`.

Example:

```jsx
useEffect(() => {
  fetch("https://jsonplaceholder.typicode.com/users")
    .then((response) => response.json())
    .then((data) => setStudents(data));
}, []);
```

---

# Part 2 — Loading State

While the data is loading, display:

```
Loading Students...
```

Once the data is loaded, display the student list.

---

# Part 3 — Error Handling

If the API request fails, display:

```
Something went wrong.
```

---

# Part 4 — Display Students

Display every student using:

```jsx
map()
```

Each student card should show:

- Name
- Email
- Phone

Example:

```
Leanne Graham

[email@example.com]

1-770-736-8031
```

---

# Part 5 — Search Students

Create a search input.

Users should be able to search students by **name**.

Use:

```jsx
filter()
```

Example:

Searching:

```
Lea
```

Should display:

```
Leanne Graham
```

---

# Part 6 — Case-Insensitive Search

Searching:

```
john
```

should still find

```
John
```

Hint:

```jsx
toLowerCase()
```

---

# Part 7 — View Student Details

Each student card should contain a button:

```
View Details
```

Clicking the button should display additional information:

- Username
- Company
- Website
- Address

Clicking it again should hide the information.

Use **Conditional Rendering**.

---

# Part 8 — Filter Students

Allow users to filter students by company.

Example:

```
All Companies
```

↓

```
Romaguera-Crona
```

Only students from the selected company should be displayed.

---

# Part 9 — Conditional Rendering

If there are no students:

```jsx
students.length === 0
```

Display:

```
No Students Found
```

If searching or filtering returns no results, display:

```
No Matching Students
```

---

# Part 10 — Events

Your application must use:

- onClick
- onChange

---

# Part 11 — Multiple State Variables

Your application should include multiple state variables.

Example:

```jsx
const [students, setStudents] = useState([]);
const [search, setSearch] = useState("");
const [loading, setLoading] = useState(true);
const [error, setError] = useState("");
const [selectedCompany, setSelectedCompany] = useState("All");
const [expandedStudent, setExpandedStudent] = useState(null);
const [darkMode, setDarkMode] = useState(false);
const [sortOrder, setSortOrder] = useState("asc");
```

---

# Part 12 — Controlled Input

Use controlled inputs.

Every input must use:

```jsx
value
```

and

```jsx
onChange
```

---

# Part 13 — Props

Create the following component structure.

```
App
│
├── SearchBar
├── FilterBar
└── StudentList
      │
      └── StudentCard
```

Pass data between components using **Props**.

---

# Part 14 — Lifting State Up

The following state should live inside **App.jsx**:

- students
- search
- selectedCompany
- expandedStudent
- darkMode
- sortOrder

Pass data and functions down to child components using props.

---

# Part 15 — Dark Mode

Create a button.

```
Dark Mode
```

Clicking it should toggle the application's theme.

Example:

```jsx
const [darkMode, setDarkMode] = useState(false);
```

---

# Part 16 — Student Count

Display the total number of visible students.

Example:

```
Total Students: 10
```

The count should automatically update after searching or filtering.

---

# Part 17 — Highlight Search Results

When searching:

```
john
```

Highlight matching student cards with a different background color.

---

# Part 18 — Sort Students

Create two buttons.

```
A-Z
```

```
Z-A
```

Sort students alphabetically by **name**.

---

# Part 19 — Refresh Data

Create a button.

```
Refresh
```

Clicking the button should fetch the latest data from the API again.

---

# Part 20 — Reset

Create a button.

```
Reset
```

Clicking the button should reset:

- Search
- Filter
- Sort
- Expanded Details

---

# Suggested Folder Structure

```
src/
│
├── components/
│   ├── SearchBar.jsx
│   ├── FilterBar.jsx
│   ├── StudentList.jsx
│   └── StudentCard.jsx
│
├── App.jsx
├── main.jsx
└── index.css
```

---

# React Concepts Covered

| Topic | Required |
|---------|----------|
| Components | ✅ |
| JSX | ✅ |
| useState | ✅ |
| useEffect | ✅ |
| Fetch API | ✅ |
| Events | ✅ |
| Input Handling | ✅ |
| Controlled Components | ✅ |
| Conditional Rendering | ✅ |
| Arrays | ✅ |
| map() | ✅ |
| filter() | ✅ |
| Props | ✅ |
| Lifting State Up | ✅ |
| Multiple State Variables | ✅ |
| Search | ✅ |
| Filtering | ✅ |
| Sorting | ✅ |

---

# Submission

Submit your assignment by providing:

- GitHub Repository Link

---

# Bonus (Optional)

Complete any **two** of the following:

### ⭐ Favorite Students

Allow users to mark students as favorites.

---

### ⭐ Search by Email

Search students using both **name** and **email**.

---

### ⭐ Grid/List View

Add buttons to switch between Grid View and List View.

---

### ⭐ Copy Email

Add a button that copies the student's email to the clipboard.

---

### ⭐ Student Profile Modal

Instead of expanding the card, open a modal showing the student's full information.

---

### ⭐ Responsive Design

Make the application look good on desktop, tablet, and mobile devices.

---

Good luck and happy coding! 🚀
