# How to bind PostgreSQL database to a Pivot Table

A quick start project for connecting a PostgreSQL database to a Syncfusion Pivot Table. This repository includes a Web API Controller ([MyWebService](./MyWebService/)) for retrieving data from a PostgreSQL database, as well as quick start samples in the [TypeScript](./Typescript/), [JavaScript](./Javascript/), [Angular](./Angular/), [React](./React/), [VUE](./VUE/), ASP.NET [Core](./Core/), [Blazor](./Blazor/) and [MVC](./MVC/) platforms that display the retrieved data in a Syncfusion Pivot Table.

---

## 🔎 Analysis Report
- Repository: web-bind-PostgreSQL-database-to-pivot-table — https://github.com/SyncfusionExamples/web-bind-PostgreSQL-database-to-pivot-table
- Detected languages: C#, JavaScript, TypeScript, HTML (server: .NET Web API; clients: JS/TS/Angular/React/Vue)
- Repository type: Showcase / Educational sample (end-to-end demo)
- Primary dependencies (inferred): Npgsql or Npgsql.EntityFrameworkCore.PostgreSQL, Microsoft.AspNetCore.* (server), @syncfusion/ej2-pivotview (clients), Node.js tooling
- Maturity: Sample/demo — Stable as example code; not a production library
- Community activity: Typical SyncfusionExamples pattern — low PR/issue volume; update cadence TBD
- Documentation gaps: No consolidated README with SEO metadata, missing explicit dependency versions and CI badges, missing CONTRIBUTING/CODE_OF_CONDUCT
- Recommended focus: Add dependency versions, quick start for each client, API contract, CORS and security notes, and GitHub topics

---

## 🚀 Hero — What this repo does
A compact, multi-framework sample showing how to expose PostgreSQL query results via a .NET Web API and bind the returned JSON to a Syncfusion Pivot Table (PivotView) on client apps (JS/TS/Angular/React/Vue, ASP.NET Core, Blazor, MVC).

---

## 📚 Table of Contents
- ✅ Quick overview
- ✨ Key features
- 🛠️ Supported technologies & requirements
- ⚙️ Installation & setup
- 🧩 Quick code samples (3–5)
- 🏗️ Project structure
- ❓ Troubleshooting & FAQ
- 🤝 Contributing & License
- 🔎 SEO & GitHub metadata

---

## ✅ Quick overview
This project demonstrates the end-to-end flow: PostgreSQL → .NET Web API → Syncfusion PivotView. It helps developers build BI-style pivot reports using relational data served as JSON.

Use cases: dashboards, ad-hoc reporting, analytics prototypes.

---

## ✨ Key features
- Server-side endpoint exposing PostgreSQL query results as JSON
- Client examples across JS/TS/Angular/React/Vue and server-side (.NET Core/Blazor/MVC)
- Appsettings sample for secure DB connection
- Minimal, copy-paste-ready PivotView initialization
- CORS and sample fetch usage (recommended)

Benefits: fast prototyping, multi-framework reference, reusable server + client patterns.

---

## 🛠️ Supported technologies & requirements
- .NET SDK 6.0+ (project files: MyWebService/*.csproj)
- PostgreSQL 11+
- Npgsql ADO.NET provider (or EF Core provider) — recommended Npgsql 7.x (align with .NET SDK)
- Node.js 14+ for client samples
- Syncfusion EJ2 PivotView packages (npm / NuGet) — ensure license compliance
- Modern browsers (Chrome, Edge, Firefox, Safari)

Suggested dependency examples:
- Npgsql >= 7.0.0
- Microsoft.AspNetCore.App (as in project file)
- @syncfusion/ej2-pivotview ^20.1.0 (match client samples)

---

## ⚙️ Installation & setup (quick)
Prerequisites:
- PostgreSQL server with sample table (e.g., sales_table)
- .NET SDK 6.0+
- Node.js 14+
- Syncfusion packages (trial or licensed)

1. Clone
```bash
git clone https://github.com/SyncfusionExamples/web-bind-PostgreSQL-database-to-pivot-table.git
cd web-bind-PostgreSQL-database-to-pivot-table
```

2. Configure DB (MyWebService/Controllers/PivotController.cs)
```csharp
private dynamic GetPostgreSQLResult()
{
    NpgsqlConnection connection = new NpgsqlConnection("<Enter your valid connection string here>");
}
```

3. Run Web API
```bash
cd MyWebService
dotnet restore
dotnet build
dotnet run
# API: http://localhost:xxxx/...
```

4. Run a client (TypeScript example)
```bash
cd ../Typescript
npm install
npm start
# open the served app in browser
```

Tips:
- Enable CORS in Startup/Program to allow local client origins.
- Use environment variables for production DB credentials.

---

## 🧩 Quick code samples

1) SQL example (sample table)
```sql
CREATE TABLE sales_table (
  id serial PRIMARY KEY,
  category text,
  subcategory text,
  region text,
  sales numeric
);
```

2) Minimal .NET Web API controller (Npgsql)
```csharp
// Controllers/PivotDataController.cs
using Microsoft.AspNetCore.Mvc;
using Npgsql;
using System.Data;

[ApiController]
[Route("[controller]")]
public class PivotController : ControllerBase
{
    [HttpGet(Name = "GetPostgreSQLResult")]
    public object Get()
    {
        return JsonConvert.SerializeObject(GetPostgreSQLResult());
    }

    private dynamic GetPostgreSQLResult()
    {
        NpgsqlConnection connection = new NpgsqlConnection("<Enter your valid connection string here>");
        connection.Open();
        NpgsqlCommand command = new NpgsqlCommand("SELECT * FROM apxtimestamp", connection);
        NpgsqlDataAdapter dataAdapter = new NpgsqlDataAdapter(command);
        DataTable dataTable = new DataTable();
        dataAdapter.Fill(dataTable);
        connection.Close();
        return dataTable;
    }
}
```

4) Vanilla JS — fetch + PivotView init
```html
<div id="PivotView"></div>
<script src="https://cdn.syncfusion.com/ej2/32.1.19/dist/ej2.min.js"></script>
<script>
var pivotObj = new ej.pivotview.PivotView({
  dataSourceSettings: {
    url: 'https://localhost:xxxx/...',
  },
  showFieldList: true,
  width: '100%',
  height: 350,
});
pivotObj.appendTo('#PivotView');
</script>
```

5) TypeScript snippet (TS client)
```ts
import { PivotView } from '@syncfusion/ej2-pivotview';
let pivotTableObj: PivotView = new PivotView({
dataSourceSettings: {
  url: 'https://localhost:44378/Pivot',
},
showFieldList: true,
width: '100%',
height: 350,
});
pivotTableObj.appendTo('#PivotView');
```

---

## 🏗️ Project structure (high level)
- MyWebService/ — .NET Web API (controllers, models, appsettings.json)
- Typescript/ — TypeScript client demo
- Javascript/ — Plain JS demo
- Angular/, React/, VUE/ — framework demos
- Core/, Blazor/, MVC/ — ASP.NET examples
- LICENSE, README.md — repo metadata

---

## ❓ Troubleshooting & FAQ
- Empty response: check DB connection string and table data.
- CORS blocked: enable CORS in Program.cs with allowed origins.
- Field mismatch: ensure JSON keys match PivotView field names (case-sensitive depending on client).
- Syncfusion errors: confirm package versions & license activation.

---

## 🤝 Contributing & license
- Suggested files to add: CONTRIBUTING.md, CODE_OF_CONDUCT.md, ISSUE_TEMPLATEs, PR_TEMPLATE.
- License: see LICENSE file.

Minimal CONTRIBUTING.md outline (add to repo root):
```markdown
# 🤝 Contributing
- Fork → feature branch → PR
- Describe changes, tests, and run instructions
- Keep PRs scoped and include screenshots or logs
```

---

## 🔎 SEO & GitHub metadata (recommended)
Repository description (<=160 chars):
"Example showing how to bind a PostgreSQL database to a Syncfusion Pivot Table via a .NET Web API with JS/TS/Angular/React/Vue and .NET samples."

Suggested topics (comma-separated):
postgreSQL, syncfusion, pivot-table, pivotview, aspnet-core, dotnet, javascript, typescript, angular, react, vue, blazor, mvc, analytics, dashboard, sample

Primary keywords:
- Syncfusion Pivot Table
- PostgreSQL Pivot binding
- PivotView PostgreSQL example

Secondary keywords:
- .NET Web API Npgsql
- Syncfusion EJ2 PivotView
- analytics dashboard sample

Meta description (example):
"Bind PostgreSQL to Syncfusion Pivot Table via .NET Web API — client samples for JS/TS/Angular/React/Vue + ASP.NET Core/Blazor/MVC."

Structured data (JSON-LD) suggestion:
- Add a simple JSON-LD snippet in docs/pages for richer search results (title, description, repo URL, license, author, keywords).

---

## ✅ Next steps & recommendations
- Add explicit dependency versions (csproj / package.json).
- Add CI badge (GitHub Actions) and test coverage if applicable.
- Add CONTRIBUTING.md, CODE_OF_CONDUCT.md, ISSUE/PR templates.
- Provide sample dataset SQL and Postman collection for API testing.
- Add live demo link or screenshots/GIFs demonstrating PivotView with sample data.

---

## 📌 Last updated
2026-02-03
