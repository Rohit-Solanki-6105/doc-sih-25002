Phase 1 —>
1️⃣ Police Verification & Token Generation
1.	Tourist provides physical documents:

○	Indian → Aadhaar

○	Foreigner → Passport

2.	Police verify documents manually.

3.	Once verified, police generate a unique token (NFT or ERC20) on Ethereum blockchain, storing verified info:

○	Name

○	Aadhaar (for Indian) or Passport (for foreigner)

○	Mobile Number

○	Verified Status

4.	FastAPI backend stores mapping:
 ID → Token_ID → Mobile Number

○	ID = Aadhaar for Indians, Passport for foreigners

________________________________________
2️⃣ Tourist Mobile App Login
1.	Tourist opens app and enters:

○	Indian → Aadhaar + OTP

○	Foreigner → Passport + OTP

2.	Backend checks the database:

○	Does this ID exist?

○	Is a token issued?

3.	If yes → generate OTP → send to mobile linked to the token.

4.	Tourist enters OTP → backend verifies.

________________________________________
3️⃣ Profile Access (Blockchain Integration)
1.	After OTP verification, backend fetches tourist info from Ethereum blockchain using Token_ID.

2.	Mobile app displays verified profile:

○	Name

○	ID (Aadhaar or Passport)

○	Mobile Number

○	Verified Status

________________________________________
4️⃣ Real-Time Police Dashboard Update
1.	FastAPI server uses Socket.IO to communicate with police dashboard.

2.	On successful tourist login:

○	Backend emits a real-time event containing tourist info to police dashboard.

3.	Police dashboard displays:

○	Tourist Name

○	ID (Aadhaar/Passport)

○	Token_ID

○	Login Time

○	Verified Status

