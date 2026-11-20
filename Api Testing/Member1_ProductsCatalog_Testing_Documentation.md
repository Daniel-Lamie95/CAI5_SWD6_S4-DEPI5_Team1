# Member 1 – Products Catalog API Testing Documentation & Final Report

**Project:** DEPI – CAI5_SWD6_S4 (Team 1)  
**Assignee:** Rehab Adel (Member 1)  
**Assigned Module:** Products Catalog APIs  
**Base URL:** `https://automationexercise.com`  
**Repository Branch:** `feature/member-1-products-catalog`  
**Target Folder:** `Api Testing/`  

---

## 1. Executive Summary & Scope

This document provides a comprehensive technical walkthrough and executive summary of the API testing, automation, and documentation delivered by **Member 1** for the **Products Catalog** module. All testing activities were executed live against the real Automation Exercise environment (`https://automationexercise.com`).

### Scope of Assigned APIs:
1. **API 1 – Get All Products List**
   * **HTTP Method:** `GET`
   * **Endpoint:** `/api/productsList`
2. **API 2 – Search Product**
   * **HTTP Method:** `POST`
   * **Endpoint:** `/api/searchProduct`
   * **Parameter:** `search_product` (sent as `form-data`)

---

## 2. Test Execution Metrics

* **Total Test Cases Designed:** **29 Test Cases**
* **Executed Test Cases:** **29 Test Cases (100% Execution Rate)**
* **Passed Test Cases:** **26 Test Cases (89.7%)**
* **Failed Test Cases (Defects Logged):** **3 Test Cases (10.3%)**
* **Not Run:** **0 Test Cases**
* **Automated Postman Requests:** **25 Requests** (across 3 structured folders)

---

## 3. Live Testing Findings & API Reality

### Endpoint 1: `GET /api/productsList`
* **Status Code:** Returns `HTTP 200 OK`.
* **Total Products Returned:** Exactly **34 products**.
* **Primary Key Uniqueness:** All product IDs (`1` through `43`) are strictly unique with zero duplicates.
* **Schema Contract:** Every item adheres to required schema: `id` (int), `name` (string), `price` (string), `brand` (string), and `category` (object with nested `usertype` and `category`).
* **Identified Quirk / Defect (DEF-01):** The response header returns `Content-Type: text/html; charset=utf-8` instead of standard `application/json; charset=utf-8`, despite the body containing valid JSON.

### Endpoint 2: `POST /api/searchProduct`
* **Payload Requirement:** The API strictly parses `multipart/form-data` or `application/x-www-form-urlencoded`. Sending `application/json` causes the API to reject the request with `responseCode: 400` (*DEF-04*).
* **Keyword Search (`search_product='top'`):** Returns **14 matching items**.
* **Keyword Search (`search_product='jean'`):** Returns **3 matching items**.
* **Exact Name Match (`search_product='Blue Top'`):** Returns exactly **1 item (ID: 1)**.
* **Case-Insensitivity (`search_product='TSHIRT'`):** Returns **6 matching items**, confirming search is case-insensitive.
* **Non-Matching Search (`search_product='xyz987nomatch'`):** Returns `responseCode: 200` with clean empty array `[]`.
* **Missing Parameter:** Properly rejected with `responseCode: 400` and message `"Bad request, search_product parameter is missing in POST request."`.
* **Empty String Search (`search_product=''`):** **Critical Boundary Failure (DEF-03)**: Rather than returning `400 Bad Request` or empty array `[]`, the server returns `responseCode: 200` and dumps all **34 products** in the database.
* **Whitespace-Only Search (`search_product='   '`):** Treated as literal search; returns empty array `[]` safely.
* **Special Characters & SQL Injection (`"' OR '1'='1"`):** Parameterized properly; returns empty array `[]` without leaking data.
* **Long String (500 characters):** Handled safely without 500 server crash.

---

## 4. Defects & Architectural Quirks Log

| Defect ID | Severity | Endpoint | Description & Actual Behavior | Expected REST Behavior |
| :---: | :---: | :--- | :--- | :--- |
| **DEF-01** | Medium | `GET /api/productsList` | Header returns `Content-Type: text/html; charset=utf-8`. | Header should be `Content-Type: application/json`. |
| **DEF-02** | Low | Unsupported Methods | Returning HTTP `200 OK` on invalid HTTP methods (e.g. POST on productsList), with `responseCode: 405` inside JSON body. | Should return standard `HTTP 405 Method Not Allowed`. |
| **DEF-03** | High | `POST /api/searchProduct` | Empty parameter `search_product=''` dumps entire catalog (34 items) with code 200. | Should validate input and return `400 Bad Request` or empty array `[]`. |
| **DEF-04** | Low | `POST /api/searchProduct` | Rejects `application/json` payload with 400 parameter missing. | Modern APIs should parse JSON search bodies. |

---

## 5. Overview of Deliverable Files

### File 1: Excel Test Tracker
* **Filename:** `AutomationExercise_API_Testing_Team_Breakdown_Updated.xlsx`
* **Location:** `Api Testing/`
* **Typography:** `Calibri` (aligned 100% with DEPI team standard).
* **Palette:** Slate Dark Navy `#1E293B`, White Headers, Soft Green PASS, Soft Red FAIL.
* **Sheets Included:**
  1. `Execution Summary`: Executive dashboard with KPI metric cards, endpoint breakdowns, and Defect Log.
  2. `Team Work Breakdown`: Preserved entire 6-member team data; updated Member 1 Assignee to `Rehab Adel` with `Completed` status.
  3. `Member 1 - Products Catalog`: 29 detailed test cases formatted with the 16 mandatory columns, filters, freeze panes, text wrap, and color-coded status.
  4. `Test Case Tracker`: Team tracking sheet with Member 1's entries updated with live execution evidence and dynamic formulas.

### File 2: Postman Collection
* **Filename:** `Member1_ProductsCatalog_Postman_Collection.json`
* **Location:** `Api Testing/`
* **Postman Schema:** `https://schema.getpostman.com/json/collection/v2.1.0/collection.json` (v2.1.0)
* **Collection Variable:** `baseUrl` = `https://automationexercise.com`
* **Folders & Automated Requests (25 Requests Total):**
  * `Folder 1: API 1 – Products List` (7 requests): Status code, JSON parsing, products array count, field schemas, ID uniqueness, reference product integrity, unsupported method test.
  * `Folder 2: API 2 – Search Product` (7 requests): Keyword searches, exact match, case insensitivity, schema validation in search results, no-match scenario, missing parameter negative test.
  * `Folder 3: Boundary Value Testing` (11 requests): Empty query, whitespace query, single character (alpha & numeric), long input (500 chars), special characters, SQL injection security test, raw JSON body rejection test, and unsupported HTTP methods (GET, PUT, DELETE).

---

## 6. Git & GitHub Branch Information

* **Working Branch:** `feature/member-1-products-catalog`
* **User Remote Fork:** `https://github.com/Rehab2905/CAI5_SWD6_S4-DEPI5_Team1`
* **Upstream Target:** `https://github.com/Daniel-Lamie95/CAI5_SWD6_S4-DEPI5_Team1`
* **Pull Request Compare Link:** [Open PR to Daniel's main branch](https://github.com/Daniel-Lamie95/CAI5_SWD6_S4-DEPI5_Team1/compare/main...Rehab2905:CAI5_SWD6_S4-DEPI5_Team1:feature/member-1-products-catalog?expand=1)
