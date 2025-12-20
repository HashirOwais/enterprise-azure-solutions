# Project: Automated Monthly Expense Report

## 1. Project Overview
**Objective:** To build a reliable, serverless function that automatically generates and emails a monthly expense report. This project serves as a practical, industry-standard learning path for the AZ-204 certification, focusing on time-triggered functions and integrations.
**Target Audience:** Developers preparing for AZ-204, Engineers learning serverless with .NET.
**Tech Stack:** .NET 10, Azure Functions (`TimerTrigger`), Azure SQL (local SQL Server for dev), Entity Framework Core, SendGrid (for email).

## 2. Architecture: Scheduled Batch Job
*   **Trigger (`GenerateExpenseReport`):** A time-triggered function that runs on a schedule (e.g., the first day of every month). It uses a CRON expression for scheduling.
*   **Data Integration (Entity Framework Core):** The function connects to the application's database to retrieve expense data from the past month.
*   **Business Logic:** The core logic aggregates the expenses, calculates totals, and formats a simple report (e.g., as an HTML string).
*   **Email Dispatch (SendGrid):** The function uses an output binding or an SDK to send the formatted report via email to a designated administrator.
*   **Data Store (SQL Server):** A relational database for storing expense information. We will use a local SQL Server instance (via Docker) for development and Azure SQL in production.

## 3. Learning & Implementation Roadmap

### Phase 1: Local Environment & Project Setup
- [ ] **Verify Prerequisites:**
    - [ ] .NET 10 SDK
    - [ ] Azure Functions Core Tools
    - [ ] Docker Desktop
- [ ] **Initialize Project:**
    - [ ] Create a new .NET Solution (`.sln`) to house the shared projects.
    - [ ] Create a shared Class Library for data models and DbContext.
    - [ ] Create a new Azure Functions project (`func init`) within the solution.
- [ ] **Set up Local Database:**
    - [ ] Pull and run the official Microsoft SQL Server Docker image.
    - [ ] Connect to the local database instance and create a database.
- [ ] **Configure Local Settings:**
    - [ ] Add the SQL connection string and SendGrid API key to `local.settings.json`.

### Phase 2: Data Model & Database Integration
- [ ] **Define Data Model:**
    - [ ] Create a C# class `Expense` in the shared class library.
- [ ] **Set up Entity Framework Core:**
    - [ ] Add EF Core NuGet packages to the shared library and the Functions project.
    - [ ] Create a `DbContext` class in the shared library.
    - [ ] Use EF Core Migrations to generate the database schema from the `Expense` model.

### Phase 3: Function Implementation & Testing
- [ ] **Implement `GenerateExpenseReport` (Timer Trigger):**
    - [ ] Create the function with a CRON expression for a monthly schedule.
    - [ ] Use EF Core to query the database for the previous month's expenses.
    - [ ] Implement logic to aggregate data and format an HTML report.
    - [ ] Integrate the SendGrid SDK to email the report.
- [ ] **Local Testing:**
    - [ ] Temporarily adjust the CRON expression for frequent execution (e.g., every 5 minutes) to test the trigger.
    - [ ] Manually run the function to verify the data flow, report generation, and email dispatch.

### Phase 4: Deployment to Azure (Future Scope)
- [ ] Provision Azure Resources (Resource Group, Function App, Azure SQL, etc.).
- [ ] Configure the CRON schedule and application settings in Azure.
- [ ] Publish the Function App to Azure.
- [ ] Test the deployed application.