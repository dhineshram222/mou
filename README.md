# MOUTracker
# Overview
MOUTracker is a full-stack web application designed to manage and track Memoranda of Understanding (MOUs) between institutions and faculty members.

The system centralizes MOU records by storing metadata (institute, faculty, duration, purpose, outcomes, etc.) along with the signed document, making it easier to search, filter, export, and get notifications about expiry dates.

This project is a prototype for small academic departments or institutions, built with React (frontend) and Node.js/Express (backend), with Excel file storage for simplicity.

# Features

User Registration & Login (basic authentication).
Add new MOUs with details + signed document upload.
Store metadata in Excel (mou_data.xlsx).
Filter MOUs by faculty, institute, academic year, or duration.
Export filtered results as Excel file.
Notifications for upcoming expiry dates.
View/download signed MOU files from uploads/ folder.

# Tech Stack

Frontend: React.js, Axios, React Router, XLSX

Backend: Node.js, Express.js, Multer (file upload), XLSX (Excel handling)

Storage:

MOU Records → mou_data.xlsx

User Accounts → users.json

Signed Documents → uploads/ folder

# Workflow

Authentication:

Users register/login with email & password.

Credentials stored in users.json.

Adding a New MOU:

Fill details (institute, faculty, purpose, duration, outcomes, etc.).

Upload signed document (PDF/Word/Image).

Backend saves file in uploads/ and appends metadata into mou_data.xlsx.

Filtering & Exporting:

Users filter MOUs by faculty name, academic year, duration, or institute.

Filtered data returned as JSON and displayed in table.

Export option to download results as Excel file.

Notifications:

System checks expiry dates based on AddedDate + Duration.

Shows alerts for MOUs nearing expiry.



# API Endpoints

1.Register a new user:

`POST /api/register`
Request Body (JSON):

```json
{
  "username": "admin",
  "password": "securePassword"
}
```

**Response:**

```json
{ "message": "User registered successfully" }
```

---

### 2. **Login**

`POST /api/login`
**Request Body (JSON):**

```json
{
  "username": "admin",
  "password": "securePassword"
}
```

**Response:**

```json
{ "message": "Login successful" }
```

---

### 3. **Add New MOU**

`POST /api/mou/add` (multipart/form-data)
**Request Body (form-data):**

```
institution: "IIT Delhi"
country: "India"
start_date: "2025-01-01"
end_date: "2027-01-01"
file: (PDF/DOC upload)
```

**Response:**

```json
{ "message": "MOU added successfully" }
```

---

### 4. **Filter MOUs**

`GET /api/mou/filter?institution=IIT Delhi&country=India`
**Response:**

```json
[
  {
    "institution": "IIT Delhi",
    "country": "India",
    "start_date": "2025-01-01",
    "end_date": "2027-01-01",
    "file": "/uploads/mou_iitdelhi.pdf"
  }
]
```

---

### 5. **Access Uploaded File**

`GET /uploads/<filename>`

* Returns the actual signed MOU document (PDF/DOC).

---

