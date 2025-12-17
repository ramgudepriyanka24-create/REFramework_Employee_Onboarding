This project is an Employee Onboarding Automation built using UiPath Robotic Enterprise Framework (REFramework).

The automation:

Fetches employee data from a public REST API

Adds employees into an Orchestrator Queue with priority based on salary

Processes only High-Priority employees

Submits employee details on a web form

Generates and stores QR codes

Creates an Excel report

Zips QR codes

Sends a summary email at the end

The solution follows UiPath best practices, including:

Queue-based transaction processing

Robust logging

Exception handling

Retry mechanism

🛠️ Technology Stack

UiPath Studio

REFramework

UiPath Orchestrator

REST API (HTTP Request)

Excel Automation

Web Automation

Email Automation

🗂️ Project Structure
Employee_Onboarding_REFramework
│
├── Main.xaml
├── InitAllSettings.xaml
├── GetTransactionData.xaml
├── Process.xaml
├── EndProcess.xaml
├── SetTransactionStatus.xaml
├── Config.xlsx
│
├── QRCodes
│   └── (Generated QR Images)
│
└── Output
    ├── Onboarding_Report_yyyyMMdd.xlsx
    └── QRCodes.zip

⚙️ Pre-Requisites
1. Orchestrator Setup

Create a Queue named: New Hires

Queue Type: Default

Ensure the robot has access permissions

2. Local Folders

Create the following folders in the project root:

QRCodes
Output

3. Required UiPath Packages

Ensure the following packages are installed:

UiPath.System.Activities

UiPath.Web.Activities

UiPath.Excel.Activities

UiPath.Mail.Activities

UiPath.Core.Activities

🔁 Business Logic
Employee Priority Rules
Salary Range	Queue Priority
> 300,000	High
100,000 – 300,000	Normal
< 100,000	Low

👉 Only High-Priority employees are processed.

🚀 Workflow Explanation
🔹 InitAllSettings.xaml

Calls Employee API

Parses JSON response

Determines priority based on salary

Adds employees to New Hires Queue

Logs all queue additions

🔹 GetTransactionData.xaml

Fetches next transaction from Orchestrator Queue

Orchestrator automatically picks High Priority first

🔹 Process.xaml

For each transaction:

Reads employee details from Queue Item

Skips Normal & Low priority employees

Splits employee name into First & Last name

Submits data to web form (rpachallenge.com)

Generates QR Code

Saves QR image to QRCodes folder

Stores details in an in-memory DataTable

Logs success or failure

🔹 EndProcess.xaml

Writes processed employees to Excel report

Zips all QR code images

Sends email with:

Excel report

QR codes ZIP

Logs completion summary
