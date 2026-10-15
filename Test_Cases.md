# Formal Software Testing & Verification Matrix
## Project: E-Commerce Customer Support & Ticket Management System Using Salesforce

**Author:** Mihira Baklikar  
**Subject:** Cloud Computing Semester Project  
**Platform:** Salesforce Service Cloud & Twilio CPaaS  

---

### Test Summary
- **Total Test Cases Executed:** 10
- **Passed:** 10
- **Failed:** 0
- **Pass Rate:** 100%

---

| Test Case ID | Test Module | Test Scenario | Test Input / Steps | Expected Result | Actual Result | Status |
|:---|:---|:---|:---|:---|:---|:---:|
| **TC-01** | Web-to-Case | Required Field Validation on Complaint Form | Attempt to submit `complaint_form.html` with empty Name and Order ID fields. | HTML5 form validation intercepts submission; highlights missing fields with warning tooltip. | Client-side validation intercepted submit event; form was blocked until inputs supplied. | **PASS** |
| **TC-02** | Web-to-Case | Successful Complaint Submission & Ingestion | Fill valid customer details: Name, Email, Mobile (`9322926898`), Order ID (`ORD-999`), Category (`Damaged Product`). Click Submit. | Payload is POSTed to Salesforce servlet; redirected to configured return URL (`retURL`). | Successfully submitted; redirected to return URL without network faults. | **PASS** |
| **TC-03** | Service Cloud CRM | Case Record Creation in Multi-tenant Database | Inspect Cases view in Salesforce Service Console (`All Open Cases`). | New Case record appears with auto-incremented Case Number (`00001029`). | Case record successfully created with unique system identifier. | **PASS** |
| **TC-04** | Custom Fields | Custom Schema Mapping Verification | Open newly generated Case record and review custom field values. | Custom fields (`Order_ID__c`, `Complaint_Category__c`, `Customer_Mobile__c`) accurately reflect submitted values. | All custom fields mapped accurately from hidden and visible form inputs. | **PASS** |
| **TC-05** | Flow Automation | Record-Triggered Flow Execution | Case record committed with origin `'Web'`. | Salesforce Flow Builder catches record insert event and executes configured downstream actions. | Flow engine executed immediately on commit; audit trail logged in Flow Explorer. | **PASS** |
| **TC-06** | Integration Engine | Asynchronous Apex REST Callout | Flow passes Case ID collection to `TwilioSMSNotification.cls`. | Invocable method schedules `@future(callout=true)` thread; signs HTTP POST request with Basic Auth. | Callout executed asynchronously without blocking database transaction thread. | **PASS** |
| **TC-07** | Twilio CPaaS | SMS Gateway Authorization & Dispatch | Twilio receives HTTPS POST to `/2010-04-01/Accounts/.../Messages.json`. | Twilio authenticates Account SID and Auth Token, maps approved template, returns HTTP 201 Created. | Twilio processed request and dispatched SMS payload to GSM carrier. | **PASS** |
| **TC-08** | End-User Hardware | Real Mobile SMS Reception | Monitor physical mobile phone (`+919322926898`). | Real SMS received on mobile device via telecom network within 15 seconds. | Real SMS received on phone at 6:16 PM from Twilio virtual number. | **PASS** |
| **TC-09** | Business Intelligence | Real-Time Report Data Aggregation | Navigate to Reports: `Tickets by Status`, `Tickets by Complaint Category`. | Reports aggregate and display newly inserted cases according to grouping criteria. | Reports automatically reflected new case volume without manual refresh. | **PASS** |
| **TC-10** | Analytics Dashboard | Interactive Visual Dashboard Component Updates | Open `Customer Support & Operations Dashboard`. | Donut, Bar, Column, and Metric widgets visualize live case distributions. | All 4 charts updated with accurate proportions and case counters. | **PASS** |

---

### Verification Sign-off
- **Developer & Tester:** Mihira Baklikar
- **Evaluation Status:** Verified & Ready for Academic Demonstration
