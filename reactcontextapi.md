# React.js Assignment
# Flight Booking Dashboard using React Context API

**Course:** React.js

**Submission:** GitHub Repository Link

---

# Objective

In this assignment, you will enhance your previous **Flight Search Dashboard** by implementing **React Context API**.

The goal is to replace prop drilling with shared state using:

- createContext()
- Provider
- useContext()

You should continue using the project you built in the previous assignment.

---

# Learning Outcomes

After completing this assignment, you should understand:

- Creating a Context
- Sharing data using Provider
- Accessing shared data with useContext()
- Updating shared state
- Avoiding Prop Drilling
- Managing global application state

---

# Rules

- Continue using your previous Flight Search project.
- Do not remove any existing functionality.
- Replace shared props with Context where appropriate.
- Use React Functional Components.
- Use React Hooks only.
- Write clean and readable code.
- Comment important sections of your code.

---

# Part 1 — Theme Context

Create a Theme Context.

### Default Theme

```
Light
```

Create a button:

```
Toggle Theme
```

The button should switch between:

```
Light

↓

Dark

↓

Light
```

The current theme should be displayed in:

- Navbar
- Search Form
- Flight Results
- Booking Summary

---

# Part 2 — User Context

Create a User Context.

Store the following user information:

```jsx
{
  name: "John Doe",
  email: "john@gmail.com"
}
```

Display the logged-in user inside:

- Navbar
- Search Form
- Booking Summary

Do **not** pass the user through props.

---

# Part 3 — Booking Context

Create a Booking Context.

Store:

```jsx
selectedFlight
```

Default value:

```jsx
null
```

---

# Part 4 — Book Flight

Each Flight Card should contain a button.

```
Book Flight
```

When clicked:

- Save the selected flight into Booking Context.
- The Booking Summary should update automatically.

---

# Part 5 — Booking Summary

Create a component:

```
BookingSummary.jsx
```

Display:

- Airline
- Flight Number
- Departure Airport
- Destination Airport
- Departure Time
- Arrival Time
- Total Price

If no booking exists, display:

```
No Flight Selected
```

---

# Part 6 — Favorite Flights

Create a Favorites Context.

Store:

```jsx
favorites = []
```

Each Flight Card should include:

```
❤️ Add Favorite
```

Clicking the button should add the flight to the Favorites list.

---

# Part 7 — Favorite Flights Component

Create:

```
Favorites.jsx
```

Display every favorite flight.

Example:

```
Favorite Flights

Qatar Airways

QR201

$520
```

---

# Part 8 — Remove Favorite

Each favorite flight should include:

```
Remove
```

Clicking Remove should delete the flight from Favorites.

---

# Part 9 — Navbar

The Navbar should display:

```
Welcome John Doe

Theme : Light

Bookings : 2

Favorites : 5
```

All information must come from Context.

---

# Part 10 — Theme Styling

When the theme changes:

Light Theme

- White background
- Black text

Dark Theme

- Dark background
- White text

The theme should update every component automatically.

---

# Part 11 — Component Structure

```
App
│
├── Navbar
│
├── SearchForm
│
├── FlightResults
│     │
│     └── FlightCard
│
├── BookingSummary
│
├── Favorites
│
└── ThemeButton
```

---

# Part 12 — Folder Structure

```
src/
│
├── components/
│   ├── Navbar.jsx
│   ├── SearchForm.jsx
│   ├── FlightResults.jsx
│   ├── FlightCard.jsx
│   ├── BookingSummary.jsx
│   ├── Favorites.jsx
│   └── ThemeButton.jsx
│
├── context/
│   ├── ThemeContext.jsx
│   ├── UserContext.jsx
│   ├── BookingContext.jsx
│   └── FavoritesContext.jsx
│
├── providers/
│   ├── ThemeProvider.jsx
│   ├── UserProvider.jsx
│   ├── BookingProvider.jsx
│   └── FavoritesProvider.jsx
│
├── App.jsx
├── main.jsx
└── index.css
```

---

# Part 13 — Providers

Wrap the application using Providers.

Example:

```jsx
<UserProvider>
    <ThemeProvider>
        <BookingProvider>
            <FavoritesProvider>

                <App />

            </FavoritesProvider>
        </BookingProvider>
    </ThemeProvider>
</UserProvider>
```

---

# Part 14 — Context API Requirements

Your project must use:

| Feature | Required |
|----------|----------|
| createContext() | ✅ |
| Provider | ✅ |
| useContext() | ✅ |
| useState() | ✅ |
| Events | ✅ |
| Conditional Rendering | ✅ |
| Arrays | ✅ |
| map() | ✅ |
| Props | Minimal |
| Context API | ✅ |

---

# Part 15 — Do Not Use Props

The following data **must come from Context** instead of props.

- Theme
- Logged-in User
- Selected Flight
- Favorite Flights

---

# Bonus (Complete Any Two)

### ⭐ Booking History

Keep a history of booked flights.

---

### ⭐ Search History

Display the last five searches.

---

### ⭐ Recently Viewed Flights

Display the last viewed flights.

---

### ⭐ Clear Favorites

Add a button to remove every favorite.

---

### ⭐ Responsive Design

Make the application responsive for:

- Desktop
- Tablet
- Mobile

---

### ⭐ Dark Mode Styling

Apply different colors and styles for Light and Dark themes.

---

# Expected Output

```
------------------------------------------------

Welcome John Doe

Theme : Dark

Bookings : 2

Favorites : 5

------------------------------------------------

Search Flights

------------------------------------------------

Flight Results

✈️ Qatar Airways

Book Flight

❤️ Favorite

------------------------------------------------

Booking Summary

Qatar Airways

QR201

Dubai → London

$520

------------------------------------------------

Favorite Flights

Emirates

British Airways

Qatar Airways

------------------------------------------------
```

---

# Submission

Submit:

- GitHub Repository Link

---

# Grading Criteria

| Criteria | Marks |
|-----------|-------|
| Context API Implementation | 25 |
| Correct Use of Provider | 10 |
| useContext Usage | 15 |
| Theme Context | 10 |
| Booking Context | 10 |
| Favorites Context | 10 |
| Code Quality | 10 |
| UI & Functionality | 10 |
| Project Structure | 10 |
| **Total** | **100 Marks** |

---

# Good Luck!

This assignment focuses on using **React Context API** to share data across multiple components without prop drilling while extending your existing Flight Search Dashboard.

**Happy Coding! 🚀✈️**
