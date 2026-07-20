# React.js Assignment
## Student Directory Dashboard

**Course:** React.js Fundamentals
**Duration:** [Fill in — suggested 2 weeks]
**Submission Format:** GitHub repo link OR zipped project folder

---

### Instructions to Students
1. Build a single React application called **Student Directory Dashboard** that fulfills every requirement below.
2. Use the free API: `https://jsonplaceholder.typicode.com/users`
3. Organize your code using the folder structure provided at the end of this paper.
4. Attempt every question — partial or incomplete attempts are still worth submitting.
5. Comment your code where the logic may not be obvious.
6. No copy-pasted solutions from AI tools without understanding — you may be asked to explain any part of your code during evaluation.

---

## Section A: Data Fetching & App States

**Q1.** Using `useEffect` and the Fetch API, load all students from `https://jsonplaceholder.typicode.com/users` when the app first loads, and store the result in state.

**Q2.** While the data is loading, display the message:
```
Loading Students...
```
Once loading finishes, display the student list instead.

**Q3.** Simulate or handle an API failure (e.g., using a try/catch or `.catch()`), and display:
```
Something went wrong.
```
Explain in a code comment what would cause this branch to run.

---

## Section B: Displaying Data

**Q4.** Using `.map()`, render every student as a card showing:
- Name
- Email
- Phone

Do **not** hard-code student data — it must come from state.

---

## Section C: Search & Filter

**Q5.** Add a search `<input>` above the student list. Use a controlled input (`value` + `onChange`).

**Q6.** Using `.filter()`, show only students whose name matches the search text. Typing `Lea` should show only *Leanne Graham*.

**Q7.** Make the search case-insensitive using `.toLowerCase()`. Typing `leanne` (all lowercase) must still match *Leanne Graham*.

---

## Section D: Add, Edit, Delete (CRUD)

**Q8.** Build a form with three controlled inputs — Name, Email, Phone — and an **Add Student** button. On submit, the new student should appear instantly in the list without a page reload.

**Q9.** Add a **Delete** button on every student card. Clicking it should remove that student using `.filter()`. It must not affect any other student.

**Q10.** Add an **Edit** button on every student card. Clicking it should:
- Pre-fill a form with that student's current values
- Show a **Save** button
- On save, update that specific student using `.map()` (not delete-and-re-add)

---

## Section E: Conditional Rendering

**Q11.** If `students.length === 0`, display:
```
No Students Found
```
Otherwise, render the list normally.

**Q12.** If a search produces zero matches (but students exist overall), display a **different** message:
```
No Matching Students
```
Explain briefly (in a comment) why this needs a separate condition from Q11.

---

## Section F: Component Architecture & Props

**Q13.** Split your app into at least these components:
```
App.jsx
 └── StudentList.jsx
      └── StudentCard.jsx
StudentForm.jsx
SearchBar.jsx
```
Pass student data down via **props** — do not fetch or store the student list inside `StudentCard`.

**Q14.** Apply **lifting state up**: `deleteStudent`, `editStudent`/`updateStudent`, and `addStudent` functions must be defined in `App.jsx` and passed down as props to the components that trigger them (e.g., the delete button lives in `StudentCard`, but the actual deletion logic lives in `App.jsx`).

---

## Section G: Extra Features

**Q15.** Add a **Dark Mode** toggle button that switches the whole app's theme using a `darkMode` state variable.

**Q16.** Display a live student counter at the top of the page, e.g. `Total Students: 8`, that updates automatically as students are added/deleted.

**Q17.** When searching, give the matching student card(s) a different background color to visually highlight the match.

**Q18.** Add **A–Z** and **Z–A** buttons that sort the student list alphabetically by name.

**Q19.** Add a **Reset** button that clears the search box, clears the add-student form, and exits edit mode — all in one click.

---

## Bonus Challenge (optional)

Choose **one**:
- (a) Add form validation (e.g., valid email format, no empty name field) with inline error messages.
- (b) Persist students to `localStorage` so the list survives a page refresh.
- (c) Add a "View Details" modal/panel showing the student's company and address (both available in the API response).

---

## Required Folder Structure

```
src/
  components/
    StudentList.jsx
    StudentCard.jsx
    StudentForm.jsx
    SearchBar.jsx
  App.jsx
```

## Submission Checklist
- [ ] App runs with `npm start` / `npm run dev` without errors
- [ ] All state variables use `useState` (students, search, loading, error, newName, newEmail, newPhone, editingStudent, darkMode)
- [ ] All inputs are controlled (no uncontrolled inputs)
- [ ] Used `onClick`, `onChange`, and `onSubmit` at least once each
- [ ] Code is committed with meaningful commit messages (if using Git)
- [ ] Short README explaining how to run the project
