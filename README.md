<h1 align="center">ACME Generate Yearly Report</h1>

<p align="center">
  <strong>UiPath automation for generating and uploading yearly vendor reports</strong><br>
  Web automation, Excel processing, work item handling and exception management
</p>

<p align="center">
  <img alt="UiPath" src="https://img.shields.io/badge/Automation-UiPath-FA4616?style=for-the-badge">
  <img alt="RPA" src="https://img.shields.io/badge/Type-RPA-2d2d2d?style=for-the-badge">
  <img alt="Excel" src="https://img.shields.io/badge/Output-Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white">
  <img alt="Scope" src="https://img.shields.io/badge/Scope-End--to--End%20Automation-1f6feb?style=for-the-badge">
</p>

<p align="center">
  <strong>Author:</strong> Aris-Georgian ILIE
</p>

---

## TABLE OF CONTENTS

- [ABOUT THE PROJECT](#about-the-project)
- [BUSINESS CONTEXT](#business-context)
- [AUTOMATION OBJECTIVE](#automation-objective)
- [PROCESS OVERVIEW](#process-overview)
- [HOW THE AUTOMATION WORKS](#how-the-automation-works)
- [MAIN COMPONENTS](#main-components)
- [INPUTS AND OUTPUTS](#inputs-and-outputs)
- [EXCEPTION AND ERROR HANDLING](#exception-and-error-handling)
- [APPLICATIONS USED](#applications-used)
- [TECHNICAL APPROACH](#technical-approach)

---

## ABOUT THE PROJECT

<p align="justify">
<strong>ACME Generate Yearly Report</strong> is a UiPath automation designed to process vendor reporting tasks inside the ACME System 1 web application. The robot identifies work items of type <strong>WI4</strong>, retrieves the vendor tax identifier from each task, downloads all available monthly reports for the previous year, consolidates them into a single yearly Excel report, uploads the result back into the system and then updates the original work item with the generated upload ID.
</p>

<p align="justify">
The process belongs to the <strong>Finance and Accounting</strong> department and was selected for automation in order to reduce processing time, improve reliability and eliminate repetitive manual work. The activity is performed yearly, usually in mid-January, for around <strong>7 to 15 vendors</strong>, with an average manual handling time of about <strong>15 minutes per vendor</strong>.
</p>

<p align="justify">
This project is an end-to-end unattended automation scenario. It combines browser automation, data extraction, iterative processing of work items, file download handling, Excel file generation, upload actions and robust exception management. The overall goal is to transform a repetitive reporting process into a structured and reliable digital workflow.
</p>

---

## BUSINESS CONTEXT

<p align="justify">
The business process automated here is called <strong>Generate Yearly Report for Vendor</strong>. Its purpose is to create a yearly Excel report by gathering the monthly reports associated with a specific vendor and the previous calendar year. The robot receives its work from the ACME System 1 platform and completes the task fully inside the scope of the process.
</p>

<p align="justify">
A key business rule is that some monthly reports may be missing. Between <strong>1 and 3 monthly reports</strong> for a vendor can be absent and those missing months must simply be ignored instead of stopping the process. This makes the automation more realistic and requires the workflow to tolerate partial data while still producing a valid yearly output.
</p>

---

## AUTOMATION OBJECTIVE

<p align="justify">
The automation was built to improve the speed and consistency of yearly vendor reporting. Its main objectives are to deliver faster processing, reduce the duration of time-consuming activities and improve the overall performance and reliability of the department through automation.
</p>

<p align="justify">
From a technical point of view, the robot is expected to open the target application, authenticate securely, process all relevant WI4 items, generate correctly named yearly Excel files and return a valid upload ID for each completed case. It must also handle predictable business exceptions and technical issues in a controlled way.
</p>

---

## PROCESS OVERVIEW

<p align="justify">
The process begins by opening the <strong>ACME System 1</strong> web application and logging into the platform with the required credentials. After reaching the dashboard, the robot accesses the <strong>Work Items</strong> list and searches for activities of type <strong>WI4</strong>. For each matching work item, it opens the details page and extracts the <strong>Vendor Tax ID</strong>.
</p>

<p align="justify">
Once the tax ID has been collected, the robot returns to the dashboard and navigates to the <strong>Download Monthly Report</strong> section under the Reports menu. It fills in the vendor tax ID and downloads all available monthly reports for the previous year. The downloaded files are then grouped into a single Excel report using the naming convention <strong>Yearly-Report-[Year]-[Tax ID].xlsx</strong>.
</p>

<p align="justify">
After generating the yearly report file, the robot goes to the <strong>Upload Yearly Report</strong> section, fills in the vendor tax ID and year, selects the generated file and uploads it. The system returns a unique <strong>Upload ID</strong>. The robot then goes back to the original work item, selects <strong>Update Work Item</strong>, sets the status to <strong>Completed</strong> and writes a comment in the format <strong>Uploaded with ID [Upload ID]</strong>. The robot then continues with the next WI4 item until all valid tasks are processed.
</p>

---

## HOW THE AUTOMATION WORKS

<p align="justify">
At runtime, the automation follows a clear sequence of actions. It starts in the browser, performs login, loads the dashboard and uses navigation elements to reach the work item list. This first part is responsible for establishing the application session and identifying the tasks that belong to the yearly reporting workflow.
</p>

<p align="justify">
The second part of the automation is task processing. For each WI4 item, the robot opens the details page, reads the tax ID and uses it as the main input for the reporting actions. The tax ID drives the report download, the yearly file generation and the upload step. In this way, each work item becomes one complete reporting transaction.
</p>

<p align="justify">
The third part is document handling. The robot downloads the monthly files, processes the available data and creates a single Excel output for the entire year. This output file acts as the final deliverable for the vendor. Its standardized naming format helps maintain consistency and traceability.
</p>

<p align="justify">
The last part is closing the loop in the source system. After upload, the robot captures the returned upload ID and records it back into the work item as proof that the yearly report has been successfully submitted. This makes the work item status meaningful both for operational tracking and for audit purposes.
</p>

---

## MAIN COMPONENTS

### 1. Login and application initialization
<p align="justify">
The automation opens ACME System 1 in a web browser and authenticates with the required email and password. Credentials should be stored securely in <strong>Windows Credential Manager</strong> or <strong>UiPath Orchestrator Assets</strong>.
</p>

### 2. Work item discovery
<p align="justify">
After login, the robot navigates to the Work Items listing and scans the available tasks. Only items of type <strong>WI4</strong> are relevant for this process. If no WI4 task exists, the process follows the documented exception handling path.
</p>

### 3. Tax ID extraction
<p align="justify">
For each selected WI4 task, the robot opens the details page and extracts the vendor tax ID. This value becomes the central business input for the download and upload operations.
</p>

### 4. Monthly report download
<p align="justify">
The robot navigates to the Download Monthly Report page, enters the tax ID and requests all monthly reports for the previous year. The workflow must tolerate missing monthly reports and continue processing with the available ones.
</p>

### 5. Yearly Excel generation
<p align="justify">
The downloaded monthly reports are consolidated into one yearly Excel file. The required output naming pattern is <code>Yearly-Report-[Year]-[Tax ID].xlsx</code>, which ensures consistent file naming across vendors and years.
</p>

### 6. Report upload
<p align="justify">
The robot goes to the Upload Yearly Report page, enters the vendor tax ID, selects the year and uploads the generated file. The upload action returns a unique ID that is needed to complete the original work item.
</p>

### 7. Work item completion
<p align="justify">
The final business step is updating the initial task. The robot changes the status to <strong>Completed</strong> and adds the upload ID inside the comments field using the required text pattern. This records the final outcome inside the source application.
</p>

---

## INPUTS AND OUTPUTS

<p align="justify">
The primary input for the process is the <strong>Vendor Tax ID</strong>, retrieved from the WI4 work item details page. The automation uses this identifier to search, download and upload all files related to the vendor.
</p>

<p align="justify">
The main output is the <strong>Yearly Report Excel file</strong>, generated from the available monthly reports. A second important output is the <strong>Upload ID</strong> returned by the system after the yearly report is uploaded. This ID is written back into the work item comments to complete the business transaction.
</p>

---

## EXCEPTION AND ERROR HANDLING

<p align="justify">
The documentation separates exceptions into business and technical categories and provides specific actions for known cases. One documented business exception is <strong>incorrect email or password</strong> at the login step. In this case, the robot should send an email notification explaining that the username or password is incorrect and that the process should be restarted after correction.
</p>

<p align="justify">
Another known business exception is the case where <strong>no WI4 task exists</strong>. For that scenario, the documented action is to stop the process. This prevents unnecessary navigation or invalid processing attempts when there is no work available for the automation.
</p>

<p align="justify">
For unknown or unexpected exceptions, the robot should send an email notification and include the original message and an error screenshot attachment. This gives the support team enough information to investigate failures that were not previously defined in the process map.
</p>

<p align="justify">
On the technical side, a documented error case is <strong>application unresponsive or page not loading</strong>. The expected action is to retry the step up to two times and then close the application and rerun the sequence if the issue persists. This retry-based recovery pattern increases robustness against temporary platform issues.
</p>

---

## APPLICATIONS USED

<p align="justify">
The automation works with two main applications: <strong>ACME System 1</strong> and <strong>Microsoft Excel</strong>. ACME System 1 is used through a web browser and handles work items, downloads and uploads. Microsoft Excel is used locally to consolidate the monthly reports into the final yearly output.
</p>

<p align="justify">
This combination makes the project a good example of cross-application RPA. The robot does not stay inside one system only. It moves between browser-based business tasks and local document processing while preserving the continuity of each case.
</p>

---

## TECHNICAL APPROACH

<p align="justify">
From a development perspective, this project can be understood as a transaction-based UiPath workflow. Each WI4 item behaves like an individual business case with a defined start, processing phase and completion action. This structure makes the automation easier to scale, debug and maintain.
</p>

<p align="justify">
A practical implementation usually includes initialization, login, work item retrieval, transaction processing, Excel consolidation, upload handling and final update steps. It also benefits from clear logging, retry logic, secure credential storage and structured exception handling so that business issues and application failures are treated differently.
</p>

<p align="justify">
Because the process runs yearly and handles multiple vendors in one session, it is also well suited for an unattended robot model.
</p>

---
