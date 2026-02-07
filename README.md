# GPON ONU Serial Number Assignment

Production grade automation tool for assigning GPON ONUs on **Iskratel SI3000 Pono** access devices.

This repository is published as a portfolio showcase to demonstrate system design, automation logic, safety considerations and real-world ISP operations.

> **Availability**  
> Source code and executable files are not publicly distributed to prevent misusage and protect proprietary working logic.  
> A demo, walkthrough or technical discussion is available upon request.

---

## Why I created this tool

Assigning ONUs on Iskratel GPON devices via CLI is highly sensitive:
- A mistyped command (example: wrong "onu clear 1/2//") can impact an entire OLT.
- Manual serial number-to-subscriber port assignment is slow.
- Devices may respond with delayed or segmented output.
- Internal database locks frequently interrupt assigning process.

This little tool was built to eliminate human accidental error, increase speed and add safety.

---

## How the tool works

- Connects to GPON access devices over **Telnet (TCP 23)**.
- Network engineer enters IP address, login and password.
- Network engineer selects an **OLT slot (1-8)**.
- Network engineer pastes **ONU modem serial numbers** (8-hex format) into **ONU port fields 1–64**.
- Executes validated CLI commands automatically, for example: onu set 1/OLT/ONU vendorid ZNTS serno fsan <SERIAL>
- Waits for device confirmation before proceeding to the next ONU.

---

## Key safety & reliability features

- **Strict serial validation**  
Accepts only exactly **8 hexadecimal characters** (example: "0329F87E").

- **Dangerous command protection**  
Dangerous commands (such as "onu clear") are explicitly blocked.

- **Database lock detection & retry logic**  
Automatically detects DB lock messages and retries with safe backoff.

- **Segmented output handling**  
Correctly processes CLI output that arrives in partial unit of data.

- **Per-ONU visual feedback**
- **Green** - successful assignment
- **Yellow** - success after retry (example: database lock)
- **Red** - failure after retries or timeouts

- **Threaded GUI execution**  
Long operations never freeze the user interface.

---

## User interface overview

- **Top control bar:**
- IP Address / login / password
- OLT slot selector
- Start / Stop / Clear controls

- **Main panel:**
- ONU 1-64 serial input fields

- **Bottom panel:**
- Live execution logs with retry and status messages

---

## Screenshots

See docs/screenshots/ for:
- Main application window
- ONU status color feedback
- Example of assignment logs

---

## Technical highlights

- Real device tested retry logic tuned for Iskratel GPON
- Deterministic success detection based on actual ISP device output
- Clear separation between UI, networking and execution
- Designed for engineer safety, not just automation speed

---

## Distribution note

This project interacts directly with live GPON infrastructure.

To prevent unauthorized usage or unsafe deployment source code is not published and executable files are not distributed.

---

## Author

Created by: Guga Gugunava  
Email: guga.gugunava@gmail.com  
WhatsApp: +995 577 50 69 05
