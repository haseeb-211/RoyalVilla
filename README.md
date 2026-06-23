# 🏰 RoyalVilla – Luxury Villa Booking Platform

> A **modern ASP.NET Core Full-Stack solution** featuring a secure REST API (JWT + Refresh Tokens) and an MVC frontend consuming it.

---

## 📌 Overview
RoyalVilla is a scalable villa booking system built with:
- ⚙️ ASP.NET Core Web API (.NET 10)
- 🧑‍💻 ASP.NET Core MVC Frontend
- 🔐 JWT Authentication + Refresh Tokens
- 🗄️ Entity Framework Core + SQL Server
- 📦 Clean Architecture with DTO separation

---

## 🧱 Architecture

### Backend (RoyalVilla_API)
- RESTful API with versioning (`api/v1/...`)
- ASP.NET Core Identity for authentication
- JWT + Refresh Token system with reuse detection
- EF Core + Code First migrations
- OpenAPI / Scalar documentation

### Frontend (RoyalVillaWeb)
- ASP.NET Core MVC UI
- Cookie-based session authentication
- HttpClientFactory integration
- Typed service layer (`VillaService`, `AuthService`)
- TokenProvider for API communication

---

## 📂 Projects Structure

### 🔹 RoyalVilla_API
- `Controllers/`
  - AuthController
  - VillaController (v1)
- `Services/`
  - AuthService
  - TokenService
  - ImageService
- `Data/`
  - ApplicationDbContext
- `Migrations/`

### 🔹 RoyalVillaWeb
- `Controllers/`
  - HomeController
  - VillaController
  - AuthController
- `Services/`
  - VillaService
  - AuthService
  - TokenProvider
- `SD.cs` (Shared constants)

### 🔹 RoyalVilla.DTO
- VillaDTO
- LoginRequestDTO
- RegisterationRequestDTO
- Token DTOs

---

## ⚙️ Prerequisites
- .NET 10 SDK
- SQL Server (LocalDB or full instance)
- Visual Studio 2026 or CLI
- Postman (optional)

---

## 🔧 Configuration

### API (`appsettings.json`)
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=RoyalVillaDb;Trusted_Connection=True;"
  },
  "JwtSettings": {
    "Secret": "YOUR_SUPER_SECURE_SECRET_KEY"
  }
}
```

### Web (`appsettings.json`)
```json
{
  "ServiceUrls": {
    "VillaAPI": "https://localhost:5001/"
  }
}
```

---

## 🗄️ Database Setup

Run migrations:

```bash
dotnet ef database update --project RoyalVilla_API
```

Or in Visual Studio:
```
Update-Database
```

---

## 🚀 Running the Project

### Step 1: Start API
```bash
dotnet run --project RoyalVilla_API
```

### Step 2: Start MVC Web
```bash
dotnet run --project RoyalVillaWeb
```

### Step 3: Open in browser
- 🌐 MVC Frontend: `https://localhost:{port}`
- 📘 API Docs: `/scalar` or `/openapi`

---

## 🔐 Authentication Flow

1. User logs in via `/api/auth/login`
2. API returns:
   - JWT Access Token
   - Refresh Token
3. Frontend stores tokens in session
4. Each API call includes:
   ```
   Authorization: Bearer <token>
   ```
5. Refresh token endpoint regenerates access tokens securely

---

## 📡 API Endpoints

### Auth
- `POST /api/auth/register`
- `POST /api/auth/login`
- `POST /api/auth/refresh-token`

### Villas
- `GET /api/v1/villa`
- `GET /api/v1/villa/{id}`
- `POST /api/v1/villa` (Admin)
- `PUT /api/v1/villa/{id}` (Admin)
- `DELETE /api/v1/villa/{id}` (Admin)

---

## 🧪 Sample Login Request

```bash
curl -X POST https://localhost:5001/api/auth/login \
-H "Content-Type: application/json" \
-d '{"email":"user@example.com","password":"P@ssw0rd"}'
```

---

## 🛡️ Security Highlights
- JWT Authentication
- Refresh Token Rotation
- Token Family Reuse Detection
- Role-Based Authorization (Admin / User)
- Secure secret handling via environment variables

---

## 🧠 Development Notes
- AutoMapper for DTO mapping
- Dependency Injection everywhere
- Clean separation of concerns
- Typed HttpClient usage
- Session-based frontend token storage

---

## 🐛 Troubleshooting
- ❌ 401 Unauthorized → check JWT secret mismatch
- ❌ API not reachable → verify ServiceUrls
- ❌ DB errors → run migrations
- ❌ CORS issues → enable API CORS policy

---

## 🤝 Contributing
- Follow existing architecture patterns
- Keep controllers thin
- Put logic inside services
- Never commit secrets

---

## 🏁 Final Note
RoyalVilla is designed as a **production-style backend architecture demo** showcasing modern ASP.NET Core best practices.
