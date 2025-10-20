
# 🚀 Kaiburr Task API – Java Spring Boot + MongoDB

This project is a **Java backend application** that provides REST API endpoints to manage and execute “Task” objects.  
Each **Task** represents a shell command that can be executed (locally or in a Kubernetes pod) and stores execution details in **MongoDB**.

---

## 🧩 Tech Stack
- **Java 17 / 21**
- **Spring Boot** (Web, Data MongoDB)
- **MongoDB**
- **Maven**
- **Postman / cURL** for testing

---

## 📁 Project Structure


src/
├─ main/java/com/kaiburr/taskapi/
│   ├─ controller/TaskController.java
│   ├─ model/Task.java
│   ├─ model/TaskExecution.java
│   ├─ repository/TaskRepository.java
│   ├─ service/TaskService.java
│   └─ TaskApiApplication.java
└─ main/resources/
└─ application.properties

`

---

## ⚙ Features

| Feature | Description |
|----------|--------------|
| 🧠 **Create Task** | Add a new task (with command validation) |
| 🔍 **Search Tasks** | Get all tasks or filter by ID or name |
| 🗑 **Delete Task** | Delete a task by ID |
| ⚡ **Execute Task** | Run a shell command and store execution result |
| 💾 **MongoDB Integration** | All tasks and executions persist in MongoDB |

---

## 🧰 Task Object Structure

json
{
  "id": "123",
  "name": "Print Hello",
  "owner": "John Smith",
  "command": "echo Hello World again!",
  "taskExecutions": [
    {
      "startTime": "2023-04-21T15:51:42.276Z",
      "endTime": "2023-04-21T15:51:43.276Z",
      "output": "Hello World!"
    }
  ]
}
`

---

## 🌐 API Endpoints & Screenshots

### 🔹 1. Get All Tasks

**GET** `/api/tasks`

Retrieves all existing tasks from MongoDB.

**Response Example:**

json
[
  {
    "id": "123",
    "name": "Print Hello",
    "owner": "John Smith",
    "command": "echo Hello World!"
  }
]


📸 **Screenshot:**
![Get All Tasks](https://github.com/AmalRayudu19/Task-1/blob/main/get.jpg)

---

### 🔹 2. Get Task by ID

**GET** `/api/tasks/{id}`
Returns a single task or **404** if not found.

📸 **Screenshot:**
![Get Task by ID](https://github.com/AmalRayudu19/Task-1/blob/main/getbyid.jpg)

---

### 🔹 3. Create or Update Task

**PUT** `/api/tasks`

**Request Body:**

json
{
  "id": "123",
  "name": "Print Hello",
  "owner": "John Smith",
  "command": "echo Hello World!"
}


✅ Validates the command to ensure it’s safe before saving to MongoDB.

📸 **Screenshot:**
![Create Task](https://github.com/AmalRayudu19/Task-1/blob/main/notfound.jpg)

---

### 🔹 4. Delete Task

**DELETE** `/api/tasks/{id}`
Deletes a task by ID.

📸 **Screenshot:**
![Delete Task](https://github.com/AmalRayudu19/Task-1/blob/main/execute.jpg)

---

### 🔹 5. Search Task by Name

**GET** `/api/tasks/search/{name}`
Finds tasks whose name **contains** the given string.
If nothing matches, returns **404**.

📸 **Screenshot:**
![Search Task by Name](https://github.com/AmalRayudu19/Task-1/blob/main/post.jpg)

---

### 🔹 6. Execute Task Command

**PUT** `/api/tasks/{id}/run`

Executes the stored shell command for a specific task, captures output, and stores an execution record in MongoDB.

**Response Example:**

json
{
  "id": "123",
  "name": "Print Hello",
  "owner": "John Smith",
  "command": "echo Hello World!",
  "taskExecutions": [
    {
      "startTime": "2025-10-19T10:21:00Z",
      "endTime": "2025-10-19T10:21:01Z",
      "output": "Hello World!"
    }
  ]
}


📸 **Screenshot:**
![Execute Task](https://github.com/AmalRayudu19/Task-1/blob/main/put.jpg)

---

## 🧪 Testing with Postman

| Method | Endpoint                   | Description             |
| ------ | -------------------------- | ----------------------- |
| GET    | `/api/tasks`               | Get all tasks           |
| GET    | `/api/tasks/{id}`          | Get by ID               |
| GET    | `/api/tasks/search/{name}` | Search by name          |
| PUT    | `/api/tasks`               | Create or update a task |
| DELETE | `/api/tasks/{id}`          | Delete a task           |
| PUT    | `/api/tasks/{id}/run`      | Execute a command       |

---

## 🧩 Validation Rules

Unsafe or malicious commands like these are **blocked**:


rm, sudo, shutdown, reboot, kill, format


**Error Example:**

json
{
  "error": "Unsafe command detected"
}


📸 **Screenshot (Invalid Command):**
![Unsafe Command Validation](screenshots/invalid_command.png)

---

## 🧑‍💻 Setup Instructions

### 1️⃣ Clone the Repository

bash
git clone https://github.com/<your-username>/kaiburr-task-api.git
cd kaiburr-task-api


### 2️⃣ Configure MongoDB

Edit `src/main/resources/application.properties`:

properties
spring.data.mongodb.uri=mongodb://localhost:27017/kaiburrdb
server.port=8080


### 3️⃣ Build and Run

bash
mvn clean install
mvn spring-boot:run


---


Would you like me to make it *GitHub-styled* with a banner/title emoji and collapsible “Endpoints” sections (for cleaner scrolling)?
```
