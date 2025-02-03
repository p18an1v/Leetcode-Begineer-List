# LeetCode Begineer List Tracker 

LeetCode Begineer List Tracker is a full-stack application that allows users to track their progress on coding questions categorized by topics and patterns. The project uses **Spring Boot** for the backend, **MongoDB** as the database, and **ReactJS** for the frontend.

## Features
- User authentication (Login, Registration, Forgot Password, Reset Password)
- Track solved questions by topic and pattern
- Admin functionalities to manage topics, patterns, and questions
- RESTful API with JWT authentication

## Technologies Used
- **Backend:** Spring Boot, Spring Security, MongoDB
- **Frontend:** ReactJS (Vite), React Router
- **Authentication:** JWT-based security
- **Database:** MongoDB
- **Build Tool:** Maven

---

## Getting Started
### Prerequisites
Ensure you have the following installed:
- Java 17+
- Maven
- MongoDB
- Node.js & npm (for frontend)

### Backend Setup
1. Clone the repository:
   ```sh
   git clone https://github.com/yourusername/leetcode-tracker.git
   cd leetcode-tracker/backend
   ```
2. Install dependencies:
   ```sh
   mvn clean install
   ```
3. Configure MongoDB connection in `application.properties`:
   ```properties
   spring.data.mongodb.uri=mongodb://localhost:27017/leetcode_tracker
   ```
4. Run the application:
   ```sh
   mvn spring-boot:run
   ```

### Frontend Setup
1. Navigate to the frontend folder:
   ```sh
   cd ../frontend
   ```
2. Install dependencies:
   ```sh
   npm install
   ```
3. Start the frontend:
   ```sh
   npm run dev
   ```

---

## API Endpoints

### Authentication
| Method | Endpoint | Description |
|--------|---------|-------------|
| POST | `/api/auth/login` | User login |
| POST | `/api/auth/register` | User registration |
| POST | `/api/auth/forgot-password` | Request password reset |
| POST | `/api/auth/reset-password` | Reset user password |

### User
| Method | Endpoint | Description |
|--------|---------|-------------|
| GET | `/api/user/details` | Get user details |
| GET | `/api/user/progress/{userId}` | Get user progress |
| POST | `/api/user/progress/{userId}/toggle?questionId={questionId}&completed=true` | Track a completed question |

### Topics
| Method | Endpoint | Description |
|--------|---------|-------------|
| GET | `/api/auth/topics/getAll` | Get all topics |
| GET | `/api/auth/topics/{topicId}/questions` | Get questions by topic |
| POST | `/api/admin/topics` | Add a new topic |
| PUT | `/api/admin/topics/{topicId}` | Update a topic |
| DELETE | `/api/admin/topics/{topicId}` | Delete a topic |

### Patterns
| Method | Endpoint | Description |
|--------|---------|-------------|
| GET | `/api/auth/patterns/getAll` | Get all patterns |
| GET | `/api/auth/patterns/{patternId}/questions` | Get questions by pattern |
| POST | `/api/admin/patterns` | Add a new pattern |
| PUT | `/api/admin/patterns/{patternId}` | Update a pattern |
| DELETE | `/api/admin/patterns/{patternId}` | Delete a pattern |

### Questions Management
| Method | Endpoint | Description |
|--------|---------|-------------|
| POST | `/api/admin/topics/{topicId}/questions` | Add a question to a topic |
| PUT | `/api/admin/topics/{topicId}/questions/{questionId}` | Update a topic question |
| DELETE | `/api/admin/topics/{topicId}/questions/{questionId}` | Delete a topic question |
| POST | `/api/admin/patterns/{patternId}/questions` | Add a question to a pattern |
| PUT | `/api/admin/patterns/{patternId}/questions/{questionId}` | Update a pattern question |
| DELETE | `/api/admin/patterns/{patternId}/questions/{questionId}` | Delete a pattern question |

---
## API Endpoints

### Authentication
```json
POST /api/auth/login
{
    "email": "eamil@gmail.com",
    "password": "password123"
}
Response:
{
    "token": "<JWT_TOKEN>",
    "message": "Login successful"
}
```
```json
POST /api/auth/register
{
    "email": "",
    "password": ""
}
```
```json
POST /api/auth/forgot-password
{
    "email": ""
}
```
```json
POST /api/auth/reset-password
{
    "token": "78a0ea2f-8fd8-4f9b-8ac6-7ac3b0ba5347",
    "newPassword": "password123"
}
```

### User
```json
GET /api/user/progress/{userId}
Response:
{
    "userId": "6791f8cb3d485764b917faa9",
    "userEmail": "email@gmail.com",
    "completedQuestions": [],
    "totalSolved": 0
}
```
```json
GET /api/user/details
Response:
{
    "id": "6791f8cb3d485764b917faa9",
    "email": "email@gmail.com",
    "role": "ROLE_USER"
}
```
```json
POST /api/user/progress/{userId}/toggle?questionId={questionId}&completed=true
Response:
{
    "userId": "6791f8cb3d485764b917faa9",
    "userEmail": "email@gmail.com",
    "completedQuestions": ["679279388f10b0104b3df475"],
    "totalSolved": 1
}
```

### Questions Management
```json
POST /api/admin/topics/{topicId}/questions
  {
       "questionId": "6792683e635d63456b2016d9",
        "questionName": "tree question",
        "url": "https://leetcode.com/problems/two-sum",
        "level": "Easy",
        "dataStructure": "Array"
   }
Response:
{
       "questionId": "6792683e635d63456b2016d9",
        "questionName": "tree question",
        "url": "https://leetcode.com/problems/two-sum",
        "level": "Easy",
        "dataStructure": "Array"
}
```
```json
PUT /api/admin/topics/{topicId}/questions/{questionId}
{
   "questionName": "Updated newly",
    "url": "https://leetcode.com/problems/two-sum",
    "level": "Medium",
    "dataStructure": "Array"
}
```
```json
DELETE /api/admin/topics/{topicId}/questions/{questionId}
```
```json
GET /api/admin/questions/{questionId}
Response:
{
    "id": "67a0e7f2c8cc19a3cff11f5c3",
    "title": "Updated Two Sum",
    "difficulty": "Medium",
    "topicId": "6793136c8cc19a3cff11f5b0",
    "patternId": "6799fb9acd728945292c0a96"
}
```

### Topics Management
```json
POST /api/admin/topics
{
    "dataStructure": "Linked List",
    "questionsList": []
}
```
```json
PUT /api/admin/{topicId}
{
    "dataStructure": "Updated new type",
    "questionsList": []
}
```
```json
DELETE /api/admin/{topicId}
```
```json
GET /api/admin/topics/{topicId}
Response:
{
    "id": "6793136c8cc19a3cff11f5b0",
    "dataStructure": "Updated testing",
    "questionIds": ["679314c18cc19a3cff11f5b3"]
}
```

### Patterns Management
```json
POST /api/admin/patterns
{
    "pattern": "two pointers",
    "questionsList": []
}
Response:
{
    "id": "6799fb9acd728945292c0a96",
    "pattern": "two pointers",
    "questionIds": []
}
```
```json
PUT /api/admin/patterns/{patternId}
```
```json
DELETE /api/admin/patterns/{patternId}
```

### Error Handling

All endpoints return appropriate status codes and error messages. Common status codes include:

- **200 OK**: For successful requests.
- **201 Created**: For successful creation of resources.
- **400 Bad Request**: For invalid or missing data.
- **404 Not Found**: When the requested resource is not found.
- **500 Internal Server Error**: For server-side errors.

### Contribution
1. Clone the repository:
   ```sh
   git clone <repo-url>
   ```
2. Install dependencies:
   ```sh
   cd frontend && npm install
   ```
   ```sh
   cd backend && mvn clean install
   ```
3. Run the backend:
   ```sh
   mvn spring-boot:run
   ```
4. Run the frontend:
   ```sh
   npm run dev
   ```


## License
This project is open-source and available for anyone.

## Contact
For any queries, reach out at: **p18an1v@gmail.com**
