# 🛡️ Tourist Verification & Alert System (Phase 1)

This system verifies tourists using **Ethereum Blockchain**, provides **OTP-based login**, and updates the **Police Dashboard in real-time** via **FastAPI + Socket.IO**.

---

## 🚀 Flow Overview

### 1. Police Verification & Token Generation
- Tourist shows **Aadhaar (Indian)** or **Passport (Foreigner)**.  
- Police verify the document **physically**.  
- If correct → Police generate **Token_ID** on **Ethereum blockchain** (stores verified tourist info).  
- Backend maps:  
---

### 2. Tourist Login (Mobile App)
1. Tourist enters only **Aadhaar (Indian)** or **Passport (Foreigner)** in the app.  
2. Backend checks database:  
 - Does this ID exist?  
 - Does it have a token?  
3. If yes → Backend generates **OTP** → sends to tourist’s mobile number.  
4. Tourist enters OTP in the app.  
5. Backend verifies OTP.  

---

### 3. Profile Access
- Once OTP is verified:  
- Backend fetches **tourist info from blockchain (via Token_ID)**.  
- Mobile app displays **verified profile**:  
  - ✅ Name  
  - ✅ Aadhaar/Passport  
  - ✅ Mobile Number  
  - ✅ Verified Status  

---

### 4. Police Dashboard Auto-Update
- When tourist login succeeds:  
- **FastAPI emits tourist info via Socket.IO**.  
- Police dashboard instantly updates, showing:  
  - 👤 Tourist Name  
  - 🆔 Aadhaar/Passport  
  - 🔑 Token_ID  
  - ⏰ Login Time  
  - 🛡 Verified Status  

---

## 📊 Flow Diagram (Mermaid)

```mermaid
flowchart TD
  A[Tourist: Aadhaar/Passport] --> B[FastAPI Backend]
  B -->|Check DB| C{Token Exists?}
  C -->|No| D[Reject Login]
  C -->|Yes| E[Generate OTP → Send to Mobile]
  E --> F[Tourist Enters OTP]
  F -->|Verify OTP| G[Fetch Tourist Info from Blockchain]
  G --> H[Mobile App Displays Verified Profile]
  G --> I[Emit Tourist Info via Socket.IO]
  I --> J[Police Dashboard Updates]
