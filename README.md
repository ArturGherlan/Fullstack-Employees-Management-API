# Fullstack Employees Management

Employee management built as two halves: a REST API on .NET 6 with Entity
Framework Core, and an Angular 14 single-page front end that consumes it.

## What it does

Create, list, edit and delete employees. The API exposes them over REST,
Entity Framework Core handles persistence against SQL Server, and the Angular
app provides the screens.

## Layout

```
FullStack API/FullStack.API/FullStack.API/
  Controllers/EmployeesController.cs     the REST endpoints
  Data/FullStackDbContext.cs             the EF Core context
  Models/Employee.cs                     the entity
  Migrations/                            schema history
  appsettings.json                       connection string

FullStack UI/FullStack.UI/
  src/app/components/employees/          list, add and edit screens
  src/app/services/employees.service.ts  the HTTP client
  src/app/models/employee.model.ts
  src/environments/                      the API base URL per build
```

## Running it

**Requirements:** .NET 6 SDK, Node.js with the Angular CLI, and SQL Server
(Express or LocalDB).

**API.** Point `ConnectionStrings:FullStackConnectionString` in
`appsettings.json` at your SQL Server instance, then apply the migrations and
start it:

```bash
dotnet ef database update
```

```bash
dotnet run
```

It listens on `https://localhost:7061` by default.

**Front end.** From `FullStack UI/FullStack.UI`:

```bash
npm install
```

```bash
ng serve
```

Then open `http://localhost:4200`. If the API runs on a different port, change
`baseApiUrl` in `src/environments/environment.ts`.

## Notes

The connection string uses `Trusted_Connection=true`, so it carries Windows
credentials rather than a password, and no secret is committed. Build output,
NuGet caches and Visual Studio files are not tracked — see `.gitignore`.
