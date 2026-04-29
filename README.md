# C-essentials
# 🧠 Memory-Mastery-C-Security: Arrays, Pointers, and Strings
> **Course:** Cisco Cybersecurity Essentials / CLA Programming Essentials
> **Student:** Kush Pithadia

---

## 📖 PROJECT OVERVIEW
In low-level programming, memory is a physical resource. This project explores how C manages data in RAM and how a cybersecurity professional identifies memory-based vulnerabilities like Buffer Overflows.

---

## 🚀 PART 1: THE SECURITY LAB (C CODE)
/* 
 * Save this as 'security_lab.c'
 * Compile: gcc security_lab.c -o lab
 */

#include <stdio.h>
#include <string.h>

void memory_demonstration() {
    // 1. ARRAYS & MEMORY LOCALITY
    // Array elements are stored in contiguous memory addresses
    int sensor_data[3] = {101, 202, 303};
    
    // 2. POINTERS: Direct Address Access
    // A pointer stores the 'where', not the 'what'
    int *ptr = sensor_data; 

    printf("[SYSTEM] Analyzing Memory Layout...\n");
    for(int i = 0; i < 3; i++) {
        printf("Index %d | Address: %p | Value: %d\n", i, (void*)&sensor_data[i], sensor_data[i]);
    }

    // 3. STRINGS & VULNERABILITY
    // Strings MUST end with \0. If missing, we get 'Information Leakage'.
    char secret_token[] = "CISCO_PASS_123";
    char buffer[10];

    printf("\n[ALERT] Testing String Security...\n");
    
    // UNSAFE: strcpy(buffer, secret_token); // This would cause a Buffer Overflow
    
    // SAFE: strncpy with null-termination
    strncpy(buffer, secret_token, sizeof(buffer) - 1);
    buffer[sizeof(buffer) - 1] = '\0'; 

    printf("[SAFE] Buffer Content: %s\n", buffer);
}

int main() {
    printf("========================================\n");
    printf("   CISCO CYBERSECURITY MEMORY LAB       \n");
    printf("========================================\n");
    memory_demonstration();
    return 0;
}

---

## 🛡️ PART 2: TECHNICAL DOCUMENTATION

### 🏗️ Memory Architecture Breakdown
| Concept | Definition | Security Significance |
| :--- | :--- | :--- |
| **Arrays** | Contiguous memory blocks. | Accessing out of bounds causes "Memory Corruption." |
| **Pointers** | Variables storing addresses. | Can be hijacked to redirect program flow. |
| **Strings** | Null-terminated char arrays. | Missing `\0` leads to "Buffer Over-read." |

### ⚔️ Attack & Defense Matrix
1. **Buffer Overflow:** 
   - *Risk:* Overwriting the Stack to execute malicious code.
   - *Mitigation:* Use `fgets()` and `strncpy()` instead of `gets()` or `strcpy()`.
   - 

2. **Dangling Pointers:**
   - *Risk:* Accessing memory after it's freed leads to crashes or exploits.
   - *Mitigation:* Always set pointers to `NULL` after calling `free()`.

3. **Format String Attack:**
   - *Risk:* Using `printf(user_input)` allows an attacker to leak memory addresses.
   - *Mitigation:* Always use `printf("%s", user_input)`.

---

## 🛠️ HARDENING CHECKLIST
- [x] Initialized all variables and pointers.
- [x] Implemented manual bounds checking on all loops.
- [x] Verified null-termination for every string operation.
- [x] Replaced all "unsafe" C functions with secure alternatives.

---

## 👤 AUTHOR INFORMATION
**Kush Pithadia**
* **Project:** Memory Management & Logic Hardening
* **LinkedIn:** [View Profile](https://www.linkedin.com/in/kush-pithadia-966b662bb)

*Disclaimer: This documentation is for educational purposes only.*
