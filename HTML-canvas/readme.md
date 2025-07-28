# 🖌️ HTML Canvas Drawing App

A fun and interactive drawing app built with HTML5 Canvas and JavaScript.  
Draw with your mouse and watch the colors shift and line thickness animate dynamically!  
Inspired by [Wes Bos' JavaScript30](https://javascript30.com) and documented with help from [MDN Web Docs](https://developer.mozilla.org/).

---

## 💻 Live Preview

Just open the HTML file in any modern web browser — no build tools required.

---

## 📁 File Structure

```
index.html
```

---

## 🚀 How It Works

Below is the full code with inline comments for educational purposes.

### `index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>HTML canvas</title>
  <style>
    /* Removes default browser margin so the canvas fills the window */
    html, body {
      margin: 0;
    }
  </style>
</head>
<body>
  <!-- The canvas element where drawing happens -->
  <canvas id="draw" width="800" height="800"></canvas>

  <script>
    // Select the canvas and get the 2D rendering context
    const canvas = document.querySelector("#draw");
    const ctx = canvas.getContext("2d");

    // Make the canvas responsive to window size
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    // Set up drawing styles
    ctx.strokeStyle = "#BADA55"; // initial stroke color
    ctx.lineJoin = "round";      // rounded edges between lines
    ctx.lineCap = "round";       // rounded ends of lines
    ctx.lineWidth = 10;          // initial line thickness

    // Flags and values to track drawing state
    let isDrawing = false;
    let lastX = 0;
    let lastY = 0;
    let hue = 0;
    let direction = true;

    // Drawing function that runs on mousemove
    function draw(e) {
      if (!isDrawing) return; // only draw when mouse is down

      // Use HSL to shift hue for rainbow effect
      ctx.strokeStyle = `hsl(${hue}, 100%, 50%)`;

      ctx.beginPath(); // start a new path
      ctx.moveTo(lastX, lastY); // move to the last known position
      ctx.lineTo(e.offsetX, e.offsetY); // draw to the current position
      ctx.stroke(); // render the stroke

      // Update last position
      [lastX, lastY] = [e.offsetX, e.offsetY];

      // Increment hue and wrap around if needed
      hue++;
      if (hue >= 360) hue = 0;

      // Oscillate line width between 1 and 100
      if (ctx.lineWidth >= 100 || ctx.lineWidth <= 1) {
        direction = !direction;
      }
      ctx.lineWidth += direction ? 1 : -1;
    }

    // Event listeners to control drawing
    canvas.addEventListener("mousemove", draw);
    canvas.addEventListener("mousedown", (e) => {
      isDrawing = true;
      [lastX, lastY] = [e.offsetX, e.offsetY];
    });
    canvas.addEventListener("mouseup", () => isDrawing = false);
    canvas.addEventListener("mouseout", () => isDrawing = false);
  </script>
</body>
</html>
```

---

## 🧠 Concepts Used

- Canvas API (`getContext`, `moveTo`, `lineTo`, `stroke`)
- HSL color cycling
- Dynamic line width control
- Mouse event handling
- Destructuring assignment

---

## 🙏 Credit

- [MDN Web Docs – Canvas API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API)
- [HSL Color Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/hsl)
- [Wes Bos – JavaScript30](https://javascript30.com)

---
