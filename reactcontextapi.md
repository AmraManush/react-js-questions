````md
# React.js Assignment
# Flight Search Dashboard with Context API & Custom Hooks

**Course:** React.js

**Submission:** GitHub Repository Link

---

# API

Use the following free API (no API key required):

```
https://raw.githubusercontent.com/mwgg/Airports/master/airports.json
```

This returns a JSON object of airports keyed by ICAO code.

Example:

```json
"KJFK": {
  "icao": "KJFK",
  "iata": "JFK",
  "name": "John F Kennedy International Airport",
  "city": "New York",
  "country": "US",
  "lat": 40.63980103,
  "lon": -73.77890015
}
```

Only airports with an **IATA code** should be used.

---

# Project Objective

Build a **Flight Search Dashboard** similar to Google Flights.

This project demonstrates your understanding of:

- Components
- JSX
- useState
- useEffect
- Fetch API
- Events
- Forms
- Controlled Inputs
- Arrays
- map()
- filter()
- sort()
- Props
- Lifting State Up
- Context API
- Custom Hooks

---

# Rules

- Use Functional Components only.
- Use React Hooks only.
- Do not hard-code airport data.
- Fetch airport data from the API.
- Organize your code properly.
- Add comments where necessary.
- Use Context API where required.
- Create reusable Custom Hooks.

---

# Part 1 — Fetch Airports

When the application starts:

- Fetch airport data.
- Convert the object into an array.
- Filter airports that have an IATA code.
- Store the result in state.

Use:

```jsx
useEffect()
```

---

# Part 2 — Loading State

Display

```
Loading Airports...
```

while fetching data.

---

# Part 3 — Error Handling

Display

```
Something went wrong.
```

if the request fails.

---

# Part 4 — Airport Search

Create two search inputs.

- From
- To

As the user types (minimum 2 characters):

Search using:

- Airport Name
- City
- IATA Code

Use:

```jsx
filter()
```

---

# Part 5 — Case-Insensitive Search

Searching

```
london
```

should also return

```
London Heathrow Airport
```

Hint:

```jsx
toLowerCase()
```

---

# Part 6 — Airport Selection

When a suggestion is clicked:

- Fill the input
- Save the selected airport
- Close suggestions

---

# Part 7 — Departure Date

Create a controlled input:

```html
<input type="date">
```

---

# Part 8 — Calculate Distance

Calculate the real distance between airports using the Haversine Formula.

---

# Part 9 — Generate Mock Flights

Clicking

```
Search Flights
```

should generate **5–8 mock flight offers**.

Each flight must contain:

- Airline
- Flight Number
- Aircraft
- Stops
- Duration
- Departure Time
- Arrival Time
- Class
- Status
- Price
- Distance

---

# Part 10 — Conditional Rendering

Before searching

```
Search for flights
```

If no flights

```
No flights found.
```

---

# Part 11 — Events

Your application must use

- onClick
- onChange
- onSubmit

---

# Part 12 — Multiple State Variables

Example

```jsx
const [airports, setAirports] = useState([]);
const [loading, setLoading] = useState(true);
const [error, setError] = useState("");

const [origin, setOrigin] = useState(null);
const [destination, setDestination] = useState(null);

const [date, setDate] = useState("");

const [flights, setFlights] = useState([]);

const [sortBy, setSortBy] = useState("price");

const [searched, setSearched] = useState(false);
```

---

# Part 13 — Controlled Components

Every input must use

```jsx
value
```

and

```jsx
onChange
```

---

# Part 14 — Component Structure

```
App
│
├── Navbar
│
├── SearchForm
│     │
│     └── AirportInput
│
├── ResultsList
│     │
│     └── FlightCard
│
└── BookingSummary
```

---

# Part 15 — Lifting State Up

Store these inside App.jsx

- airports
- origin
- destination
- flights
- date
- sortBy

Pass them through Props where necessary.

---

# Part 16 — Swap Airports

Create a

```
Swap
```

button.

Swap:

```
From

↓

To
```

---

# Part 17 — Result Count

Display

```
7 Flights Found
```

---

# Part 18 — Sort Flights

Allow users to sort by

- Price
- Duration

Use

```jsx
sort()
```

---

# Part 19 — Flight Details

Each card should display

- Airline
- Flight Number
- Aircraft
- Stops
- Distance
- Duration
- Price
- Class
- Status

---

# Part 20 — Search Again

Every new search should replace previous results.

---

# Part 21 — Context API (Theme)

Create

```
ThemeContext
```

Store

```jsx
theme
```

Default:

```
Light
```

Create a button

```
Toggle Theme
```

The theme should update:

- Navbar
- Search Form
- Results
- Booking Summary

without using props.

---

# Part 22 — Context API (User)

Create

```
UserContext
```

Store

```jsx
{
    name:"John Doe",
    email:"john@gmail.com"
}
```

Display the logged-in user inside:

- Navbar
- Booking Summary

Do **not** use props.

---

# Part 23 — Context API (Booking)

Create

```
BookingContext
```

Store

```jsx
selectedFlight
```

Initially

```jsx
null
```

Each Flight Card must contain

```
Book Flight
```

Clicking the button updates Booking Context.

Booking Summary updates automatically.

---

# Part 24 — Custom Hook (useAirports)

Move all airport fetching logic into

```
useAirports.js
```

The hook should:

- Fetch airports
- Handle loading
- Handle errors
- Return airport data

Example

```jsx
const {
    airports,
    loading,
    error
} = useAirports();
```

---

# Part 25 — Custom Hook (useFlightSearch)

Create

```
useFlightSearch.js
```

The hook should contain all search logic.

Responsibilities:

- Search airports
- Generate flights
- Calculate distance
- Sort flights

Example

```jsx
const {
    flights,
    searchFlights,
    sortFlights
} = useFlightSearch();
```

---

# Part 26 — Custom Hook (useToggle)

Create

```
useToggle.js
```

Use it for

- Theme Button
- Show/Hide Booking Summary
- Show/Hide Favorites

Example

```jsx
const {
    value,
    toggle
} = useToggle();
```

---

# Part 27 — Reuse Custom Hooks

Your project **must** use your custom hooks in multiple components.

Example

```
Navbar

↓

useToggle()

-------------------

SearchForm

↓

useAirports()

-------------------

ResultsList

↓

useFlightSearch()
```

---

# Suggested Folder Structure

```
src/
│
├── components/
│   ├── Navbar.jsx
│   ├── AirportInput.jsx
│   ├── SearchForm.jsx
│   ├── ResultsList.jsx
│   ├── FlightCard.jsx
│   └── BookingSummary.jsx
│
├── context/
│   ├── ThemeContext.jsx
│   ├── UserContext.jsx
│   └── BookingContext.jsx
│
├── hooks/
│   ├── useAirports.js
│   ├── useFlightSearch.js
│   └── useToggle.js
│
├── utils/
│   └── flightUtils.js
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
| Controlled Components | ✅ |
| Conditional Rendering | ✅ |
| map() | ✅ |
| filter() | ✅ |
| sort() | ✅ |
| Props | ✅ |
| Lifting State Up | ✅ |
| Context API | ✅ |
| createContext() | ✅ |
| Provider | ✅ |
| useContext() | ✅ |
| Custom Hooks | ✅ |
| Reusable Logic | ✅ |

---

# Submission

Submit:

- GitHub Repository Link

---

# Bonus (Complete Any Two)

### ⭐ Round Trip

Generate return flights.

---

### ⭐ Passenger Count

Allow users to select passengers.

---

### ⭐ Favorites

Save favorite flights using Context API.

---

### ⭐ Search History

Store the last five searches using Context API.

---

### ⭐ Recently Booked Flights

Display the most recently booked flight.

---

### ⭐ Filter by Stops

Nonstop

1 Stop

2 Stops

---

### ⭐ Price Range

Filter by price.

---

### ⭐ Responsive Design

Desktop

Tablet

Mobile

---

# Grading Criteria

| Criteria | Marks |
|-----------|-------|
| React Fundamentals | 20 |
| Flight Search Features | 20 |
| Props & Components | 10 |
| Context API | 20 |
| Custom Hooks | 15 |
| UI & Responsiveness | 10 |
| Code Quality & Comments | 5 |
| **Total** | **100 Marks** |

---

# Good Luck! ✈️

This assignment is designed to help you build a **real-world React application** while practicing **Props, Lifting State Up, Context API, and Custom Hooks** together in a single project.
````
