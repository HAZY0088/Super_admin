# 🍴 Cloud Kitchen Super Admin – Backend

This is the **backend service** for the **Cloud Kitchen Super Admin platform**.  
It is built using **Spring Boot (Java)** with **Spring Security (JWT)**, **Spring Data JPA**, and **MySQL**.  
The backend provides REST APIs for managing managers, kitchens, delivery partners, authentication, and reports.

---

## 🚀 Features
- 🔑 **Authentication**
  - Super Admin login with **JWT token-based authentication**
- 👨‍💼 **Manager Management**
  - Create, list, update, and delete managers
  - Assign managers to kitchens
- 🚚 **Delivery Partner Management**
  - Register delivery partners
  - List and delete delivery partners
- 🍴 **Kitchen Management**
  - Create and manage kitchens
  - Assign managers and delivery partners
- 📊 **Reports**
  - View financial and performance reports
- 📂 **Excel Export**
  - Export kitchens, managers, delivery partners data to Excel (using Apache POI)

---

## 🛠️ Tech Stack
- **Java 17+**
- **Spring Boot 3**
- **Spring Security 6** (JWT)
- **Spring Data JPA (Hibernate)**
- **MySQL**
- **Apache POI** (for Excel export)
- **Maven**

---

## 📦 Project Structure
```
cloud-kitchen-superadmin
 ┣ src/main/java/com/cloudkitchen/admin
 ┃ ┣ config/        # Security config, JWT filter
 ┃ ┣ controller/    # REST Controllers (Auth, Manager, Kitchen, Delivery, Reports, Export)
 ┃ ┣ model/         # JPA Entities (Admin, Manager, Kitchen, DeliveryPartner)
 ┃ ┣ repository/    # Spring Data JPA Repositories
 ┃ ┣ service/       # Business logic & Excel export service
 ┃ ┗ util/          # Utility classes (JWT utils, etc.)
 ┣ src/main/resources
 ┃ ┣ application.properties
 ┃ ┗ data.sql       # (optional) Initial test data
 ┗ pom.xml
```

---

## ⚙️ Setup & Run

### 1️⃣ Clone the repository
```bash
git clone https://github.com/HAZY0088/Super_admin.git
cd cloud-kitchen-superadmin-final
```

### 2️⃣ Configure MySQL
Create a database in MySQL:
```sql
CREATE DATABASE superadmin;
```

Update `src/main/resources/application.properties`:
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/superadmin
spring.datasource.username=root
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

### 3️⃣ Run the app
```bash
mvn spring-boot:run
```

Backend runs at:  
👉 `http://localhost:8080`

---

## 🔑 Super Admin Login
Default super admin (insert manually in DB):

```sql
INSERT INTO admin (username, password)
VALUES ('superadmin', '$2a$10$e8ZkXXoHUpHug7fYQzG/ceRyz5x2FJzFG8M8fZrg1uOXCRMy3r0DS');
```

> The above hash is for password: **`SuperAdmin@123`**

Login API:
```http
POST /api/admin/login
Content-Type: application/json

{
  "username": "superadmin",
  "password": "SuperAdmin@123"
}
```

Response:
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR..."
}
```

---

## 📌 API Endpoints

### Auth
- `POST /api/admin/login` → Login (JWT token)

### Managers
- `POST /api/admin/managers` → Create Manager
- `GET /api/admin/managers` → Get all Managers
- `DELETE /api/admin/managers/{id}` → Delete Manager
- `PUT /api/admin/managers/{id}` → Update Manager

### Delivery Partners
- `POST /api/admin/delivery-partners` → Create Delivery Partner
- `GET /api/admin/delivery-partners` → Get all Delivery Partners
- `DELETE /api/admin/delivery-partners/{id}` → Delete Delivery Partner

### Kitchens
- `POST /api/admin/kitchens` → Create Kitchen
- `GET /api/admin/kitchens` → Get all Kitchens
- `DELETE /api/admin/kitchens/{id}` → Delete Kitchen

### Reports
- `GET /api/admin/reports` → Get Reports

### Excel Export
- `GET /api/admin/export/all` → Download Excel with all data
- `GET /api/admin/export/kitchen/{id}` → Download Excel for one kitchen

---

## 🧪 Testing with Postman
A **Postman collection** is available in the repo:  
`Cloud Kitchen Super Admin API.postman_collection.json`

Import it into Postman to test all endpoints quickly.

---

## 📄 License
This project is for educational/demo purposes. You can extend it into a full production-ready cloud kitchen management system.
