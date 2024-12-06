# SourceCodester Phone Contact Manager System in C++ with Source Code V1.0 ContactBook.cpp -Buffer Pollution Leading to Data Storage Corruption

## **Vulnerability Name**

- Buffer Pollution Leading to Data Storage Corruption

## **Submitted By**

- **Submitter Name:** Tinkanet

## **Project Information**

- **Project Name**: Phone Contact Manager System
- **Source Code Download**: [Download Source Code](https://www.sourcecodester.com/sites/default/files/download/razormist/Phone%20Contact%20Manager%20System%20in%20C%2B%2B.zip)
- **Project Homepage**: [homepage](https://www.sourcecodester.com/cc/16822/phone-contact-manager-system-c-source-code.html)

## **Vulnerable File**

- **Filename**: ContactBook.cpp
- **Location**: ContactBook::adding() method

## **Vulnerable Code**

```cpp
void ContactBook::adding() {

std::string vals[4];

for (int i = 0; i < 4; i++) {

std::cout << details[i] << ": ";

getline(std::cin >> std::ws, vals[i]);

}

Contact contact(vals[0], vals[1], vals[2], vals[3]);

contact.add();

}
```

![image.png](SourceCodester%20Phone%20Contact%20Manager%20System%20in%20C++%201544643d864880a5a504c78bab78f866/image.png)

## **Vulnerability Description**

The vulnerability stems from the program’s improper handling of input buffers, leaving residual data in the buffer that pollutes subsequent logic.

When the user enters a menu option (e.g., 1kkk):

- The program parses the numeric portion (1) as the menu option.
- The remaining characters (kkk) are left in the input buffer.

During subsequent contact information entry logic, the program calls getline to read the Name. Instead of waiting for user input, it directly reads the residual characters kkk from the buffer.

As a result, the invalid data is incorrectly treated as legitimate contact information and stored in the system.

## **Vulnerability Logic**

1. **Trigger Condition**
- The user enters mixed input (e.g., 1kkk) when selecting a menu option.
1. **Problem Occurrence**
- Residual characters in the buffer are not cleared, directly affecting the getline logic.
1. **Resulting Impact**
- Polluted data is recorded as legitimate contact information:

![image.png](SourceCodester%20Phone%20Contact%20Manager%20System%20in%20C++%201544643d864880a5a504c78bab78f866/image%201.png)

## **Debugging Screenshots**

1. **Trigger Point: Residual Data in Buffer After Menu Selection**

![image.png](SourceCodester%20Phone%20Contact%20Manager%20System%20in%20C++%201544643d864880a5a504c78bab78f866/image%202.png)

![image.png](SourceCodester%20Phone%20Contact%20Manager%20System%20in%20C++%201544643d864880a5a504c78bab78f866/image%203.png)

1. **Polluted Input Logic**

*In ContactBook::adding(), observe vals[0] assigned with kkk*

![image.png](SourceCodester%20Phone%20Contact%20Manager%20System%20in%20C++%201544643d864880a5a504c78bab78f866/image%204.png)

1. **Stored Polluted Data**

*Check the stored contact information with polluted data*

![image.png](SourceCodester%20Phone%20Contact%20Manager%20System%20in%20C++%201544643d864880a5a504c78bab78f866/image%205.png)

![image.png](SourceCodester%20Phone%20Contact%20Manager%20System%20in%20C++%201544643d864880a5a504c78bab78f866/image%206.png)

## **Impact**

1. **Data Integrity**
- Invalid data is stored, compromising the integrity of contact information.
1. **Logical Deviation**
- The program skips user interaction for input and directly uses residual data.
1. **Potential Risks**
- Malicious users could exploit this vulnerability to input invalid data, leading to program instability or further exploits.

## **Mitigation Suggestions**

1. **Clear Input Buffer**

Clear the input buffer after parsing menu options:

```cpp
std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
```

1. **Input Validation**

Validate the user input for each field to ensure legitimacy:

```cpp
if (vals[i].empty()) {

std::cerr << details[i] << " cannot be empty.\n";

continue;

}
```

1. **Testing and Validation**
- Conduct comprehensive tests for boundary inputs and invalid data scenarios.
- Ensure input buffer clearance and input validation logic function correctly.