# 📄 Interactive Flex Panels – Documentation

This project creates an interactive full-screen layout of animated image panels using HTML, CSS, and JavaScript. When clicked, each panel expands smoothly to reveal content and collapses when clicked again.

---

## 🧱 HTML Structure

```html
<div class="panels">
  <div class="panel panel1">
    <p>Hey</p>
    <p>Let's</p>
    <p>Dance</p>
  </div>
  <div class="panel panel2">
    <p>Give</p>
    <p>Take</p>
    <p>Receive</p>
  </div>
  <div class="panel panel3">
    <p>Experience</p>
    <p>it's</p>
    <p>Today</p>
  </div>
  <div class="panel panel4">
    <p>Give</p>
    <p>All</p>
    <p>You can</p>
  </div>
  <div class="panel panel5">
    <p>life</p>
    <p>In</p>
    <p>Motion</p>
  </div>
</div>
```

* `.panels`: Acts as the flex container holding all 5 panels.
* `.panel.panelX`: Each panel contains 3 `<p>` elements that animate. `panelX` (1 to 5) assigns unique background images.

---

## 🎨 CSS Styling

### 🌐 Global Styles

```css
html {
  box-sizing: border-box;
  background: #ffc600;
  font-family: 'helvetica neue';
  font-size: 20px;
  font-weight: 200;
}
*, *:before, *:after {
  box-sizing: inherit;
}
body {
  margin: 0;
}
```

* Ensures consistent box sizing.
* Sets base font, background color, and removes margin.

---

### 📀 Font Styling

```css
.amatic-sc-regular, .amatic-sc-bold {
  font-family: "Amatic SC", sans-serif;
  font-style: normal;
}
.amatic-sc-regular { font-weight: 400; }
.amatic-sc-bold { font-weight: 700; }
```

* Applies the imported Google Font (Amatic SC) with regular and bold weights.

---

### 🔠 Flex Container

```css
.panels {
  display: flex;
  min-height: 100vh;
  overflow: hidden;
}
```

* Makes `.panels` a horizontal flex container.
* Ensures full height and hides overflow during animation.

---

### 👟 Panel Styling

```css
.panel {
  background: #6B0F9C;
  box-shadow: inset 0 0 0 5px rgba(255,255,255,0.1);
  transition:
    font-size 0.7s cubic-bezier(0.61,-0.19, 0.7,-0.11),
    flex 0.7s cubic-bezier(0.61,-0.19, 0.7,-0.11),
    background 0.2s;
  font-size: 20px;
  background-size: cover;
  background-position: center;
  flex: 1;
  color: white;
  width: 100%;
  display: flex;
  justify-content: center;
  text-align: center;
  align-items: center;
  flex-direction: column;
}
```

* Each panel takes equal space (`flex: 1`) initially.
* Background image is set via the `.panelX` classes.
* Smooth transitions on expansion and font-size changes.

---

### 👩‍🎓 Panel Text Effects

```css
.panel p {
  text-transform: uppercase;
  font-family: 'Amatic SC', cursive;
  text-shadow: 0 0 4px rgba(0, 0, 0, 0.72), 0 0 14px rgba(0, 0, 0, 0.45);
  font-size: 2em;
}
.panel p:nth-child(2) {
  font-size: 4em;
}
```

* Adds shadow, uppercase styling, and larger middle text.

---

### 🎭 Panel Backgrounds

```css
.panel1 { background-image: url(...); }
.panel2 { background-image: url(...); }
.panel3 { background-image: url(...); }
.panel4 { background-image: url(...); }
.panel5 { background-image: url(...); }
```

* Each panel gets a unique background image from Unsplash.

---

### 🔄 Panel Children Transitions

```css
.panel > * {
  margin: 0;
  width: 100%;
  transition: transform 0.5s;
  flex: 1 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
}
.panel > *:first-child {
  transform: translateY(-100%);
}
.panel > *:last-child {
  transform: translateY(100%);
}
.panel.open-active > *:first-child,
.panel.open-active > *:last-child {
  transform: translateY(0);
}
```

* Animates text sliding in from top/bottom once the panel is activated.

---

### 🔓 Open and Active Panel Styling

```css
.panel.open {
  flex: 5;
  font-size: 40px;
}
```

* Expands the clicked panel (`flex: 5`) and increases text size.

---

### 📱 Responsive Design

```css
@media only screen and (max-width: 600px) {
  .panel p {
    font-size: 1em;
  }
}
```

* Makes text smaller on small screens.

---

## ⚙️ JavaScript Interactivity

```javascript
const panels = document.querySelectorAll('.panel');

function toggleOpen() {
  this.classList.toggle('open');
}

function toggleActive(e) {
  if (e.propertyName.includes('flex')) {
    this.classList.toggle('open-active');
  }
}

panels.forEach(panel => panel.addEventListener('click', toggleOpen));
panels.forEach(panel => panel.addEventListener('transitionend', toggleActive));
```

* `toggleOpen()`: Toggles `open` class to expand panel on click.
* `toggleActive()`: Waits for `flex` transition to end before revealing text.
* Two event listeners for each panel: `click` and `transitionend`.

---

## ✅ Summary

| Feature       | Description                                   |
| ------------- | --------------------------------------------- |
| Layout        | Responsive, animated Flexbox                  |
| Interactivity | Click-to-expand/collapse via transitions      |
| Animation     | Text slides in with transform on open         |
| Styling       | Custom fonts, shadows, responsive adjustments |
| Media Query   | Font scales for smaller screens               |
| Images        | Backgrounds from Unsplash                     |

---

## 📘 Credits

* **Images**: [Unsplash](https://unsplash.com/)
* **Fonts**: [Google Fonts – Amatic SC](https://fonts.google.com/specimen/Amatic+SC)

---

> Feel free to use and modify this project for learning, portfolio, or creative purposes!
