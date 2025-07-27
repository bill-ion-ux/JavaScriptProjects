
# 🌆 City & State Search (Type Ahead)

This project is a **real-time search interface** built with vanilla JavaScript. Users can search for U.S. cities and states. Matches are highlighted as they type, and population numbers are formatted with commas.

## 📁 Project Files

- `index.html` — Contains the form, input field, and result list.
- `style.css` — External CSS file (assumed to exist, not provided).
- Uses the Fetch API to load city/state data from a remote endpoint.

---

## 🚀 Features

- Fetch data from a JSON endpoint
- Filter and highlight cities/states matching the input
- Format population with commas
- Responsive, keyboard-driven user interaction

---

## 📦 Dataset Source

[US Cities Dataset (GitHub Gist)](https://gist.githubusercontent.com/Miserlou/c5cd8364bf9b2420bb29/raw/2bf258763cdddd704f8ffd3ea9a3e81d25e2c6f6/cities.json)

Each entry contains:

```json
{
  "city": "Los Angeles",
  "state": "California",
  "population": "3971883"
}
```

---

## 💻 Code with Inline Comments

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>City & State Search</title>
  <link rel="stylesheet" href="style.css"> <!-- External styling -->
</head>
<body>

  <!-- Search form -->
  <form class="search-form">
    <input type="text" class="search" placeholder="City or State">
    <ul class="suggestions">
      <li>Filter for a city</li>
      <li>or a state</li>
    </ul>
  </form>

  <script>
    // JSON data endpoint
    const endpoint = 'https://gist.githubusercontent.com/Miserlou/c5cd8364bf9b2420bb29/raw/2bf258763cdddd704f8ffd3ea9a3e81d25e2c6f6/cities.json';

    const cities = [];

    // Fetch and parse JSON, spread into cities array
    fetch(endpoint)
      .then(blob => blob.json())
      .then(data => cities.push(...data));

    // Find matches in city/state names
    function findMatches(wordToMatch, cities) {
      return cities.filter(place => {
        const regex = new RegExp(wordToMatch, 'gi'); // case-insensitive match
        return place.city.match(regex) || place.state.match(regex);
      });
    }

    // Add commas to large numbers
    function numberWithCommas(x) {
      return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
    }

    // Display matches in list
    function displayMatches() {
      const matchArray = findMatches(this.value, cities);
      const html = matchArray.map(place => {
        const regex = new RegExp(this.value, 'gi');
        const cityName = place.city.replace(regex, `<span class="hl">\${this.value}</span>`);
        const stateName = place.state.replace(regex, `<span class="hl">\${this.value}</span>`);
        return \`
          <li>
            <span class="name">\${cityName}, \${stateName}</span>
            <span class="population">\${numberWithCommas(place.population)}</span>
          </li>
        \`;
      }).join('');
      suggestions.innerHTML = html;
    }

    // DOM elements and event listeners
    const searchInput = document.querySelector('.search');
    const suggestions = document.querySelector('.suggestions');

    searchInput.addEventListener('change', displayMatches);
    searchInput.addEventListener('keyup', displayMatches);
  </script>

</body>
</html>
```

---

## 🧠 Concepts Used

- `fetch()` API
- Promises: `.then()`, `.catch()`
- Regular expressions with `RegExp`
- DOM manipulation
- Event listeners (`keyup`, `change`)
- JavaScript array methods: `.filter()`, `.map()`, `.join()`

---



## ✅ TODO / Improvements

- Add loading indicator while fetching
- Debounce input for performance
- Style highlight effect using CSS
- Add country column if expanding beyond U.S.

---


