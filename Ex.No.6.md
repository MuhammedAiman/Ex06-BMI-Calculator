# Ex06 BMI Calculator
## AIM
To create a BMI calculator using React Router 

## ALGORITHM
### STEP 1 State Initialization
Manage the current page (Home or Calculator) using React Router.

### STEP 2 User Input
Accept weight and height inputs from the user.

### STEP 3 BMI Calculation
Calculate the BMI based on user input.

### STEP 4 Categorization
Classify the BMI result into categories (Underweight, Normal weight, Overweight, Obesity).

### STEP 5 Navigation
Navigate between pages using React Router.

## PROGRAM

### App.jsx
```
import React, { useState } from "react";
import "./App.css";

function App() {
  const [weight, setWeight] = useState("");
  const [height, setHeight] = useState("");
  const [bmi, setBmi] = useState(null);
  const [category, setCategory] = useState("");

  const calculateBMI = () => {
    if (weight && height) {
      const heightInMeters = height / 100;
      const bmiValue = (weight / (heightInMeters * heightInMeters)).toFixed(2);
      setBmi(bmiValue);

      if (bmiValue < 18.5) setCategory("Underweight");
      else if (bmiValue < 25) setCategory("Normal weight");
      else if (bmiValue < 30) setCategory("Overweight");
      else setCategory("Obesity");
    }
  };

  const reset = () => {
    setWeight("");
    setHeight("");
    setBmi(null);
    setCategory("");
  };

  return (
    <div className="container">
      <h1 className="title">BMI Calculator</h1>
      <div className="card glass-card">
        <div className="input-group">
          <label>Weight (kg)</label>
          <input
            type="number"
            value={weight}
            onChange={(e) => setWeight(e.target.value)}
            placeholder="Enter weight"
          />
        </div>
        <div className="input-group">
          <label>Height (cm)</label>
          <input
            type="number"
            value={height}
            onChange={(e) => setHeight(e.target.value)}
            placeholder="Enter height"
          />
        </div>
        <div className="buttons">
          <button className="btn calculate" onClick={calculateBMI}>
            Calculate
          </button>
          <button className="btn reset" onClick={reset}>
            Reset
          </button>
        </div>

        {bmi && (
          <div className="result fade-in">
            <h2>Your BMI: {bmi}</h2>
            <p className={`category ${category.toLowerCase().replace(" ", "-")}`}>
              {category}
            </p>
          </div>
        )}
      </div>
      <footer><h3>Designed by Austin</h3></footer>
    </div>
  );
}

export default App;
```

### App.css
```
/* ===== Base Style ===== */
body {
  margin: 0;
  font-family: "Poppins", sans-serif;
  background: linear-gradient(75deg, #ffffff, #5aedf4);
  color: #ffffff;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
}

/* ===== Container ===== */
.container {
  text-align: center;
  width: 100%;
  max-width: 420px;
  padding: 20px;
}

/* ===== Title ===== */
.title {
  font-size: 2.2em;
  margin-bottom: 25px;
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
}

/* ===== Glass Card ===== */
.glass-card {
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-radius: 20px;
  padding: 35px 25px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.25);
  border: 1px solid rgba(255, 255, 255, 0.2);
  animation: slideUp 0.6s ease;
}

/* ===== Input Groups ===== */
.input-group {
  margin-bottom: 20px;
  text-align: left;
}

.input-group label {
  display: block;
  margin-bottom: 8px;
  font-weight: 500;
  color: #6c7074;
}

.input-group input {
  width: 100%;
  padding: 10px;
  border: none;
  border-radius: 10px;
  font-size: 1em;
  background: rgba(255, 255, 255, 0.8);
  outline: none;
  transition: all 0.3s;
}

.input-group input:focus {
  background: #fff;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.4);
}

/* ===== Buttons ===== */
.buttons {
  display: flex;
  justify-content: space-between;
  gap: 10px;
  margin-top: 10px;
}

.btn {
  flex: 1;
  padding: 10px;
  border: none;
  border-radius: 10px;
  font-size: 1em;
  font-weight: 600;
  cursor: pointer;
  transition: 0.3s;
}

.calculate {
  background: #00c86e;
  color: white;
  box-shadow: 0 4px 10px rgba(0, 200, 151, 0.3);
}

.calculate:hover {
  background: #17a125;
}

.reset {
  background: #ff4d6d;
  color: white;
  box-shadow: 0 4px 10px rgba(255, 77, 109, 0.3);
}

.reset:hover {
  background: #bc1131;
}

/* ===== Result Section ===== */
.result {
  margin-top: 25px;
  background: rgba(0, 0, 0, 0.1);
  border-radius: 15px;
  padding: 15px;
  animation: fadeIn 0.6s ease;
}

.result h2 {
  color: #fff;
  font-size: 1.5em;
}

.category {
  display: inline-block;
  margin-top: 8px;
  padding: 6px 14px;
  border-radius: 20px;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* Category colors */
.category.normal-weight {
  background: #00ffae;
  color: #003a2b;
}

.category.underweight {
  background: #ffe066;
  color: #805b00;
}

.category.overweight {
  background: #ffa07a;
  color: #5b1d00;
}

.category.obesity {
  background: #ff5f5f;
  color: #360000;
}

/* ===== Footer ===== */
footer {
  border: #000000;
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
  margin-top: 30px;
  font-size: 0.9em;
  opacity: 1.0;
}

/* ===== Animations ===== */
@keyframes slideUp {
  from {
    transform: translateY(40px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
```


## OUTPUT

<img width="1919" height="1092" alt="Screenshot 2025-11-05 155942" src="https://github.com/user-attachments/assets/f146917a-2a69-40f9-bae2-c05066b48262" />

<img width="1913" height="987" alt="Screenshot 2025-11-05 160239" src="https://github.com/user-attachments/assets/035f709d-c15c-4a91-9c59-848d6fea82fe" />

<img width="1919" height="866" alt="Screenshot 2025-11-05 160318" src="https://github.com/user-attachments/assets/4b291270-d51e-4978-8fe2-709ab68c69e9" />

## RESULT
The program for creating BMI Calculator using React Router is executed successfully.
