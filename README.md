<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>GPA Calculator</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        background-color: #f4f4f4;
      }
      .container {
        background: white;
        padding: 30px;
        border-radius: 10px;
        box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.2);
        width: 500px;
      }
      h2 {
        text-align: center;
      }
      .header {
        display: flex;
        font-weight: bold;
        margin-bottom: 10px;
      }
      .header div {
        flex: 1;
        text-align: center;
      }
      .subject {
        display: flex;
        margin-bottom: 15px;
      }
      input,
      select {
        padding: 10px;
        margin: 5px;
        border: 1px solid #ccc;
        border-radius: 5px;
        flex: 1;
      }
      button {
        width: 100%;
        padding: 12px;
        border: none;
        border-radius: 5px;
        background-color: #007bff;
        color: white;
        cursor: pointer;
        margin-top: 15px;
        font-size: 16px;
      }
      button:hover {
        background-color: #0056b3;
      }
      #result {
        text-align: center;
        font-size: 20px;
        margin-top: 15px;
        font-weight: bold;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <h2>GPA Calculator</h2>
      <div class="header">
        <div>Subject Name</div>
        <div>Grade</div>
      </div>
      <div id="subjects"></div>
      <button onclick="addSubject()">Add Subject</button>
      <button onclick="calculateGPA()">Calculate GPA</button>
      <div id="result"></div>
    </div>

    <script>
      const gradePoints = {
        S: 10,
        A: 9,
        B: 8,
        C: 7,
        D: 6,
        E: 4,
        F: 0,
      };

      function addSubject() {
        const subjectsDiv = document.getElementById("subjects");
        const div = document.createElement("div");
        div.classList.add("subject");
        div.innerHTML = `
                <input type="text" placeholder="Subject Name (Optional)" />
                <select>
                    <option value="S">S (90-100)</option>
                    <option value="A">A (80-89)</option>
                    <option value="B">B (70-79)</option>
                    <option value="C">C (60-69)</option>
                    <option value="D">D (50-59)</option>
                    <option value="E">E (40-49)</option>
                    <option value="F">F (Below 40)</option>
                </select>
            `;
        subjectsDiv.appendChild(div);
      }

      function initializeSubjects() {
        for (let i = 0; i < 3; i++) {
          addSubject();
        }
      }

      function calculateGPA() {
        const subjects = document.querySelectorAll(".subject select");
        if (subjects.length < 3) {
          document.getElementById("result").innerText =
            "Please enter at least 3 subjects.";
          return;
        }
        let totalPoints = 0,
          count = 0;
        subjects.forEach((select) => {
          totalPoints += gradePoints[select.value];
          count++;
        });
        const gpa = count > 0 ? (totalPoints / count).toFixed(2) : 0;
        document.getElementById("result").innerText = `Your GPA: ${gpa}`;
      }

      window.onload = initializeSubjects;
    </script>
  </body>
</html>
