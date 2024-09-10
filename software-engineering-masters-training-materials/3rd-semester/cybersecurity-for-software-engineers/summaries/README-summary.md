# Cybersecurity for Software Engineers

## Course Overview
This course provides a comprehensive understanding of cybersecurity principles and practices crucial for software engineers. It covers secure coding practices, cryptographic techniques, network security, and advanced security testing methods.

## Course Content

### **1. Introduction to Cybersecurity**

#### **Security Fundamentals**
- **Confidentiality, Integrity, Availability (CIA Triad)**: Key principles for ensuring data security.
- **Threats and Vulnerabilities**: Common threats (e.g., malware, phishing) and vulnerabilities (e.g., software bugs, configuration issues).

**Real-World Example:**
- **Threat Modeling**: Analyze a software application to identify potential threats and vulnerabilities.

### **2. Secure Coding Practices**

#### **Common Vulnerabilities**
- **OWASP Top Ten**: Common security risks such as SQL Injection, Cross-Site Scripting (XSS), and Cross-Site Request Forgery (CSRF).

**Code Example (Python for SQL Injection Prevention):**
```python
import sqlite3

def get_user_by_id(user_id):
    conn = sqlite3.connect('database.db')
    cursor = conn.cursor()
    # Using parameterized queries to prevent SQL Injection
    cursor.execute("SELECT * FROM users WHERE id=?", (user_id,))
    user = cursor.fetchone()
    conn.close()
    return user
```

**Code Example (C++ for Secure String Handling):**
```cpp
#include <iostream>
#include <cstring>

// Secure function to prevent buffer overflow
void safeCopy(char* dest, const char* src, size_t destSize) {
    strncpy(dest, src, destSize - 1);
    dest[destSize - 1] = '\0'; // Null-terminate the string
}

int main() {
    char buffer[10];
    const char* input = "This is a long string!";
    safeCopy(buffer, input, sizeof(buffer));
    std::cout << buffer << std::endl;
    return 0;
}
```

#### **Secure Coding Guidelines**
- **Input Validation**: Ensure all inputs are validated and sanitized.
- **Error Handling**: Avoid exposing sensitive information through error messages.

**Real-World Example:**
- **Secure Coding Review**: Conduct a review of a codebase to identify and fix security issues.

### **3. Cryptography**

#### **Symmetric and Asymmetric Encryption**
- **Symmetric Encryption**: AES, DES.
- **Asymmetric Encryption**: RSA, ECC.

**Code Example (Python with Cryptography Library):**
```python
from cryptography.fernet import Fernet

# Generate a key
key = Fernet.generate_key()
cipher_suite = Fernet(key)

# Encrypt and decrypt data
text = b"Sensitive data"
cipher_text = cipher_suite.encrypt(text)
plain_text = cipher_suite.decrypt(cipher_text)

print(f"Encrypted: {cipher_text}")
print(f"Decrypted: {plain_text}")
```

**Code Example (C++ with OpenSSL for RSA Encryption):**
```cpp
#include <openssl/rsa.h>
#include <openssl/pem.h>
#include <openssl/err.h>
#include <iostream>

// Generate RSA key pair
void generateRSAKeyPair() {
    RSA *rsa = RSA_generate_key(2048, RSA_F4, NULL, NULL);
    BIO *bio = BIO_new(BIO_s_mem());

    PEM_write_bio_RSAPublicKey(bio, rsa);
    PEM_write_bio_RSAPrivateKey(bio, rsa, NULL, NULL, 0, NULL, NULL);

    char *key;
    long keyLength = BIO_get_mem_data(bio, &key);

    std::cout << "Generated RSA Key Pair: " << std::endl << std::string(key, keyLength) << std::endl;

    BIO_free_all(bio);
    RSA_free(rsa);
}

int main() {
    generateRSAKeyPair();
    return 0;
}
```

#### **Hashing and Digital Signatures**
- **Hash Functions**: SHA-256, SHA-3.
- **Digital Signatures**: Signing and verifying messages using private and public keys.

**Code Example (Python for Hashing with SHA-256):**
```python
import hashlib

def hash_message(message):
    sha256 = hashlib.sha256()
    sha256.update(message.encode('utf-8'))
    return sha256.hexdigest()

print(hash_message("This is a message"))
```

**Code Example (C++ with OpenSSL for SHA-256 Hashing):**
```cpp
#include <openssl/sha.h>
#include <iostream>
#include <iomanip>

std::string hashSHA256(const std::string& input) {
    unsigned char hash[SHA256_DIGEST_LENGTH];
    SHA256_CTX sha256;
    SHA256_Init(&sha256);
    SHA256_Update(&sha256, input.c_str(), input.size());
    SHA256_Final(hash, &sha256);

    std::ostringstream oss;
    for (int i = 0; i < SHA256_DIGEST_LENGTH; i++) {
        oss << std::hex << std::setw(2) << std::setfill('0') << (int)hash[i];
    }
    return oss.str();
}

int main() {
    std::string input = "This is a message";
    std::cout << "SHA-256 Hash: " << hashSHA256(input) << std::endl;
    return 0;
}
```

#### **Public Key Infrastructure (PKI)**
- **Certificate Authorities**: Role of CA in managing digital certificates.
- **Certificate Management**: Issuance, renewal, and revocation.

**Real-World Example:**
- **PKI Implementation**: Set up a simple PKI system to manage digital certificates.

### **4. Network Security**

#### **Firewalls and VPNs**
- **Firewalls**: Types (network vs. application firewalls), rules, and configurations.
- **VPNs**: Secure communication over public networks.

**Code Example (Python for Simple Firewall Rule Implementation):**
```python
import ipaddress

def is_ip_allowed(ip_address, allowed_ips):
    return ipaddress.ip_address(ip_address) in allowed_ips

allowed_ips = {ipaddress.ip_address('192.168.1.1')}
print(is_ip_allowed('192.168.1.1', allowed_ips))  # Output: True
print(is_ip_allowed('10.0.0.1', allowed_ips))  # Output: False
```

#### **Intrusion Detection and Prevention Systems (IDS/IPS)**
- **IDS/IPS Basics**: Monitoring, detection, and response to security breaches.
- **Types**: Signature-based, anomaly-based.

**Real-World Example:**
- **IDS Implementation**: Develop a basic IDS to detect suspicious network activity.

### **5. Security Testing and Auditing**

#### **Penetration Testing**
- **PenTest Methodologies**: Scanning, exploitation, and reporting.
- **Tools**: Metasploit, Burp Suite.

**Code Example (Python with Scapy for Network Scanning):**
```python
from scapy.all import sr1, IP, ICMP

def ping(host):
    packet = IP(dst=host)/ICMP()
    response = sr1(packet, timeout=2)
    if response:
        print(f"{host} is reachable")
    else:
        print(f"{host} is not reachable")

ping("8.8.8.8")  # Test with Google DNS
```

#### **Security Audits and Compliance**
- **Auditing Techniques**: Reviewing code, configuration, and processes.
- **Compliance Standards**: GDPR, HIPAA.

**Real-World Example:**
- **Conducting a Security Audit**: Perform a comprehensive security audit on a software application.

## Assessment
- **Security Assessment Project**: Design and implement a security assessment of a real-world application.
- **Penetration Testing Exercises**: Conduct penetration tests and report findings.
- **Final Exam**: Comprehensive exam covering all course topics.

## Resources
- **"Computer Security: Principles and Practice" by William Stallings**: In-depth exploration of cybersecurity principles.
- **"The Web Application Hacker's Handbook" by Dafydd Stuttard, Marcus Pinto**: Detailed guide on web application security.
