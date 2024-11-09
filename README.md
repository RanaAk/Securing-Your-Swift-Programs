# Securing Your Swift Programs

Swift offers several ways to implement secure functionalities for apps. Here are seven essential methods to enhance the security of your Swift programs.

### 1. Generate a Secure Random Token

```swift
import CryptoKit

func generateSecureToken(length: Int) -> String {
    let token = (0..<length).map { _ in
        String(format: "%02x", Int.random(in: 0...255))
    }.joined()
    return token
}

print("Secure Token:", generateSecureToken(length: 16))
```

- This function creates a secure token by generating random bytes and converting them into a hexadecimal string. You can Adjust the length as needed.

---

### 2. Generate a Strong Password

```swift
import Foundation

func generatePassword(length: Int = 12) -> String {
    let letters = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*()"
    let password = String((0..<length).compactMap { _ in letters.randomElement() })
    return password
}

print("Generated Password:", generatePassword())
```
- This function creats a strong , random password using letters, digits and symbols.

---

### 3. Select a Secure Random Element from a List

```swift
import Foundation

let participants = ["Alice", "Bob", "Charlie", "David"]

if let winner = participants.randomElement() {
    print("Winner:", winner)
}
```


- The `randomElement()` function securely picks an item from the array.

---

### 4. Create a Cryptographically Secure OTP (One-Time Password)

```swift
import Foundation

func generateOTP(length: Int = 5) -> String {
    return (0..<length).map { _ in String(Int.random(in: 0...9)) }.joined()
}

print("Generated OTP:", generateOTP())
```

- To create a one-time password (OTP) for secure, temporary access codes.

---

### 5. Compare Sensitive Data Securely

```swift
import CryptoKit

func secureCompare(_ actualToken: String, _ userToken: String) -> Bool {
    guard let actualData = actualToken.data(using: .utf8),
          let userData = userToken.data(using: .utf8) else {
        return false
    }
    
    let key = SymmetricKey(size: .bits256)
    let actualHMAC = HMAC<SHA256>.authenticationCode(for: actualData, using: key)
    let userHMAC = HMAC<SHA256>.authenticationCode(for: userData, using: key)
    
    return actualHMAC == userHMAC
}

// Example Usage
let actualToken = "AAA000"
let userToken = "AAA000"
if secureCompare(actualToken, userToken) {
    print("Tokens match!")
} else {
    print("Tokens do not match.")
}
```

- To securely compare sensitive data, use a method to avoid timing attacks. This example uses HMACs to securely compare two tokens.

---
