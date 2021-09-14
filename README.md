# action-generate-migrations-script
An action that can be used to generate an SQL script from the [Entity Framework Core](https://docs.microsoft.com/en-us/ef/core/) DbContexts and Migrations contained inside a .NET Core project.
The Generated script is idempotent, meaning that it won't have any undesired effect if run multiple times.

## Usage
Running this action requires the build for the specified `build-configuration` to be already up to date. Therefore, you can use [EasyDesk/action-dotnet-build](https://github.com/EasyDesk/action-dotnet-build) to make it available.

### Usage example
```yaml
    steps:
      - uses: EasyDesk/action-generate-migrations-script@v1
        with:
          # (Required) The path to the startup project.
          project-dir: '<your-project-dir>'

          # (Required) The name of the generated SQL output file.
          output-file: migrate.sql

          # (Optional) The version of the EF Core tools.
          # If not specified, defaults to the latest version.
          ef-core-version: 5.0.9

          # (Optional) The build configuration.
          # If not specified, defaults to 'Release'.
          build-configuration: Release

          # (Optional) A whitespace separated list of the DbContexts to include.
          # If not specified, the action will auto-detect all the DbContexts available in the project.
          db-context-list: |
            DbContext1
            DbContext2
```