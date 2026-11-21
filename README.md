# 🧪 DEPI — CAI5_SWD6_S4 | Team 1 Testing Project
### End-to-End API Test Cases & Manual Quality Assurance for [Automation Exercise](https://automationexercise.com)

[![DEPI Project](https://img.shields.io/badge/DEPI-CAI5__SWD6__S4-0284C7?style=for-the-badge&logo=googlecloud&logoColor=white)](https://automationexercise.com)
[![Team](https://img.shields.io/badge/Team-Team%201-16A34A?style=for-the-badge)](https://github.com/Daniel-Lamie95/CAI5_SWD6_S4-DEPI5_Team1)
[![Testing Type](https://img.shields.io/badge/Testing-API%20%26%20Manual-EA580C?style=for-the-badge)](https://automationexercise.com/api_list)
[![Excel](https://img.shields.io/badge/Microsoft%20Excel-Test%20Suites-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)](https://products.office.com/excel)

---

## 📌 Table of Contents
- [📖 Project Overview](#-project-overview)
- [📂 Repository Structure](#-repository-structure)
- [👥 Team Work Breakdown (6 Members)](#-team-work-breakdown-6-members)
- [🌟 Member 1 Spotlight — Products Catalog APIs](#-member-1-spotlight--products-catalog-apis)
  - [Tested Endpoints](#tested-endpoints)
  - [Execution Metrics](#execution-metrics)
  - [Identified Defects Log](#identified-defects-log)
- [📊 Excel Deliverables Overview](#-excel-deliverables-overview)
- [🤝 Collaboration & Git Workflow](#-collaboration--git-workflow)

---

## 📖 Project Overview

This repository contains the comprehensive **Manual and API Testing test suites** developed for the **Digital Egypt Pioneers Initiative (DEPI)** under code **CAI5_SWD6_S4 (Team 1)**.

All test scenarios were designed, validated, and documented in professional **Microsoft Excel Test Trackers** covering:
- **Products Catalog & Directory Management**
- **Search Capabilities & Boundary Validations**
- **User Authentication, Registration, and Profile Management**
- **Security Validations (SQL Injection, Payload Sanitization, HTTP Method Constraints)**

---

## 📂 Repository Structure

```text
CAI5_SWD6_S4-DEPI5_Team1/
│
├── 📁 Api Testing/
│   ├── 📊 API_Test_Cases.xlsx                                           # Master Shared API Test Cases (50 Cases Across Full Team)
│   └── 🐞 API_Bugs.xlsx                                                 # Master Shared API Defect & Bug Reports
│
├── 📁 Manual Testing/
│   ├── 📋 Tests Cases.xlsx                                            # Manual Functional Test Cases
│   └── 🐞 Bug Report.xlsx                                             # Manual Testing Bug Reports
│
├── 📄 Test plan.pdf                                                    # Master QA Test Plan Document
└── 📄 README.md                                                        # Project Documentation (This File)
```

---

## 👥 Team Work Breakdown (6 Members)

| Team Member | Assignee | Assigned Module | Scope & Endpoints | Status |
| :---: | :---: | :---: | :--- | :---: |
| **Member 1** | **Rehab Adel** | **Products Catalog** | `GET /api/productsList`<br>`POST /api/searchProduct`<br>+ Boundary | **✅ Completed** |
| **Member 2** | **Angelina** | **Brands Directory** | `GET /api/brandsList`<br>`PUT /api/brandsList` | **✅ Completed** |
| **Member 3** | **Gerges** | **Product Search** | `POST /api/searchProduct` (Keywords, SQL Injection) | **✅ Completed** |
| **Member 4** | **Daniel Adel** | **User Authentication** | `POST /api/verifyLogin`<br>`DELETE /api/verifyLogin` | **✅ Completed** |
| **Member 5** | **Ziad Omar** | **Registration & Deletion** | `POST /api/createAccount`<br>`DELETE /api/deleteAccount` | **✅ Completed** |
| **Member 6** | **Ahmed** | **Account Updates & Lookup**| `PUT /api/updateAccount`<br>`GET /api/getUserDetailByEmail` | ⏳ Pending |

---

## 🌟 Member 1 Spotlight — Products Catalog APIs

Member 1 holds ownership of the **Products Catalog APIs**, with full coverage across functional, negative, boundary, and security test scenarios.

### Tested Endpoints:
1. **API 1 – Get All Products:** `GET /api/productsList`
2. **API 2 – Search Product:** `POST /api/searchProduct` (Form Parameter: `search_product`)

### Execution Metrics:
* **Member 1 Test Cases in Shared Sheet (`API_Test_Cases.xlsx`):** 29 Comprehensive Test Cases (`TC_14` to `TC_28` and `TC_37` to `TC_50`).
* **Team Total in Shared Sheet (`API_Test_Cases.xlsx`):** 50 Test Cases covering all 6 team members.
* **Execution Status:** 100% Executed against live endpoints (`https://automationexercise.com`).
* **Pass Rate:** 89.7% Verified Passes | 10.3% Real Server Defects Logged.

### Identified Defects Log:

| Defect ID | Severity | Endpoint | Summary & Root Cause | Logged In |
| :---: | :---: | :--- | :--- | :---: |
| **`BUG_API_003`** | **Major** | `POST /api/searchProduct` | **Empty Search Query Leaks Entire Catalog**<br>Sending `search_product=''` returns `responseCode: 200` with all 34 products instead of `400 Bad Request` or empty array `[]`. | `API_Bugs.xlsx` |
| **`BUG_API_004`** | **Minor** | `GET /api/productsList` | **Incorrect Response Content-Type Header**<br>Server returns `Content-Type: text/html; charset=utf-8` despite body being valid JSON. | `API_Bugs.xlsx` |
| **`BUG_API_005`** | **Minor** | Unsupported Methods (`POST /api/productsList`) | **HTTP 200 OK returned on Invalid HTTP Methods**<br>Sending `POST` to `/api/productsList` returns status line `HTTP 200 OK` with `{"responseCode": 405}` in the body instead of standard `HTTP 405 Method Not Allowed`. | `API_Bugs.xlsx` |

---

## 📊 Excel Deliverables Overview

1. **`API_Test_Cases.xlsx`:**
   * Master shared repository sheet containing 50 API test cases across the team.
   * Member 1 test cases fully integrated across 29 test cases (`TC_14` to `TC_28` and `TC_37` to `TC_50`) with all standard columns (`Test ID`, `Test Case Description`, `Pre-Condition`, `Roles`, `Test Data`, `Steps/Actions`, `Expected Result`, `Actual Result`, `Created by`, `Status`, `Priority`, `Type`).
2. **`API_Bugs.xlsx`:**
   * Master shared bug report repository documenting defects discovered during testing.
   * Member 1 defects logged (`BUG_API_003`, `BUG_API_004`, `BUG_API_005`) with steps to reproduce, expected vs actual behavior, severity, and priority alongside team defects.

---

## 🤝 Collaboration & Git Workflow

- **Repository:** `Daniel-Lamie95/CAI5_SWD6_S4-DEPI5_Team1`
- **Active Branch:** `main`
- **Review Strategy:** Peer-reviewed Pull Requests.

---
*Digital Egypt Pioneers Initiative (DEPI) — CAI5_SWD6_S4 Team 1.*

