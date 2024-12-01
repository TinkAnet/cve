# Vulnerability Report

## Vulnerability Name

Buffer Overflow Vulnerability - `Student Record Management System`


## **Submitted By: Tinkanet**


## Vulnerability Information

### Affected Components

- **System/Software Name**: Student Record Management System
- **Version**: Current Implementation
- **Platform**: Linux
- **Affected Features**:
    - Add New Students (`Add New Students`)
    - View All Student Marks (`View All Student Marks`)

### Project Information

- **Source Code Link**: [Student Record Management System - Source Code](https://www.sourcecodester.com/cc/16827/student-record-management-system-c-source-code.html)
- **Project Download Link**: [Download Student Record Management System Project](https://www.sourcecodester.com/sites/default/files/download/razormist/Student%20Record%20Management%20System%20in%20C%2B%2B.zip)


## Vulnerability Overview

The `Student Record Management System` contains a **critical buffer overflow vulnerability**, which manifests as follows:

1. **Unrestricted User Input**:
In the `cin >> data` operation, there is no restriction on the length of input strings. This allows attackers to exploit this point by providing overly long inputs, leading to buffer overflow and memory corruption.
2. **Fragile File Handling Logic**:
When processing overly long records, fixed-size buffers are used, resulting in memory corruption and subsequent illegal memory access (`EXC_BAD_ACCESS`).

### Potential Impact

The vulnerability could lead to the following severe outcomes:

- **Remote Code Execution (RCE)**:
By crafting malicious inputs, attackers could overwrite return addresses or function pointers to control program execution flow.
- **Denial of Service (DoS)**:
Overly long inputs directly cause the program to crash, rendering the service unavailable.
- **Data Integrity Violations**:
Overflows could corrupt or falsify the content of record files, jeopardizing the confidentiality and integrity of the data.


## Vulnerability Type

- **Buffer Overflow**


## Steps to Reproduce

### 1. Environment Setup

1. **Compile the Program**:
Use debug symbols to enable tracing and validation during testing.
    
    ```bash
    g++ -g -o student_record "Student Record Management System.cpp"
    ```
    
    <img width="1130" alt="image" src="https://github.com/user-attachments/assets/f18524ae-ce6b-443d-8524-5a292408fc2b">



    

**2. Testing Procedure**

1. **Launch the Program**:

Start the program under lldb:

```coffeescript
lldb ./student_record
```

1. **Set Breakpoints**:

Add breakpoints at key locations:

- Line 53: cin >> data; (handles user input)
- Line 186: infile >> data; (handles file reading)

```coffeescript
breakpoint set --file "Student Record Management System.cpp" --line 53
breakpoint set --file "Student Record Management System.cpp" --line 186
run
```

<img width="1131" alt="image 1" src="https://github.com/user-attachments/assets/a6f5c435-0575-431d-a3b6-9faa0dec413c">


1. **Provide Test Input**:

<img width="1136" alt="image 2" src="https://github.com/user-attachments/assets/00602e11-41f9-4f4f-ba65-f73668c2ab8f">


1. **Memory State**

After entering the overly long string, inspect the data variable’s content and memory layout:

```coffeescript
(lldb) print data
(lldb) x/128xb &data
```

<img width="709" alt="image 3" src="https://github.com/user-attachments/assets/758180e4-7ef1-41e7-848e-1df0376d1941">


1. **rigger the Crash**:
- Choose Option 4 (View All Student Marks).
- Enter the admin password:

```coffeescript
Enter the admin password: admin
```

- The program crashes with EXC_BAD_ACCESS.

<img width="1135" alt="image 4" src="https://github.com/user-attachments/assets/0b539947-8005-4e81-bb65-13b739d15c9a">


1. **Stack Trace**

When the program crashes, check the stack trace to locate the crash point:

```coffeescript
bt
```

<img width="1130" alt="image 5" src="https://github.com/user-attachments/assets/933c9339-15b1-466a-a9bb-a3a738ca47e7">


**Insert Screenshot Here**:

- Show the call stack and EXC_BAD_ACCESS error.

**Technical Analysis**

**Vulnerable Code Locations**

1. **Input Handling Vulnerability**:

```coffeescript
cin >> data; // Unrestricted input length causes buffer overflow
```

- Variable: char data[15]
- Impact: Overly long input overwrites adjacent stack memory.
1. **File Handling Vulnerability**:

```coffeescript
infile >> data; // Fixed-size buffer causes memory corruption
```

- Variable: char data[20]
- Impact: Overly long records corrupt memory, leading to crashes.

**Vulnerability Impact**

**Exploitation Potential**

1. **Remote Code Execution**:

Attackers can overwrite return addresses or control program execution flow by crafting malicious inputs, enabling:

- Data theft
- Privilege escalation
- Full system compromise
1. **Denial of Service (DoS)**:

Overly long inputs directly crash the program, causing prolonged service downtime.

1. **Data Tampering and Leakage**:

Attackers can manipulate or falsify file content, compromising data integrity and confidentiality.

**Recommendations**

1. **Input Validation**:

Replace cin >> data with cin.getline, and define strict input length limits:

```coffeescript
cin.getline(data, sizeof(data));
```

1. **Field Length Validation**:

Ensure file field lengths do not exceed buffer sizes:

```coffeescript
if (strlen(data) >= sizeof(data)) {
    cerr << "Data too long, skipping record!" << endl;
    continue;
}
```

1. **Dynamic Memory Management**:

Replace fixed-size char[] arrays with dynamically allocated std::string to improve resilience.

**Timeline**

- **Discovery Date**: 2024-12-01
- **Reproduction Completion**: 2024-12-02

**Report Author**

- **Name**:

**Additional Notes**

This vulnerability has significant exploitation potential and poses severe risks in production environments. Immediate remediation is recommended, along with a comprehensive review of similar code sections to mitigate future threats.
