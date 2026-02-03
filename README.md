# How to bind PostgreSQL database to a Pivot Table

A quick start project for connecting a PostgreSQL database to a Syncfusion Pivot Table. This repository includes a Web API Controller ([MyWebService](./MyWebService/)) for retrieving data from a PostgreSQL database, as well as quick start samples in the [TypeScript](./Typescript/), [JavaScript](./Javascript/), [Angular](./Angular/), [React](./React/), [VUE](./VUE/), ASP.NET [Core](./Core/), [Blazor](./Blazor/) and [MVC](./MVC/) platforms that display the retrieved data in a Syncfusion Pivot Table.

---

📋 Repository Analysis Summary
- 🔎 Repository: web-bind-PostgreSQL-database-to-pivot-table (SyncfusionExamples)  
- 🧩 Languages: C# (ASP.NET Core), TypeScript/JavaScript, HTML/CSS  
- 🏷️ Type: Showcase / Starter template / Multi-platform samples  
- ⚙️ Primary dependencies: Syncfusion EJ2 (PivotView), .NET 6 (inferred), Npgsql or MySqlConnector (for DB examples)  
- 📈 Maturity: Example/demo — stable for learning and quick-start integration  
- 🧭 Target audience: Web developers integrating Syncfusion PivotView with relational DBs (intermediate)  
- 📝 Documentation gaps: add LICENSE, SQL schema/seed, CI badge, explicit install steps, security examples (parameterized SQL/ORM)

---

🚀 Quick Overview
This repository demonstrates binding a PostgreSQL backend to Syncfusion EJ2 PivotView across multiple frontend stacks and provides server-side endpoints compatible with Syncfusion DataManager for fetching data source.

---

✨ Key Features
- Multi-framework client samples: TypeScript, JavaScript, Angular, React, Vue, Blazor, ASP.NET Core, MVC  
- Web API controller (MyWebService) to fetch/serve pivot data from PostgreSQL
- Default examples for PivotView UI  
- Config via appsettings.json for secure connection strings

---

🛠️ Supported Technologies & Requirements
- .NET 6.0+ (recommended)  
- Syncfusion EJ2 PivotView (client assets or npm package)  
- PostgreSQL (recommended 9.6+/12+) with Npgsql provider
- Node.js & npm (for building frontend samples)

Example appsettings.json (PostgreSQL):
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Port=5432;Database=NetworkSupportDB;Username=postgres;Password=yourpassword"
  }
}
```

---

⚙️ Installation & Setup
Prerequisites:
- .NET 6 SDK installed
- PostgreSQL server running and reachable
- Node.js (for frontend builds)

Steps:
1. Clone:
   ```bash
   git clone https://github.com/SyncfusionExamples/web-bind-PostgreSQL-database-to-pivot-table.git
   cd web-bind-PostgreSQL-database-to-pivot-table
   ```
2. Update `appsettings.json` connection string.
3. Restore and run:
   ```bash
   dotnet restore
   dotnet run --project ./Core/YourWebProject.csproj
   ```
4. (Optional) Build frontend samples:
   ```bash
   cd Typescript
   npm install
   npm run build
   ```

Troubleshooting tips:
- Verify DB credentials and network access.
- Enable CORS in Program.cs when serving client from a different origin.
- Inspect browser console for missing Syncfusion assets.

---

📦 Quick Start — Minimal snippets

Program.cs (minimal)
```csharp
var builder = WebApplication.CreateBuilder(args);
builder.Services.AddControllers();
var app = builder.Build();
app.MapControllers();
app.Run();
```

Controller constructor (read connection string)
```csharp
public class GridController : ControllerBase {
  private readonly string _conn;
  public GridController(IConfiguration cfg) => _conn = cfg.GetConnectionString("DefaultConnection");
}
```

Client PivotView (basic)
```html
<div id="PivotView"></div>
<script>
  var pv = new ej.pivotview.PivotView({
    dataSourceSettings: { 
        url: /* configure to fetch from /api/Grid */ 
    },
    height: 600
  });
  pv.appendTo('#PivotView');
</script>
```

---

🧭 Project Structure (recommended)
- /Core or /MyWebService — ASP.NET Core controllers & models  
- /Typescript, /Javascript, /Angular, /React, /VUE, /Blazor, /MVC — client samples  
- /sql — add schema & seed scripts (recommended)  
- appsettings.json/controller file — connection strings  
- README.md, LICENSE, CONTRIBUTING.md, .github/ templates

---

🔗 API Endpoints (example)
- GET  /localhost/Pivot — fetch data for PivotView

---

🔒 Best Practices & Security
- ✅ Use parameterized queries or ORM (Dapper/EF Core) to prevent SQL injection  
- ✅ Store secrets securely (user-secrets/env vars) — do not commit credentials  
- ✅ Limit CORS origins in production  
- ✅ Validate DataManager inputs server-side  
- ✅ Register Syncfusion license as required

---

🤝 Contributing
- Fork → branch → open PR with description and tests  
- Follow .NET coding conventions and include docs for breaking changes

---

📜 License
- Add a LICENSE file (MIT recommended). Example badge:
```md
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
```

---

🔎 GitHub Metadata & SEO Recommendations
Suggested topics:
```
syncfusion, ej2, pivotview, postgresql, dotnet, aspnet-core, example, demo, dashboard, analytics
```

Suggested short description (<=160 chars):
```
Syncfusion EJ2 PivotView demo — bind PostgreSQL to Pivot Table using ASP.NET Core; includes multi-framework client samples.
```

About sidebar text:
```
Quick-start demos for binding PostgreSQL to Syncfusion PivotView across TypeScript/JS/Angular/React/Vue/.NET/Blazor/MVC. Includes server endpoints and client samples.
```

Suggested hashtags:
```
#Syncfusion #PivotTable #PostgreSQL #DotNet #ASPNetCore #WebDev #Dashboard
```

Suggested badges (examples)
```md
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![.NET](https://img.shields.io/badge/.NET-6.0-brightgreen.svg)](https://dotnet.microsoft.com/)
[![Syncfusion](https://img.shields.io/badge/Syncfusion-EJ2-orange.svg)](https://www.syncfusion.com/)
[![Last Commit](https://img.shields.io/github/last-commit/SyncfusionExamples/web-bind-PostgreSQL-database-to-pivot-table.svg)]()
```

---

✅ SEO Checklist (primary keywords used)
- Primary: Syncfusion PivotView, PostgreSQL, ASP.NET Core  
- Secondary: DataManager, CRUD API, Npgsql, dashboard demo  
- Long-tail examples: "bind PostgreSQL to Syncfusion PivotTable ASP.NET Core", "Syncfusion PivotView DataManager PostgreSQL example"

---

🧾 Suggested .github templates
- Issue: bug_report.md, feature_request.md  
- PR template: PR_TEMPLATE.md  
- CONTRIBUTING.md and CODE_OF_CONDUCT.md (add standard templates)

---

📣 Next steps & Recommendations
- Add LICENSE and SQL schema/seed in /sql  
- Replace inline SQL with parameterized/ORM examples  
- Add GitHub Actions CI and a build/test badge  
- Add a short demo GIF and a sample production checklist

_Last updated: 2026-02-03_
