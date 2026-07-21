# React.js Assignment
# Pokemon Explorer Dashboard

**Course:** React.js
**Submission:** GitHub Repository Link

---
# Clone the Starter Project

```bash
git clone https://arifulatwork-admin@bitbucket.org/arifulatwork-admin/react-js.git
```
# API

Use the following free API (no API key required, no signup):

```
https://pokeapi.co/api/v2/pokemon?limit=151
```

This first call only returns each Pokemon's **name** and a **url** pointing to its full details. To get the full details (image, types, height, weight, abilities) you need to fetch each url too.

Example of the two-step fetch:

```jsx
useEffect(() => {
  fetch("https://pokeapi.co/api/v2/pokemon?limit=151")
    .then((response) => response.json())
    .then((data) => {
      // data.results is an array of { name, url }
      const detailRequests = data.results.map((p) => fetch(p.url).then((res) => res.json()));
      return Promise.all(detailRequests);
    })
    .then((fullPokemonData) => {
      setPokemon(fullPokemonData);
      setLoading(false);
    })
    .catch(() => {
      setError("Something went wrong.");
      setLoading(false);
    });
}, []);
```

Each detailed Pokemon object gives you:

- id
- name
- sprites.front_default (image url)
- types (array of `{ type: { name } }`)
- height
- weight
- abilities (array of `{ ability: { name } }`)

---

# Project Objective

Build a **Pokemon Explorer Dashboard** using React.js.

The application should demonstrate your understanding of:

- useState
- useEffect
- Fetch API (including chained/multiple fetches)
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

- Do **not** hard-code Pokemon data.
- Fetch all Pokemon from the API.
- Use React functional components.
- Use Hooks only.
- Keep your code clean and organized.
- Comment your code where necessary.
- Follow the folder structure below.

---

# Part 1 — Fetch Pokemon

When the application loads:

- Fetch the list of Pokemon, then fetch full details for each one (see example above).
- Store the data inside React state.
- Use `useEffect()`.

---

# Part 2 — Loading State

While the data is loading, display:

```
Loading Pokemon...
```

---

# Part 3 — Error Handling

If the API request fails, display:

```
Something went wrong.
```

---

# Part 4 — Display Pokemon

Display every Pokemon using `map()`. Each card should show:

- Image (`sprites.front_default`)
- Name (capitalize the first letter)
- Types

---

# Part 5 — Search Pokemon

Create a search input. Users should be able to search Pokemon by **name**, using `filter()`.

---

# Part 6 — Case-Insensitive Search

Searching `pika` should still find `Pikachu`. Hint: `toLowerCase()`.

---

# Part 7 — View Pokemon Details

Each card should have a **View Details** button. Clicking it should reveal:

- Height
- Weight
- Abilities (comma-separated list)

Clicking again should hide the details. Use **Conditional Rendering**.

---

# Part 8 — Filter by Type

Add a dropdown to filter Pokemon by type:

```
All Types
```
↓
```
fire / water / grass / electric / ...
```

Only Pokemon that have the selected type should be displayed.

---

# Part 9 — Conditional Rendering

If there are no Pokemon at all, display:

```
No Pokemon Found
```

If searching/filtering returns nothing, display:

```
No Matching Pokemon
```

---

# Part 10 — Events

Your application must use `onClick` and `onChange`.

---

# Part 11 — Multiple State Variables

```jsx
const [pokemon, setPokemon] = useState([]);
const [search, setSearch] = useState("");
const [loading, setLoading] = useState(true);
const [error, setError] = useState("");
const [selectedType, setSelectedType] = useState("All");
const [expandedPokemon, setExpandedPokemon] = useState(null);
const [darkMode, setDarkMode] = useState(false);
const [sortOrder, setSortOrder] = useState("asc");
```

---

# Part 12 — Controlled Input

Every input must use `value` and `onChange`.

---

# Part 13 — Props

Component structure:

```
App
│
├── SearchBar
├── FilterBar
└── PokemonList
      │
      └── PokemonCard
```

Pass data between components using **Props**.

---

# Part 14 — Lifting State Up

The following state should live inside **App.jsx** and be passed down as props:

- pokemon
- search
- selectedType
- expandedPokemon
- darkMode
- sortOrder

---

# Part 15 — Dark Mode

A **Dark Mode** button toggles the app's theme.

---

# Part 16 — Pokemon Count

Display the total number of visible Pokemon, e.g. `Total Pokemon: 24`. This must update automatically after searching/filtering.

---

# Part 17 — Highlight Search Results

When searching, highlight matching cards with a different background color.

---

# Part 18 — Sort Pokemon

Create two buttons: **A-Z** and **Z-A**. Sort Pokemon alphabetically by name.

---

# Part 19 — Refresh Data

A **Refresh** button re-fetches the latest data from the API.

---

# Part 20 — Reset

A **Reset** button clears:

- Search
- Type filter
- Sort order
- Expanded details

---

# Suggested Folder Structure

```
src/
│
├── components/
│   ├── SearchBar.jsx
│   ├── FilterBar.jsx
│   ├── PokemonList.jsx
│   └── PokemonCard.jsx
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
| Fetch API (chained) | ✅ |
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

### ⭐ Favorite Pokemon
Let users star/favorite Pokemon.

### ⭐ Filter by Multiple Types
Allow selecting more than one type at once.

### ⭐ Grid/List View
Add buttons to switch between Grid View and List View.

### ⭐ Stat Bars
Show height/weight as simple CSS bar visualizations.

### ⭐ Pokemon Profile Modal
Instead of expanding the card, open a modal showing full details.

### ⭐ Responsive Design
Make the application look good on desktop, tablet, and mobile devices.

---

Good luck and happy coding! ⚡
