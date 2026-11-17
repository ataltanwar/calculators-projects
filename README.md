# Calculator Projects

A collection of simple browser-based calculators built with HTML, CSS, and
vanilla JavaScript.

## Included calculators

- **[BMI Calculator](./BMI%20Calculator/)** - Calculates body mass index from
  height and weight and displays a BMI category.
- **[Calorie Calculator](./Calorie%20Calculator/)** - Estimates BMR and daily
  calorie needs using age, height, weight, gender, and activity level.
- **[SI Calculator](./SI%20Calculator/)** - Calculates simple interest and the
  resulting total amount from principal, interest rate, and time.

## Running locally

No build tools or dependencies are required.

1. Clone or download this repository.
2. Open any calculator's `index.html` file in a web browser.
3. Enter the requested values and select **Calculate**.

For the best results when using local development tools, serve the repository
with a simple static web server.

## Technologies

- HTML5
- CSS3
- Vanilla JavaScript

## Project methodology

Each calculator follows the same small, focused workflow:

1. **Collect input** with semantic HTML form controls such as number inputs,
   radio buttons, and a select menu.
2. **Listen for an action** with a JavaScript `click` event on the Calculate
   button.
3. **Read and convert values** from the DOM. JavaScript input values arrive as
   strings, so numeric calculations explicitly use arithmetic or `Number()`.
4. **Apply the calculator formula** and any relevant conditional rules.
5. **Update the page** by writing the result into dedicated output elements.

This approach keeps the markup, presentation, and behavior understandable for
beginners while avoiding frameworks and build dependencies.

## How the calculators work

### BMI Calculator

The BMI page accepts height in centimeters and weight in kilograms. It converts
the height to the metric form needed by the BMI formula and then assigns a
category based on the calculated value:

```js
let result = (weight.value / (height.value * height.value)) * 10000;

if (result < 18.5) {
    category.textContent = "Category- Underweight";
} else if (result <= 24.9) {
    category.textContent = "Category- Normal";
} else if (result <= 29.9) {
    category.textContent = "Category- Overweight";
} else if (result >= 30 && result < 60) {
    category.textContent = "Category- Obese";
}
```

The script also checks that height and weight have been provided before showing
the result.

### Calorie Calculator

The calorie calculator uses the Mifflin-St Jeor equation to calculate BMR. It
selects the male or female equation from the radio buttons, then multiplies BMR
by an activity factor:

```js
let bmr = (10 * weight.value) +
          (6.25 * height.value) -
          (5 * age.value) + 5;

if (activity.value === "moderate") {
    score = bmr * 1.55;
}

resultBmr.textContent = "BMR (Basal Metabolic Rate)- " + bmr + " kcal/day";
resultCal.textContent = "Daily Calorie (TDEE)- " +
                        score.toFixed(0) + " kcal/day";
```

The activity menu provides five multipliers, from sedentary to super active.
The result panel is initially hidden in CSS and is displayed after calculation.

### SI Calculator

The SI calculator uses the simple-interest formula:

```text
Simple Interest = (Principal × Rate × Time) / 100
Total Amount = Principal + Simple Interest
```

The page reads the three number inputs, calculates both values, and formats the
results with the Indian English locale:

```js
let interest = (amount.value * rate.value * time.value) / 100;
let totalAmount = Number(amount.value) + Number(interest);

siOutput.textContent = "Total Interest- " +
                       interest.toLocaleString("en-IN");
taOutput.textContent = "Total Amount- " +
                       totalAmount.toLocaleString("en-IN");
```

## HTML and JavaScript structure

Each project is self-contained in its own folder. The `index.html` file
contains the page structure, links to the calculator-specific stylesheet, and
contains the calculator script. JavaScript uses `document.getElementById()`
to connect input and output elements:

```js
let amount = document.getElementById("amount");
let button = document.getElementById("calc-btn");
let siOutput = document.getElementById("si-output");

button.addEventListener("click", function () {
    // Read inputs, calculate, and update the output elements.
});
```

Outputs use `textContent`, which updates visible text without inserting HTML
markup. Number inputs also define minimum values and helpful placeholders in
the HTML to guide users.

## Styling approach

The calculators use separate CSS files so each interface can have its own
layout and visual treatment:

- **BMI Calculator:** a lightweight centered layout with a blue background,
  rounded inputs, and a blue action button.
- **Calorie Calculator:** a flexbox-based form with grouped rows, radio
  controls, an activity selector, and a bordered result panel.
- **SI Calculator:** a centered card layout with rounded corners, green
  action controls, focus styling, and a percentage sign positioned beside the
  rate input.

The shared visual choices include the Inter font, rounded form controls,
high-contrast buttons, and hidden browser number-input spinner controls. CSS
handles layout and visual feedback while JavaScript is responsible only for
calculation behavior and result updates.