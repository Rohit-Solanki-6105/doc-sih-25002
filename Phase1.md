### 1. Police Verification & Token Generation

Tourist shows Aadhaar (Indian) or Passport (foreigner).

Police verify the document physically.

If correct → police generate Token_ID on Ethereum blockchain (stores verified tourist info).

Backend maps:
ID (Aadhaar/Passport) → Token_ID → Mobile Number.

### 2. Tourist Login (Mobile App)

Tourist enters only Aadhaar (Indian) or Passport (foreigner) in the app.

Backend checks DB:

Does this ID exist?

Does it have a token?

If yes → Backend generates OTP → sends to tourist’s mobile number.

Tourist enters OTP in the app.

Backend verifies OTP.

### 3. Profile Access

Once OTP is verified:

Backend fetches tourist info from blockchain (via Token_ID).

App displays verified profile:

Name

Aadhaar/Passport

Mobile Number

Verified Status

4. Police Dashboard Auto-Update

When tourist login succeeds:

FastAPI emits tourist info via Socket.IO.

Police dashboard instantly updates, showing:

Tourist Name

Aadhaar/Passport

Token_ID

Login Time

Verified Status
