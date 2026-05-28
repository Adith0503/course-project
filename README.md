# course-project
<html>
<head>
  <title>Roommate Task Manager</title>
  <style>
    body {
      font-family: Arial;
      text-align: center;
      background: #f4f4f4;
    }

    h1 {
      margin-top: 20px;
    }

    input {
      padding: 10px;
      margin: 5px;
    }

    button {
      padding: 10px;
      cursor: pointer;
    }

    ul {
      padding: 0;
    }

    li {
      list-style: none;
      margin: 10px;
      padding: 10px;
      background: white;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .done {
      text-decoration: line-through;
      color: gray;
    }
  </style>
</head>

<body>

<h1>🏠 Roommate Task Manager</h1>

<div>
  <input id="taskInput" placeholder="Enter task">
  <input id="userInput" placeholder="Roommate name">
  <button onclick="addTask()">Add Task</button>
</div>

<ul id="taskList"></ul>

<script>
  let tasks = JSON.parse(localStorage.getItem("tasks")) || [];

  function saveTasks() {
    localStorage.setItem("tasks", JSON.stringify(tasks));
  }

  function renderTasks() {
    const list = document.getElementById("taskList");
    list.innerHTML = "";

    tasks.forEach((task, index) => {
      const li = document.createElement("li");

      li.innerHTML = `
        <span class="${task.done ? 'done' : ''}">
          ${task.text} (${task.user})
        </span>
        <div>
          <button onclick="toggleTask(${index})">✔</button>
          <button onclick="deleteTask(${index})">❌</button>
        </div>
      `;

      list.appendChild(li);
    });
  }

  function addTask() {
    const text = document.getElementById("taskInput").value;
    const user = document.getElementById("userInput").value;

    if (text === "" || user === "") {
      alert("Please fill both fields");
      return;
    }

    tasks.push({ text, user, done: false });
    saveTasks();
    renderTasks();

    document.getElementById("taskInput").value = "";
    document.getElementById("userInput").value = "";
  }

  function toggleTask(index) {
    tasks[index].done = !tasks[index].done;
    saveTasks();
    renderTasks();
  }

  function deleteTask(index) {
    tasks.splice(index, 1);
    saveTasks();
    renderTasks();
  }

  renderTasks();
</script>

</body>
</html>
