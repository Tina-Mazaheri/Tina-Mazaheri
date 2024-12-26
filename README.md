<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meal Planner App 🍽️</title>
    <link href="https://fonts.googleapis.com/css2?family=Lexend:wght@400;600&display=swap" rel="stylesheet">
    <style>
        /* General Styles */
        body {
            font-family: 'Lexend', sans-serif;
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            color: #333;
            margin: 0;
            padding: 20px;
        }

        .container {
            max-width: 700px;
            margin: auto;
            padding: 20px;
            border-radius: 16px;
            background-color: #ffffff;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
        }

        h1 {
            text-align: center;
            font-size: 2.5rem;
            color: #ff6f61;
        }

        h2 {
            color: #ff6f61;
        }

        .goals, .meal-planner, .summary {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-top: 10px;
            font-weight: bold;
        }

        input[type='number'], select {
            width: calc(100% - 22px);
            padding: 10px;
            margin-top: 5px;
            border-radius: 8px;
            border: 1px solid #ddd;
            box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        button {
            background-color: #ff6f61;
            color: white;
            border: none;
            padding: 12px 18px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
            transition: transform 0.2s ease-in-out, background-color 0.3s ease-in-out;
        }

        button:hover {
            background-color: #e85a4f;
            transform: scale(1.05);
        }

        button:active {
            transform: scale(0.95);
        }

        .hidden {
            display: none;
        }

        select {
            cursor: pointer;
        }

        .meal-inputs h3 {
            color: #ff6f61;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1> Nutrition Planner 🍏</h1>
        
        <!-- Set Goals Section -->
        <div class="goals">
            <h2>Set Your Goals 🎯</h2>
            
            <label for="calories">Calories:</label>
            <input type="number" id="calories" placeholder="Enter calories goal" required>
            
            <label for="protein">Protein (g):</label>
            <input type="number" id="protein" placeholder="Enter protein goal" required>
            
            <label for="days">Days of Meal Planning:</label>
            <input type="number" id="days" placeholder="Enter number of days" required>
            
            <button onclick="setGoals()">Set Goals 🚀</button>
        </div>

        <!-- Meal Planner Section -->
        <div id="meal-planner" class="meal-planner hidden">
            <h2>Plan Your Meals 🥗</h2>
            
            <div id="meal-inputs"></div>
            
            <button onclick="submitMeals()">Submit Meals 📝</button>
        </div>

        <!-- Summary Section -->
        <div id="summary" class="summary hidden">
            <h2>Your Meal Summary 📊</h2>
            
            <p id="summary-text"></p>
        </div>
    </div>

    <script>
        let goals = {};

        // Food options for dropdown menus
        const foodOptions = {
          breakfast: ["Oatmeal 🥣", "Pancakes 🥞", "Smoothie 🥤", "Eggs 🍳", "Toast 🍞"],
          lunch: ["Salad 🥗", "Sandwich 🥪", "Soup 🍜", "Burger 🍔", "Sushi 🍣"],
          dinner: ["Steak 🥩", "Pasta 🍝", "Pizza 🍕", "Stir-fry 🍛", "Tacos 🌮"],
          dessert: ["Ice Cream 🍨", "Cake 🍰", "Brownie 🍫", "Fruit Salad 🍓🍍", "Cookies 🍪"]
        };

        function setGoals() {
          const calories = document.getElementById("calories").value;
          const protein = document.getElementById("protein").value;
          const days = document.getElementById("days").value;

          if (calories && protein && days) {
              goals = { calories, protein, days };
              document.getElementById("meal-planner").classList.remove("hidden");
              document.getElementById("meal-inputs").innerHTML = "";

              for (let i = 1; i <= days; i++) {
                  const dayDiv = document.createElement("div");
                  dayDiv.classList.add("meal-inputs");
                  dayDiv.innerHTML = `
                      <h3>Day ${i} 🌞</h3>

                      <label for="breakfast-${i}">Breakfast:</label>
                      ${createDropdown(`breakfast-${i}`, foodOptions.breakfast)}

                      <label for="lunch-${i}">Lunch:</label>
                      ${createDropdown(`lunch-${i}`, foodOptions.lunch)}

                      <label for="dinner-${i}">Dinner:</label>
                      ${createDropdown(`dinner-${i}`, foodOptions.dinner)}

                      <label for="dessert-${i}">Dessert:</label>
                      ${createDropdown(`dessert-${i}`, foodOptions.dessert)}
                  `;
                  document.getElementById("meal-inputs").appendChild(dayDiv);
              }
              
              document.getElementById("summary").classList.add("hidden");
          }
      }

      function createDropdown(id, options) {
          let dropdown = `<select id="${id}"><option value="">Select an option</option>`;
          options.forEach(option => {
              dropdown += `<option value="${option}">${option}</option>`;
          });
          dropdown += `</select>`;
          return dropdown;
      }

      function submitMeals() {
          let totalCalories = Math.floor(Math.random() * (500 * goals.days)); // Simulated calories
          let totalProtein = Math.floor(Math.random() * (50 * goals.days)); // Simulated protein

          const summaryText = `You planned ${goals.days} days of meals! 🎉\n
                               Total Calories Consumed (approx.): ${totalCalories}\n
                               Total Protein Consumed (approx.): ${totalProtein}\n
                               Your Goals - Calories per Day: ${goals.calories}, Protein per Day (g): ${goals.protein}`;

          document.getElementById("summary-text").innerText = summaryText.replace(/\n/g, "\n");
          
          document.getElementById("summary").classList.remove("hidden");
      }
    </script>
</body>
</html>
