# React.js Assignment
# Flight Search Dashboard

**Course:** React.js
**Submission:** GitHub Repository Link

---

# API

Use the following free API (no API key required, no signup):

```
https://raw.githubusercontent.com/mwgg/Airports/master/airports.json
```

This returns a JSON object of ~29,000 airports keyed by ICAO code. Each entry looks like:

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

Only entries with an `iata` code are real commercial airports — filter out the ones without one before using them.

There is no free API that returns live flight prices for a route you choose yourself, so this project generates **mock flight offers on top of real airport data**: the distance between two airports is calculated for real using their latitude/longitude, and that real distance is used to scale believable fake prices, durations, and stop counts.

For reference on what realistic mock flight data looks like (price breakdowns, aircraft types, gates, status), see [DataMock's Flight Information API](https://datamock.dev/api-explorer/flight) — free, no key, at `https://api.datamock.dev/v1/flight`. It's used here as a *shape reference* only, since it generates its own random routes from a fixed list of ~30 airports and can't search the airports a user picks.

Example of the fetch:

```jsx
useEffect(() => {
  fetch("https://raw.githubusercontent.com/mwgg/Airports/master/airports.json")
    .then((response) => response.json())
    .then((data) => {
      // data is an object keyed by ICAO code — turn it into an array
      // and keep only airports that have a real IATA code
      const list = Object.values(data).filter((airport) => airport.iata);
      setAirports(list);
      setLoading(false);
    })
    .catch(() => {
      setError("Something went wrong.");
      setLoading(false);
    });
}, []);
```

---

# Project Objective

Build a **Flight Search Dashboard** (Google Flights style) using React.js.

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
- sort()
- Conditional Rendering
- Props
- Lifting State Up
- Multiple State Variables

---

# Rules

- Do **not** hard-code airport data.
- Fetch all airports from the API.
- Use React functional components.
- Use Hooks only.
- Keep your code clean and organized.
- Comment your code where necessary.
- Follow the folder structure below.

---

# Part 1 — Fetch Airports

When the application loads:

- Fetch the airport data from the API.
- Filter it down to airports that have an `iata` code.
- Store the result inside React state.
- Use `useEffect()`.

---

# Part 2 — Loading State

While the data is loading, display:

```
Loading Airports...
```

---

# Part 3 — Error Handling

If the API request fails, display:

```
Something went wrong.
```

---

# Part 4 — Origin & Destination Search

Create two inputs: **From** and **To**.

As the user types (2+ characters), show a list of matching airports using `filter()`, matched against city, airport name, or IATA code.

---

# Part 5 — Case-Insensitive Search

Searching `london` should still find `London Heathrow Airport`. Hint: `toLowerCase()`.

---

# Part 6 — Select an Airport

Clicking a suggestion should select that airport, fill the input with `City (IATA)`, and close the suggestion list. Use **Conditional Rendering** to only show suggestions while typing.

---

# Part 7 — Pick a Date

Add a `type="date"` input for the departure date. It must be a controlled input.

---

# Part 8 — Calculate Real Distance

Once both airports are selected, calculate the real distance between them using their latitude/longitude with the **Haversine formula**.

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

Clicking **Search Flights** should generate 5-8 flight offers using `map()`/a loop, scaled off the real distance.

There's no free API that returns live prices for a route you choose yourself, but [DataMock's Flight Information endpoint](https://datamock.dev/api-explorer/flight) (`https://api.datamock.dev/v1/flight`) shows what realistic mock flight data looks like — use its response shape as a reference for what your generator should produce:

- Flight number (e.g. `LA-9008`)
- Airline (name + code, pick from a small fixed list)
- Aircraft model (e.g. Boeing 737, Airbus A320 for short-haul; Boeing 787, Airbus A350 for long-haul — pick based on distance)
- Stop count (0, 1, or 2)
- Duration based on distance ÷ average cruise speed, plus layover time if there are stops
- Price broken into `base`, `taxes`, and `total`, scaled by distance and class — more stops cost slightly less, nonstop costs slightly more
- Class (Economy / Premium Economy / Business / First Class)
- Random departure time, with arrival time calculated from duration
- Status (e.g. Scheduled, Boarding, Delayed) and a gate/terminal assignment

Everything above still uses **your own real distance** (Part 8) between **your own real, user-picked airports** (Parts 4-6) — DataMock is only a reference for shaping realistic fake data, not something your app calls directly, since it can't search the airports you pick.

---

# Part 10 — Conditional Rendering

Before a search has been run, show nothing (or a prompt to search).

If a search returns no flights, display:

```
No flights found.
```

---

# Part 11 — Events

Your application must use `onClick`, `onChange`, and `onSubmit`.

---

# Part 12 — Multiple State Variables

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

# Part 13 — Controlled Input

Every input (From, To, Date) must use `value` and `onChange`.

---

# Part 14 — Props

Component structure:

```
App
│
├── SearchForm
│     │
│     └── AirportInput (used twice: From and To)
└── ResultsList
      │
      └── FlightCard
```

Pass data and functions between components using **Props**.

---

# Part 15 — Lifting State Up

The following state should live inside **App.jsx** and be passed down as props:

- airports
- origin
- destination
- date
- flights
- sortBy

---

# Part 16 — Swap Button

Add a **Swap** button that swaps the From and To airports.

---

# Part 17 — Result Count

Display the number of flights found, e.g. `7 flights found`. This must update automatically with each new search.

---

# Part 18 — Sort Results

Create two buttons: **Sort by Price** and **Sort by Duration**. Use `sort()` on the flights array.

---

# Part 19 — Stops & Distance Display

Each flight card must show stop count (`Nonstop`, `1 stop`, `2 stops`) and the real distance in km, alongside price and duration. Also display the aircraft model, class, and status (e.g. `Boeing 737 · Economy · Scheduled`) so the card matches the level of detail a real flight search result would show.

---

# Part 20 — Search Again

Running a new search (different airports or date) should replace the old results with a freshly generated set of flights.

---

# Suggested Folder Structure

```
src/
│
├── components/
│   ├── AirportInput.jsx
│   ├── SearchForm.jsx
│   ├── ResultsList.jsx
│   └── FlightCard.jsx
│
├── flightUtils.js
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
| sort() | ✅ |
| Props | ✅ |
| Lifting State Up | ✅ |
| Multiple State Variables | ✅ |
| Search | ✅ |
| Real-world math (Haversine distance) | ✅ |
| Sorting | ✅ |

---

# Submission

Submit your assignment by providing:

- GitHub Repository Link

---

# Bonus (Optional)

Complete any **two** of the following:

### ⭐ Round Trip
Add a return-date field and generate a return flight too.

### ⭐ Passenger Count
Add a passengers selector that scales the total price.

### ⭐ Filter by Stops
Add a dropdown to filter results to Nonstop / 1 stop / 2 stops only.

### ⭐ Price Range Slider
Let users filter flights within a min/max price range.

### ⭐ Recent Searches
Keep a list of the last 5 searches and let users click to re-run one.

### ⭐ Responsive Design
Make the application look good on desktop, tablet, and mobile devices.

---

Good luck and happy coding! ✈️
