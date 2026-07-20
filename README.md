# React.js Assignment
## Student Directory Dashboard

**Course:** React.js 
**Submission Format:** GitHub repo link

### Git Clone
```
git clone https://arifulatwork-admin@bitbucket.org/arifulatwork-admin/react-js.git
```

### Free API
```
https://jsonplaceholder.typicode.com/users
```

This API returns 10 users with:
- id
- name
- email
- phone
- website
- company
- address

### Objective
Build a Student Directory where users can:
- Fetch students from an API
- Search students
- Add new students
- Edit students
- Delete students
- Show student details
- Filter students
- Toggle dark mode
- Show loading
- Show errors
- Share data between components

### Instructions
1. Complete every part below in your own project.
2. Follow the folder structure given at the end.
3. Do not hard-code student data — everything must come from state and the API.
4. Comment your code where the logic may not be obvious.

---

## Part 1 - Fetch Data (useEffect + API)

When the page loads:
- fetch users from the API
- save them in state

Example:
```jsx
useEffect(() => {
  fetch("https://jsonplaceholder.typicode.com/users")
    .then(res => res.json())
    .then(data => setStudents(data));
}, []);
```

## Part 2 - Loading Screen

While fetching, show:
```
Loading Students...
```
When finished, display students.

## Part 3 - Error Handling

If the API fails, show:
```
Something went wrong.
```

## Part 4 - Display Students (map)

Display:
```
Ahmed
[email protected]
0123456789

John
[email protected]
...
```

Must use:
```
map()
```

## Part 5 - Search Student

Create:
```jsx
<input />
```

Search by:
- name

Must use:
```
filter()
```

Example:
Typing
```
Lea
```
Shows only
```
Leanne Graham
```

## Part 6 - Case Insensitive Search

Searching
```
leanne
```
should still find
```
Leanne Graham
```

Hint:
```
toLowerCase()
```

## Part 7 - Add Student

Create a form.

Inputs:
```
Name
Email
Phone
```

Button:
```
Add Student
```

After clicking:
The new student appears instantly.

## Part 8 - Delete Student

Every card has:
```
Delete
```

Button:
Remove that student.

Must use:
```
filter()
```

## Part 9 - Edit Student

Every student has:
```
Edit
```

Clicking it:
Shows inputs filled with current values.

Update button:
```
Save
```

Must use:
```
map()
```

## Part 10 - Conditional Rendering

If:
```
students.length === 0
```
Show:
```
No Students Found
```
Otherwise:
Display list.

Also:
If searching returns nothing, show:
```
No Matching Students
```

## Part 11 - Events

Use:
```
onClick
onChange
onSubmit
```

## Part 12 - Multiple State

Use multiple states:
```
students
search
loading
error
newName
newEmail
newPhone
editingStudent
darkMode
```

## Part 13 - Forms

Use controlled inputs:
```
value
onChange
```
No uncontrolled inputs.

## Part 14 - Props

Create:
```
App
```
↓
```
StudentList
```
↓
```
StudentCard
```

Pass data through props.

## Part 15 - Lifting State Up

Delete, Edit, Update must happen in:
```
App.jsx
```

Pass functions like:
```
deleteStudent
updateStudent
addStudent
```
to child components.

## Part 16 - Dark Mode

Button:
```
Dark Mode
```

Clicking:
Changes the entire app theme.

Hint:
```jsx
const [darkMode, setDarkMode] = useState(false);
```

## Part 17 - Student Count

Top of page:
```
Total Students: 12
```

Automatically updates.

## Part 18 - Highlight Search

Searching
```
john
```
Matching card gets a different background color.

## Part 19 - Sort

Buttons:
```
A-Z
Z-A
```
Sort students alphabetically.

## Part 20 - Reset

Button:
```
Reset
```

Clears:
- search
- form
- edit mode

---

## Suggested Folder Structure

```
src/

components/

    StudentList.jsx
    StudentCard.jsx
    StudentForm.jsx
    SearchBar.jsx

App.jsx
```
