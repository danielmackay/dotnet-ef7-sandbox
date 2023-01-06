# Entity Framework Sandbox

The Entity Framework Sandbox is a CLI project template that allows you to quickly spin up a functioning project running on the latest version of EF with a real database and real data.

This can be useful in the following scenario:

- Exploring new features of EF such as
- Safely exploring changes to a real application
- Replicating EF issues in an isolated environment

> This is not intended to be a starting point for a production application.

## Prerequisites

- VS2022
- .NET 7
- LocalDB

## Setup

### Template Installation

Install the dotnet CLI template via:

```ps1
dotnet new --install EntityFrameworkSandbox.Template 
```

### Project Creation

You can use the template to create a new project via:

```ps1
mkdir my-ef-sandbox
cd my-ef-sandbox
dotnet new ef-sandbox
```

Alternatively, you can create the project directly into a new sub-folder via:

```ps1
dotnet new ef-sandbox --name my-sub-folder
```

## Usage

### Writing Commands & Queries

- Ensure the connection matches if you are using something other than local DB
- Update the `Sandbox` to run your own EF queries and commands

```csharp
private async Task RunQueries()
{
    // NOTE: Further DB queries go here
}
```

```csharp
private Task RunCommands()
{
    // NOTE: Further DB commands go here
}
```

### Overriding Model Configuarion

This can be done in the configuration classes:

```csharp
internal class PostConfiguration : IEntityTypeConfiguration<Post>
{
    public void Configure(EntityTypeBuilder<Post> builder)
    {
        // NOTE: Custom model configuration goes here
    }
}
```

### Schema Changes

The project is designed to use migrations for schema upgrades.  However, if you prefer to instead drop and create the DB everytime you can set `Application.EnableMigrations` to `false` in `appsettings.json`:

```json
"Application": {
    "EnableMigrations": false
}
```

### Run the Project

- Press F5
  - Console up will start
  - By default, DB will be dropped & re-created
  - Data will be seeded
  - SQL queries will run
  - All SQL and results output to console
  
### Updated Nuget Version

A new package will be pushed to Nuget anytime `EntityFrameworkSandbox.Template.nuspec` is changed on `main` branch.  Normally this will happen via a package verison change.
