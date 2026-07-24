# React.js Assignment
# Flight Search Dashboard with Context API & Custom Hooks

**Course:** React.js

**Submission:** GitHub Repository Link

> **Update note:** The original DataMock reference API is no longer available, and the
> live airport dataset can be slow/unreliable to fetch directly in the browser (large
> payload, inconsistent CORS behavior). This version replaces the dead reference API
> and adds two supporting datasets (airlines and users) hosted as static JSON files,
> while keeping the airport fetch as a real network request so Part 1 (`useEffect` +
> `fetch`) is still meaningfully tested.

---

# Data Sources

You will work with **four** JSON data sources in this project. Three are static files
you fetch from GitHub Gist (fast, reliable, no rate limits). One — airports — is a
live, real-world API fetch, which is what Part 1 is designed to test.

## 1. Airports (live API — fetch this one for real)

```
https://raw.githubusercontent.com/mwgg/Airports/master/airports.json
```

Returns a JSON object of ~29,000 airports keyed by ICAO code:

```json
"KJFK": {
  "icao": "KJFK",
  "iata": "JFK",
  "name": "John F Kennedy International Airport",
  "city": "New York",
  "state": "New York",
  "country": "US",
  "elevation": 13,
  "lat": 40.63980103,
  "lon": -73.77890015,
  "tz": "America/New_York"
}
```

Only entries with a non-empty `iata` field are real commercial airports — filter out
the rest before using them.

**Known caveat:** this file is large (~4MB) and `raw.githubusercontent.com` doesn't
always send CORS headers consistently, so the fetch can occasionally hang or fail in
the browser depending on your network. Handle this the same way you'd handle any real
API failure — with the loading/error states from Parts 2 and 3. If it fails
persistently in your environment, you may cache the filtered result in memory after
the first successful load rather than re-fetching every render (you should already be
doing this correctly if you're using `useEffect` with an empty dependency array).

## 2. Airlines (static reference data)

```
https://gist.githubusercontent.com/AmraManush/78d58d03d964308f077ad06b51c90686/raw/8722b2bf275975b4ea27390a3ab9821183f801a4/airlines.json
```

Replaces the "pick from a small fixed list" instruction from the original spec with a
real, structured pricing model per airline:

```json
{
  "id": "SW",
  "name": "SkyWays",
  "code": "SW",
  "pricePerKm": 0.09,
  "basePrice": 35,
  "classMultipliers": {
    "Economy": 1,
    "Premium Economy": 1.5,
    "Business": 2.8
  }
}
```

Use this to drive your mock price generator (see Part 9): a flight's base price is
roughly `basePrice + pricePerKm * distanceKm`, then multiplied by the
`classMultipliers` value for the chosen cabin class, then adjusted slightly for stop
count.

## 3. Flights (shape reference)

```
https://gist.githubusercontent.com/AmraManush/e7fa752386dd968efbc32d8049b3b2cb/raw/02d42def894c25ef41704565cb39c64852bb21ab/flights.json
```

A realistic example flight-search result (route + ~150 generated flight offers for one
sample route) showing the exact shape your generated mock flights should match —
field names, formatting of duration/time strings, price breakdown, etc. This is a
**reference only**, the same way the old DataMock link was — your app must still
generate its own flights on demand using the real distance between the real airports
the user picked (Part 8 and Part 9), not read canned flights from this file.

## 4. Users (for Context API)

```
https://gist.githubusercontent.com/AmraManush/a88d59b033a1a6b996d2014ba2065889/raw/6a9452cb1034ead946a620ae094cbdac089c0ad9/users.json
```

```json
{
  "users": [
    { "id": 1, "name": "Ariful", "email": "arifulatwork@gmail.com" },
    { "id": 2, "name": "piotr", "email": "pierter231@gmail.com" }
  ]
}
```

Replaces the hardcoded `{ name: "John Doe", email: "john@gmail.com" }` in Part 22 —
fetch this list and use it to populate `UserContext` (e.g. default to the first user,
or add a simple user switcher as a stretch goal).

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
- Do not hard-code airport, airline, flight, or user data — fetch all four sources
  listed above.
- Organize your code properly.
- Add comments where necessary.
- Use Context API where required.
- Create reusable Custom Hooks.

---

# Part 1 — Fetch Airports

When the application starts:

- Fetch airport data from the live API above.
- Convert the object into an array.
- Filter airports that have a non-empty IATA code.
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

```jsx
function getDistanceKm(lat1, lon1, lat2, lon2) {
  const toRad = (deg) => (deg * Math.PI) / 180;
  const R = 6371;
  const dLat = toRad(lat2 - lat1);
  const dLon = toRad(lon2 - lon1);
  const a =
    Math.sin(dLat / 2) ** 2 +
    Math.cos(toRad(lat1)) * Math.cos(toRad(lat2)) * Math.sin(dLon / 2) ** 2;
  const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
  return R * c;
}
```

---

# Part 9 — Generate Mock Flights

Clicking

```
Search Flights
```

should generate **5–8 mock flight offers** for the selected route and date, using the
**Airlines** dataset to drive pricing and the **Flights** dataset as your shape
reference.

Each flight must contain:

- Airline (name + code, picked from `airlines.json`)
- Flight Number (e.g. `SW-858`)
- Aircraft (Boeing 737 / Airbus A320 / Embraer E190 for short-haul; Boeing 787 /
  Airbus A350 for long-haul — pick based on distance)
- Stops (0, 1, or 2)
- Duration — based on distance ÷ average cruise speed, plus layover time if there are
  stops
- Departure Time (random), with Arrival Time calculated from duration
- Class (Economy / Premium Economy / Business / First Class)
- Status (e.g. Scheduled, Boarding, Delayed) and a gate/terminal assignment
- Price — calculate as:

  ```
  base = airline.basePrice + airline.pricePerKm * distanceKm
  classAdjusted = base * airline.classMultipliers[selectedClass]
  final = adjust classAdjusted slightly down for more stops, slightly up for nonstop
  ```

- Distance (the real Haversine distance from Part 8)

Everything above uses **your own real distance** (Part 8) between **your own real,
user-picked airports** (Parts 4–6) — the Flights dataset is only a shape/format
reference, not something your generator copies values from directly.

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

Fetch the users list from:

```
https://gist.githubusercontent.com/AmraManush/a88d59b033a1a6b996d2014ba2065889/raw/6a9452cb1034ead946a620ae094cbdac089c0ad9/users.json
```

and default the logged-in user to the first entry in the list (`id: 1`, Ariful).

Display the logged-in user inside:

- Navbar
- Booking Summary

Do **not** use props.

*(Stretch idea, not required: add a simple dropdown to switch between users from the
fetched list.)*

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

- Fetch airports from the live API
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
- Fetch/cache the airlines dataset for pricing
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

### ⭐ Passenger Count
Allow users to select passengers.

### ⭐ Favorites
Save favorite flights using Context API.

### ⭐ Search History
Store the last five searches using Context API.

### ⭐ Recently Booked Flights
Display the most recently booked flight.

### ⭐ Filter by Stops
Nonstop / 1 Stop / 2 Stops

### ⭐ Price Range
Filter by price.

### ⭐ Responsive Design
Desktop / Tablet / Mobile

### ⭐ User Switcher
Let the logged-in user be changed from the fetched `users.json` list via a dropdown
in the Navbar, updating `UserContext` live.

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

This assignment is designed to help you build a **real-world React application** while
practicing **Props, Lifting State Up, Context API, and Custom Hooks** together in a
single project.
