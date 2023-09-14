---
title: ???
description: ???
canonical: /migrations/update-database
status: Unpublished
lastmod: 2023-09-01
---

# EF Core Update-Database

Updating a database using a migration in EF Core is the process of applying changes to a database using the `Up` method from the [migration file](/migrations/migration-files#up-method) or reverting changes using the `Down` method. To apply or unapply a migration, the `Update Command` must be run. This command checks the database for all applied migrations and will execute one of the two following processes:

- **Apply a migration**: The [Up Method](/migrations/migration-files#up-method) will be executed if the specific migration is more recent than the latest applied migrations.
- **Revert a migration**: The [Down Method](/migrations/migration-files#up-method) will be executed if the specific migration is older than the latest applied migrations.

There are 2 ways to run the `Update Database` command and both will be covered in this article:

- `Update-Database`: When using the Package Manager Console (PMC)
- `dotnet ef database update`: When using the .NET Command Line Interface (.NET CLI)

<img src="/images/efcore/migrations/update-database/thumbnail-ef-core-update-database.png" loading="lazy" alt="EF Core Update Database">

The `Update Database` command is one of the 3 main migration commands:

- [Add Migration](/migrations/add-migration)
- [Update Database](/migrations/update-database)
- [Remove Migration](/migrations/remove-migration)

## How to use the Update-Database command with PMC in EF Core?

To use the `Update-Database` command with the Package Manager Console (PMC) in EF Core:

1. Open the [Package Manager Console](/migrations/commands/pmc-commands) in Visual Studio.
2. Ensure the default project in the console is the one containing your EF Core DbContext.
3. Enter the following command:

```
Update-Database
```

For applying a specific migration or reverting to a previous migration, you must specify the migration name:

```
Update-Database [MigrationName]
```

:::{.alert .alert-info}
**NOTE**: Replace `[MigrationName]` with the name of the migration you want to apply or revert to.
:::

<img src="/images/efcore/migrations/update-database/how-to-use-update-database-command-with-pmc-in-ef-core.png" loading="lazy" alt="Update Database - PMC Example">

## How to use the Update-Database command with .NET CLI in EF Core?

To use the `dotnet ef database update` command with the .NET Command Line Interface (.NET CLI) in EF Core:

1. Open a [command prompt or terminal](/migrations/commands/cli-commands).
2. Navigate to the directory containing your context.
3. Run the following command:
```
dotnet ef database update
```

For targeting a specific migration or reverting to a previous migration, you can use:

```
dotnet ef database update [MigrationName]
```

:::{.alert .alert-info}
**NOTE**: Replace `[MigrationName]` with the name of the migration you want to apply or revert to.
:::

See [Command Line Parameters](#net-command-line-interface.net-cli) for additional parameters options.

<img src="/images/efcore/migrations/update-database/how-to-use-update-database-command-with-net-cli-in-ef-core.png" loading="lazy" alt="Update Database - CLI Example">

## What does the Update-Database command do in EF Core?

When you use the `Update-Database` command with PMC or `dotnet ef database update` with .NET CLI, both utilize EF Core Tools to perform several tasks:

1. First, EF Core Tools fetch all migrations that have been applied to your database.
2. Then, EF Core Tools determine whether a migration should be applied or reverted.
   a. If the database needs to be updated to a more recent migration, the `Up Method` for each migration since the last one applied will be run.
   b. If the database needs to be reverted to a previous migration, the `Down Method` for each migration up to the specified migration will be run.

<img src="/images/efcore/migrations/update-database/what-does-the-update-database-command-do-in-ef-core.png" loading="lazy" alt="Update Database Tasks">

## What are the parameters for the Update Database command in EF Core?

#### Package Manager Console (PMC)

The `Update-Database` command with PMC provides several optional options:

| Option | Description |
| ------ | ----------- |
| **-Name** | The name of the migration you wish to apply. If not specified, the most recent migration will be used. For example, `Update-Database AddingEFExtensions` will apply all unapplied migrations up to the one named **AddingEFExtensions**. In the case of a rollback, `Update-Database AddingEFExtensions` will revert all applied migration down to the one named **AddingEFExtensions**.  |
| **-Context** | The context class to use that contains the migration you want to apply, it can be either the `name` or the `fullname` including namespaces. For example, `Update-Database -Context Z.MyContextName` will apply the migration for the **Z.MyContextName** context. |
| **-Project** | The project containing the context used to apply the migration file. If omitted, the default project in the Package Manager Console is used. For example, `Update-Database -Project Z.MyProjectName` will apply the migration for the context in the **Z.MyProjectName** project. |
| **-StartupProject** | The project with the configurations and settings. If omitted, the startup project of your solution is used. For example, `Update-Database -StartupProject Z.MyStartupProjectName` will apply the migration using the configurations and settings of the **Z.MyStartupProjectName** project. |

:::{.alert .alert-info}
**NOTE**: The `-Project` option specifies which project contains the [context](/dbcontext), while the `-StartupProject` option indicates the project that has the application's configurations and settings.
:::

#### .NET Command Line Interface (.NET CLI)

For those working outside of Visual Studio or preferring the command line, EF Core offers similar functionality with a slightly different syntax:

| Option | Short |  Description |
| ------ | ----- |  ----------- |
| **[TargetMigration]** | | The target migration. If omitted, it will apply all pending migrations. |  
| **--context** | **-c** | Specifies the DbContext to use. |  
| **--project** | **-p** | The project that contains the migrations to be applied. |  
| **--startup-project** | **-s** | The project that contains the configurations and settings. |

```csharp
dotnet ef database update [TargetMigration] -c MyContext -p MigrationsProject -s StartupProject
```

:::{.alert .alert-info

--
System.InvalidOperationException: The ConnectionString property has not been initialized.
--