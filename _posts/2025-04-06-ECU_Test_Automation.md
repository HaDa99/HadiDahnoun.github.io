---
layout: post
title: "Test Automation for ECU Software and Its Migration to the Cloud"
date: 2025-04-06
tags: [Test Automation]
---

*Project report, status as of April 6, 2025. Original title: "Testautomatisierung für Steuergerätesoftware und deren Migration in die Cloud".*

**Language:** English translation below · [Original in German (PDF)]({{ '/assets/pdfs/Testautomatisierung_Steuergeraetesoftware_Cloud_Dahnoun.pdf' | relative_url }}) — figures not shown here are in the original PDF.

---

## 1 Introduction

### 1.1 Context and background

> "Electronic control units (ECUs) are the backbone of any automotive system" (Ravi Aravind, 2024)

The automotive industry is going through a unique transformation driven by software and electrification. ECUs are at the heart of modern vehicles and are constantly improved to meet more demanding requirements with higher reliability. Ensuring software quality through good test procedures is therefore essential. In the past, these tests were largely manual, which is time-consuming and error-prone. Test automation techniques and tools have opened up new ways to address these challenges and increase efficiency drastically. Moving test processes to the cloud is a further step: it optimizes test procedures, uses resources more efficiently and makes test environments scalable. It also brings better connectivity, easier maintenance and efficient management and evaluation of complex test data.

This report discusses the nature of automotive software together with the type of testing it needs, leading up to a test automation solution and its challenges.

### 1.2 Goal and motivation

The main goal is to develop an efficient test automation solution for ECU software that increases test depth and shortens test duration. The report also looks at migrating these processes to the cloud and analyses the resulting challenges and benefits. This leads to two research questions:

- **Does test automation improve efficiency and reliability?** The analysis covers how far the automation improves not only test execution but also defect detection and the documentation of results.
- **Would a cloud migration be possible for this process?** Moving test automation to the cloud offers several benefits:
  1. **Scalability and flexibility:** compute can be scaled quickly on demand, which matters for test scenarios with large data volumes or high compute needs. NVIDIA, for example, highlights that this lets autonomous vehicles be trained, tested and validated at scale without having to encounter rare and dangerous scenarios on real roads.
  2. **Cloud-native AI/ML tools:** data collected by the test tool can be analysed automatically in the cloud with machine learning models to detect patterns, predict failures or spot anomalies in vehicle behaviour. This kind of analysis is often impractical on a local machine; cloud platforms, with their compute and specialised services, are well suited to offering AI/ML as SaaS.
  3. **Better collaboration and workflow integration:** cloud platforms support automation environments for continuous testing, integration and delivery, so test instances and diagnostic functions stay current and can be iterated quickly. Local setups often lack the infrastructure for such agile practices. Tilley & Parveen (2012, pp. 25–26) stress that cloud-based test environments are ideal for automated tests and fast delivery because they can run many test cases in less time.

The report examines the technical challenges of introducing cloud technology into existing test structures, and ways to solve them, after first looking at when it makes sense to bring testing into the cloud.

## 2 Fundamentals and technologies

### 2.1 Automotive software testing

**Ethernet-based automotive architectures.** These have become more important because of the growing need for high-bandwidth communication for features such as over-the-air (OTA) updates, vehicle-to-everything (V2X) communication and ADAS. Ethernet provides scalable communication for real-time and high-performance applications. Traditional architectures based on CAN or FlexRay are limited in data rate and scalability, while Ethernet offers higher throughput and supports more ECUs in a decentralised setup. Typically, a central ECU communicates with several subsystem ECUs over a high-speed Ethernet network.

**AUTOSAR** (AUTomotive Open System ARchitecture) further standardised software development for these systems. It separates application software from hardware through a Runtime Environment (RTE) that abstracts hardware details and lets software components be reused across vehicle models and integrated from different suppliers.

**The ISO OSI model** (Figure 1 in the original, based on ISO 21111-1:2020) describes seven layers of network functions. For diagnosing ECUs that communicate over Ethernet, the top three matter: the session layer (manages sessions between applications), the presentation layer (translates data between the application and network formats) and the application layer (provides network services directly to user applications).

**ISO 14229-1, Unified Diagnostic Services (UDS)**, sits in the application layer. It provides diagnostic services and communication in a standardised format that diagnostic tools use to talk to vehicle ECUs. Key aspects it covers:

1. **Session control:** manages diagnostic sessions (default, programming, extended), each with specific permissions and functions.
2. **Security access:** restricts access to diagnostic services to protect vehicle systems.
3. **Communication control:** manages communication settings between the ECUs and the tester, such as message rate and type of communication.
4. **Routine control:** starts, controls and monitors diagnostic routines implemented in ECUs, e.g. for testing or recalibration.
5. **Request download/upload:** transfers data to and from the ECU, typically for reprogramming or updating calibration data.

**Testing in Ethernet-based architectures** covers several levels of integration because of the risk of system failure (test pyramid, Figure 2 in the original, based on Aniche, 2022):

1. **ECU-level testing (unit tests):** the software of a single ECU is tested in isolation, often with hardware-in-the-loop (HiL) simulation, to make sure each control function works before it joins the vehicle network.
2. **Integration testing:** verifies smooth communication between the central ECU and peripheral ECUs across the network, including timing, data synchronisation and compatibility. This is crucial for safety systems such as ADAS (Dajsuren, 2019, pp. 69–70).
3. **System-level testing (function tests):** evaluates the vehicle in real or simulated driving scenarios under various loads; for Ethernet systems, this includes fault tolerance and real-time data exchange following standards such as IEEE 802.1 Time-Sensitive Networking (TSN).
4. **End-to-end testing and safety:** at the top of the pyramid are manual or more specific tests. Because many systems are safety-critical, compliance with ISO 26262 (functional safety) is essential, especially for features such as automatic emergency braking and lane keeping. The network must be stress-tested under several failure scenarios (Dajsuren, 2019, pp. 234–235).

### 2.2 Introduction to the cloud

Cloud computing lets a shared pool of resources (servers, storage, networks, applications) be provisioned and scaled quickly on demand, which makes it a good platform for demanding test environments. It is usually divided into three service models:

1. **IaaS:** virtualised compute, storage and networks over the internet (e.g. AWS, Microsoft Azure).
2. **PaaS:** a platform to build, deploy and manage applications without handling infrastructure (e.g. Google App Engine, Azure PaaS).
3. **SaaS:** applications delivered over the internet and used in the browser (e.g. Google Workspace, Microsoft 365).

Deployment models are **public cloud** (owned and run by a third party, available to everyone, scalable and cost-efficient), **private cloud** (used by a single organisation) and **hybrid cloud** (a combination of both) (NIST, 2011).

### 2.3 State of the art in test automation

Test automation is at the core of modern test strategies, not just an extra phase. Companies use advanced tools to test millions of lines of code across subsystems, verify safety compliance and reproduce real-world events, shortening time to market while ensuring quality and removing human error.

**HiL and SiL testing** evaluate systems and ECUs virtually before they go into a vehicle:

- **dSPACE HiL platforms** model vehicle environments in real time so ECUs and other hardware can be validated before vehicle integration.
- **Vector CANoe** supports modelling and testing of vehicle networks and ECUs across the development lifecycle and automates test processes from integration to validation.
- **Applied Intuition with Porsche** offers end-to-end software validation covering SiL and HiL, enabling realistic replication and testing of complex scenarios such as autonomous driving.

**Automation for ECU and system validation:**

- **ECU-TEST (tracetronic)** automates test types from unit tests to full system validation, supports generic test cases, works with CANoe, dSPACE and National Instruments hardware in HiL, SiL and MiL setups, and offers data processing for large test datasets.
- **EXAM (MicroNova)** provides standardised test automation with a graphical environment for test case creation, supports HiL, SiL and test bench automation, and lets test cases be reused across projects.

**Test management tools:**

- **IBM DOORS:** requirements management with traceability from requirements to test cases, widely used in automotive.
- **Codebeamer:** manages requirements, tests and compliance with traceability and tool integrations.
- **Jenkins:** continuous integration, automated test execution and real-time feedback on code quality.
- **TestGuide (tracetronic):** test management and reporting integrated with ECU-TEST, with dashboards, progress tracking and central access to test triggers, data and results.

## 3 Project-specific analysis

### 3.1 Process hierarchy

The core process and the test instances in the project are presented first, with a process hierarchy diagram highlighting the sub-processes to automate. The diagram focuses on software testing and quality assurance within the software validation department.

![Process hierarchy with the main automation area highlighted]({{ '/assets/img/test-automation/process-hierarchy.png' | relative_url }})
*Figure 3: Process hierarchy (in German). The green frame marks the main automation area.*

It has four levels:

- **Core processes:** the team's primary functions, such as software analysis and testing.
- **Sub-processes (testing):**
  - *Test planning:* a detailed plan based on project requirements and customer specifications, defining which tests are needed, which resources, and the schedule.
  - *Receiving the software from the supplier and deploying it to the platform:* the supplier's software is uploaded to a platform for testing, here an HiL test bench or the ECU under test on its own.
  - *Software testing:* the core, where functional, integration, system and other tests are run to find defects.
  - *Defect management:* defects are documented, analysed and fixed, including communication with suppliers and tracking until closure.
- **Process steps for software testing and defect management:** software diagnosis, ECU coding, checking function data sets, checking the fault memory and functionality, and recording traces; then creating defect reports, tracking tickets in the group problem management tool (KPM) and aligning with suppliers.
- **Work steps:** concrete actions, e.g. running test procedures with various testing tools, and agreeing priorities and fix dates with suppliers so that defects are not caused by the own test bench.

The main automation area is **software testing**, the largest part of the process, where the extensive quality and performance tests take place. Automation could later be extended to other areas such as defect management.

### 3.2 The test instances

#### 3.2.1 Testing tools

- Rest-bus simulation and measurements/recordings: CANoe
- Documentation and data storage: Confluence, SharePoint, Excel
- Test requirements and test cases: DOORS
- Diagnostic tools: OBD tools, CANoe
- Software version management: System42

#### 3.2.2 Test setup

The test bench is a rest-bus simulation with two real components: the ECU under test (ECU1) and a real gateway. The connectors of the other ECUs in the topology are wired to a Vector box connected to a measurement PC, which simulates the required nodes so the test environment is as realistic as possible.

![Test bench setup with Vector box, ECU1 and gateway ECU]({{ '/assets/img/test-automation/test-setup.png' | relative_url }})
*Figure: Test setup*

#### 3.2.3 Test specification

Test cases run on the bench (partly based on ISO 14229-1, see Section 2.1):

| Category | No. | Test case |
|---|---|---|
| Diagnostic requests | 1–5 | ECU hard reset, ECU key off/on reset, ECU soft reset, programming session, extended session, … |
| Identification | 7–12 | Read SW version number, HW number, series number, system name; check diagnosis variant; identification of all data sets |
| DTC | 13–17 | Clear/reset DTC info, read DTC info, read active errors, read passive errors, erase passive errors |
| Flashing | 18–21 | Flash via OBD tool, flash via DoIP Ethernet, check flash logging, flash via OTA update |
| Data sets | 22–27 | Write data sets, data sets defined and given, data set coding/plausibility check |
| Sleep and wake-up | 29–43 | Transport wake-up mode, wake-up through function shutdown, CAN wake-up, transport sleep mode, sleep via function request, UDS sleep, sleep at clamp 15 off, sleep at clamp 30 off, CAN sleep |

The test cases verify the ECU's functions: reading and identifying software and hardware data, capturing diagnostic trouble codes (DTCs), performing resets (hard, soft, key off/on), working correctly in different diagnostic modes, managing sleep and wake-up modes, checking that data sets are correct and plausible, and performing software updates via OBD tool, Ethernet or OTA. The goal is that the ECU works flawlessly in every vehicle scenario.

These are mostly integration and function tests. Integration tests check that the ECU connects and communicates properly with other parts of the system; function tests confirm that it performs its core functions (diagnostics, resets, data transfer, applicability of data sets) correctly under various conditions.

Depending on the manufacturer's offer configuration, many different data sets can be tested on an ECU. Traffic sign recognition is one example: vehicles are built for different countries with different traffic signs, so vehicles for China have different data sets from those for Germany. Automation can cover all possible combinations, which widens test scope and increases test depth.

## 4 The test automation solution

The goal is to increase test depth, i.e. to test a relatively large number of scenarios or data set combinations, while shortening the test cycle.

The implementation had to fit the customer's requirements, in particular the customer-specific OBD tool, which has no API for easy automation. The solution was therefore a **GUI-based automation** for the test team that automates ECU coding for any number of vehicle combinations. The tool also reads measured values, runs diagnostic tasks (as in 3.2.3) and creates a time-stamped test report with all relevant results. A **COM API automation in CANoe** was added to cover the customer's full test scope: it manipulates signals in the rest-bus simulation and reads traces that the OBD tool alone cannot provide. Combining both approaches, CANoe for direct manipulation of communication signals and GUI automation for controlling the OBD tool, created the overall solution.

### 4.1 Implementation

The OBD tool automation combines OCR, PyAutoGUI and other libraries:

1. **OCR with the Google Cloud Vision API.** OCR recognises text in screenshots taken during the test, such as messages shown by the OBD tool. If an error like "comm. module not connected" appears, the system detects it and triggers error handling.
   - *Screenshots:* the tool captures the application window with PyAutoGUI and stores the images temporarily for text recognition.
   - *Text recognition:* the screenshots are sent to the Vision API, which returns the recognised text and its coordinates. The tool checks for required information (error messages, status updates, configuration details) by matching predefined strings or patterns. In some cases, the bounding box coordinates of a text are used to click on that text or button with PyAutoGUI.
2. **GUI automation with PyAutoGUI.** It automates interaction with the OBD tool's interface: clicking buttons, entering text and navigating menus.
   - *Mouse actions* move the cursor, click and scroll. This works on any screen size because coordinates come from a current screenshot rather than fixed values.
   - *Keyboard actions* press keys and type text.
   - *Image recognition* finds GUI elements such as buttons or icons with functions like `pyautogui.locateOnScreen()`, which searches the screen by pixel comparison and returns the coordinates.
   - *Error handling and retries:* if an element is not found within a set time (e.g. 10 seconds), the tool retries or switches to an alternative workflow, such as restarting the application or logging an error.
3. **API connection to CANoe.** In parallel with the OBD tool workflow, the CANoe COM API triggers predefined processes, e.g. setting signals to wake an ECU or creating other preconditions, so the whole test environment stays consistent and synchronised.

### 4.2 Functions

1. **Automatic coding:** codes different vehicle combinations based on country- and vehicle-specific configuration requirements. "Coding" means installing the function data sets of each combination on the ECU platform to check the software functions, e.g. testing the plausibility and applicability of the data sets using a manifest that contains the coding steps.
2. **Reading measured values:** reads all relevant measurements from the ECU. The queries are stored in an Excel list in the repository and can be edited by the user.
3. **Diagnostic tests:** runs diagnostic tests beyond what the OBD tool offers, including interaction with CANoe to manipulate signals and control vehicle communication. Tests can be activated or added in the diagnostic table.

![Diagnostic test case table of the tool]({{ '/assets/img/test-automation/test-cases-table.png' | relative_url }})
*Figure 4: Diagnostic table (UDS requests and expected responses)*

### 4.3 Workflow example: automated coding

- **User input:** the user enters the required inputs in the GUI, e.g. login credentials, vehicle configurations and project folder.
- **Test initialisation:** the tool logs in to the backend system with the provided credentials and sets up the test environment (selecting vehicle configurations, loading the required files).
- **Test execution:** the tool runs the tests in the OBD application and, where needed, in CANoe.
- **Error handling:** if OCR detects error messages, the tool tries to fix the problem automatically (repeating the action, reconnecting the communication module, or logging the error).
- **Completion and reporting:** the tool compiles a report with the test results and all detected errors and stores it as an Excel sheet in the SharePoint repository. Detected errors are taken from the DTC list exported by the OBD tool.

### 4.4 Discussion

The tool contributed significantly to efficiency. The main benefit is the time saved, especially when evaluating tests. Automation minimised human error, particularly in manual coding of variants, and its test depth made it possible to test many configurations and vehicle combinations that would have been hard to cover manually.

It also brought challenges. The tool depends on OBD tool updates: major updates can break functionality or require adjustments. It also cannot learn from defects already tested, so ongoing defect management is still needed. Despite the benefits, continuous monitoring and occasional manual intervention remain necessary to ensure high test quality.

### 4.5 Migration to the cloud

Migrating test automation to the cloud is a strategic decision with potential benefits: more efficient use of resources, better scalability and faster software validation. In some situations, however, it makes no sense, so this section asks: *does it make sense to move software tests to the cloud?* The solution already uses a cloud OCR service as SaaS, where cost efficiency through pay-as-you-go is the first benefit.

#### 4.5.1 Why a full migration may not make sense

1. **Real-time tests and physical connectivity.** Tests that need real-time data transfer and low-latency responses can suffer from network latency in the cloud. Real-time diagnostics and some HiL or SiL tests may not suit a cloud environment (Tilley & Parveen, 2012, ch. 2, pp. 27–28). The OBD tool needs a direct physical connection to the vehicle's OBD-II port, which would require intermediate hardware such as an edge device to bridge to the cloud (common in production for vehicle-wide software updates). If tests depend heavily on physical connectivity, the extra complexity and cost of maintaining edge devices can outweigh the benefits.
2. **Security and compliance.** Automotive software testing often involves sensitive data subject to strict security and privacy requirements (e.g. TISAX, ISO 26262). Meeting them in the cloud could be more complex and costly, so additional security measures and compliance checks would be needed.

#### 4.5.2 A hybrid approach

If CANoe and the OBD tool stay on a local machine, they keep working as intended and capture all diagnostic data accurately and in real time, without latency or connection issues. A hybrid solution that moves only selected services (defect analysis, test result management, etc.) to the cloud is therefore more sensible:

1. **Middleware for communicating with the local OBD tool.** A middleware running on the same machine as the OBD tool and GUI automation collects the automation's outputs (logs, diagnostic results), converts them into a standard format and sends them securely to cloud services. This moves non-real-time processes such as storage, advanced analytics and test management to the cloud without affecting the OBD tool locally. Applied Intuition, for example, offers a "Cloud Engine" that integrates simulation data from HiL and SiL with cloud analytics in local-to-cloud and cloud-to-local workflows. The cloud side would include:
   - **Data storage:** diagnostic data stored in cloud databases (e.g. AWS S3, Google Cloud Storage), accessible to other services and team members from anywhere.
   - **Analytics and reporting:** machine learning to find patterns, detect anomalies or predict follow-up failures, presented in reports for all stakeholders.
   - **Test case management and orchestration:** a cloud service such as Jenkins coordinates local OBD tests via the middleware, GUI automation and cloud tests such as simulations, while test cases stay in DOORS as the source of truth for requirements.
   - **Defect-driven test case generation:** when a new defect is found, a matching test case is generated automatically and added to the system (e.g. Jenkins linked with DOORS), so the defect is caught early next time (regression detection).
2. **Standardised service interfaces.** RESTful APIs exposed by the middleware let cloud services fetch the latest diagnostic data and send results back for local use, simplifying integration.
3. **Scalable cloud services.** Storage, analytics and test management scale with data volume or number of tests, without changes to the local machine running the OBD tool.

In short, the hybrid approach moves non-real-time processes to the cloud while keeping essential real-time operations, such as the OBD tool, local. The middleware optimises communication between the two, improves scalability and fault isolation, and opens the door to future extensions such as defect management and traceability.

## 5 Summary

This report covered the implementation of an efficient test automation solution for vehicle ECU software and the possibility of moving these processes to the cloud. The main goal was to increase test efficiency and depth.

The solution was tailored to ECU testing, integrating CANoe and the OBD tool, and used GUI-based automation to speed up interaction with diagnostic tools and reduce human error. In practice it shortened test times and increased test depth, enabling more efficient defect detection and resolution and efficient testing of different vehicle configurations.

The analysis of a cloud migration highlighted scalability and flexibility as key benefits for complex test scenarios, but found that a full migration is not always practical because of real-time requirements and physical connectivity. The proposed hybrid approach migrates selected processes while keeping essential real-time functions local. It has not yet been implemented, but it is a robust way to use cloud resources for non-real-time processes while critical real-time diagnostics stay local.

## 6 Outlook

Test development in the automotive industry faces an exciting future, especially through AI integration in defect management systems that not only detect defects automatically but also proactively monitor future vehicle versions and software changes.

A first step is moving key processes such as test management, data storage and analytics to the cloud. This lays the foundation for efficient defect management through better analytics and data access. Integrated deeply into development and release cycles, the system receives real-time updates for precise monitoring, and machine learning continuously improves its ability to predict and diagnose defects.

An intelligent defect management system built on the proposed migration strategy is a new step in automating test and diagnostic processes. Integrated into existing development environments, it can shorten test cycles significantly, leading to faster software validation and getting products customer-ready sooner.

## References

- Aniche, M. (2022). *Effective Software Testing: A Developer's Guide*. Manning.
- Dajsuren, Y., & van den Brand, M. (Eds.). (2019). *Automotive Systems and Software Engineering: State of the Art and Future Trends*. Springer.
- ISO 21111-1:2020. *Road vehicles — In-vehicle Ethernet — Part 1: General information and definitions*.
- ISO 14229-1:2020. *Road vehicles — Unified diagnostic services (UDS) — Part 1: Application layer*.
- ISO 26262-10:2018. *Road vehicles — Functional safety — Part 10: Guidelines on ISO 26262*.
- Ravi Aravind, C. V. (2024). Innovations in Electronic Control Units: Enhancing Performance and Reliability with AI. *International Journal of Engineering and Computer Science*.
- NIST (2011). *The NIST Definition of Cloud Computing* (SP 800-145). https://nvlpubs.nist.gov/nistpubs/legacy/sp/nistspecialpublication800-145.pdf
- Tilley, S., & Parveen, T. (2012). *Software Testing in the Cloud: Migration and Execution*. Springer.
