# RESTful API Kya Hoti Hai?

RESTful API ek web service architecture hai jo HTTP methods (GET, POST, PUT, PATCH, DELETE) ka use karke client aur server ke beech data exchange karti hai.

### Main HTTP Methods (Verbs)
REST me data par **CRUD** (Create, Read, Update, Delete) operations karne ke liye niche diye gaye methods use hote hain:

* **GET:** Server se data ko fetch/read karne ke liye. *(Eg: User profile dekhna)*
* **POST:** Server par naya data create/submit karne ke liye. *(Eg: Naya account register karna)*
* **PUT:** Server par pehle se maujood data ko poora update/replace karne ke liye.
* **PATCH:** Data ke kisi ek chhote part ko update karne ke liye. *(Eg: Sirf phone number change karna)*
* **DELETE:** Server se kisi data ko remove karne ke liye.

## Difference

| PUT | PATCH |
|------|------|
| Full Update | Partial Update |
| Saari fields bhejni padti hain | Sirf changed fields bhejni padti hain |
| Resource replace karta hai | Specific fields update karta hai |

# Ek API "RESTful" Kab Kehlati Hai? (6 Core Constraints)
Agar kisi API ko khud ko "RESTful" bolna hai, toh use in 6 rules ko follow karna hi padta hai:

1. **Uniform Interface (Sabse Important):**
   * API ka design consistent hona chahiye. Har resource ka ek unique address/URL hona chahiye (jaise `/users`, `/orders`).
   * API standard HTTP verbs (GET, POST, PUT, DELETE) ka hi use kare.

2. **Statelessness (Bina Yaad Rakhe Kaam Karna):**
   * Server client ki pichli kisi request ki memory (session) save nahi karta. 
   * Har request apne aap me ekdum complete honi chahiye (yani har request me authentication token aur jaruri data hona hi chahiye).

3. **Client-Server Architecture:**
   * Frontend (UI) aur Backend (Database/Logic) ek dusre se puri tarah independent hone chahiye. Isse system ko scale karna asaan hota hai.

4. **Cacheability (Speed Badhana):**
   * Server ke response me yeh clearly bataya hona chahiye ki yeh data "cache" (temporarily save) kiya ja sakta hai ya nahi. Isse network bandwidth bachti hai aur app fast chalta hai.

5. **Layered System:**
   * Client aur Server ke beech me kayi layers ho sakti hain (jaise Load Balancers, Proxies, ya Security Checkpoints). Client ko bas apna kaam hone se matlab hota hai, use nahi pata hota ki woh exact kis server layer se baat kar raha hai.

6. **Code on Demand (Optional Rule):**
   * Server chahe toh client ko execute hone wala code (jaise JavaScript applets) bhi bhej sakta hai. Halanki modern APIs me iska use bohot kam hota hai.

---

# API Versioning Kaise Karte Hain?

API Versioning ka use API me changes introduce karne ke liye kiya jata hai bina existing clients ko break kiye.

API Versioning ka matlab hai apni API ko is tarah se design aur update karna ki jab aap naye features add karein ya purane code me changes karein, toh **purane clients (jo purani API use kar rahe hain) ka system break na ho.**

## Common Methods

**A. URI / URL Path Versioning (Sabse Common & Best Practice)**
* Version directly URL me likha hota hai. Yeh dekhne aur samajhne me sabse asaan hota hai.
* *Example:* 
  * `GET https://api.mysite.com/v1/users`
  * `GET https://api.mysite.com/v2/users`

**B. Query Parameter Versioning**
* Isme version ko URL ke end me ek query ki tarah bheja jata hai.
* *Example:* `GET https://api.mysite.com/users?version=2`

**C. Custom Header Versioning**
* URL same rehta hai, par client request bhejte waqt **Header** me version mention karta hai.
* *Example:* 
  * URL: `GET https://api.mysite.com/users`
  * Header: `X-API-Version: 2`

**D. Content Negotiation (Accept Header)**
* URL same rehta hai, client HTTP `Accept` header ka use karke specify karta hai ki use kaun sa version chahiye.
* *Example:* `Accept: application/vnd.mysite.v2+json`

## Interview Answer

API Versioning ka use backward compatibility maintain karne ke liye kiya jata hai. Sabse common approach URL Versioning hai, jaise `/api/v1/users/` aur `/api/v2/users/`, jisse naye changes add kar sakte hain bina existing clients ko affect kiye.


# Filtering, Searching, Sorting Kaise Implement Karoge?

API design me Filtering, Searching aur Sorting ko query parameters ke through implement kiya jata hai.

## Filtering

Specific records fetch karne ke liye.

```http
GET /users?department=IT
GET /users?status=active
GET /users?department=IT&status=active
```

## Searching

Keyword ke basis par records search karne ke liye.

```http
GET /users?search=bittu
```

Ya

```http
GET /users?q=bittu
```

## Sorting

Data ko ascending ya descending order me return karne ke liye.

```http
GET /users?sort=name
GET /users?sort=-created_at
```

Yahan `-` descending order ko represent karta hai.

## Best Practice

Ek hi API me tino support kar sakte hain:

```http
GET /users?department=IT&search=bittu&sort=-created_at
```

## Interview Answer

API design me Filtering, Searching aur Sorting ko generally query parameters ke through implement kiya jata hai. Filtering specific records ko fetch karne ke liye, Searching keyword-based lookup ke liye aur Sorting result order control karne ke liye use hoti hai. Isse API flexible aur scalable banti hai.

# Rate Limiting Kya Hoti Hai?

Rate Limiting ek technique hai jo kisi user ya client ke API requests ki maximum limit define karti hai ek specific time period ke liye.

Iska purpose:
- API abuse ko prevent karna
- DDoS attacks se protection
- Server resources ko control karna
- Fair usage ensure karna
- Server Health & Stability

## Example

Agar limit hai:

```text
100 requests / minute
```

Aur user 101st request bhejta hai, to API response de sakti hai:

```http
429 Too Many Requests
```

# Rate Limiting: Strategies, Algorithms & Implementation

## 1. Rate Limiting Ke Types (Kisko block karna hai?)
Hum API ko kis basis par limit kar rahe hain, iske 2 main tarike hote hain:

* **User Based Rate Limiting:** 
  * *Limit:* Eg: 100 requests/minute per user.
  * *Purpose:* Yeh **Authenticated users** (jo login kar chuke hain) ke liye hota hai. API inko inke User ID ya Auth Token (JWT) se pehchanti hai.
* **IP Based Rate Limiting:** 
  * *Limit:* Eg: 50 requests/minute per IP.
  * *Purpose:* Yeh **Anonymous users** (bina login wale) ke liye hota hai. API unko unke internet connection (IP Address) se pehchanti hai.

---

## 2. Rate Limiting Algorithms (Dono me kya fark hai?)
Production systems me request count track karne ke liye mainly yeh 2 algorithms use hote hain:

### A. Token Bucket Algorithm (Allows Bursts)
* **Concept:** Ek virtual bucket (balti) hoti hai jisme lagatar 'tokens' aate rehte hain. Jab bhi koi request aati hai, woh ek token le leti hai aur process ho jati hai.
* **Fark (Difference):** Agar bucket me 10 tokens ikhatte ho gaye hain, toh user achanak se ek second me 10 requests bhej sakta hai (isko **burst** kehte hain). Agar tokens khatam ho gaye, toh baaki requests block ho jayengi.
* *Use Case:* Jab aap chahte hain ki user thode time ke liye speed me requests bhej sake, par overall limit cross na kare.

### B. Leaky Bucket Algorithm (Constant Flow)
* **Concept:** Ek bucket jisme niche ek chhed (hole) hai. Requests upar se kisi bhi speed me aa sakti hain, par process sirf ek **fixed (constant) speed** se hi hongi (jaise paani ka leak hona).
* **Fark (Difference):** Isme burst allow nahi hota. Chahe aap ek sath 100 requests bhej do, server unhe queue me daal dega aur ek-ek karke aaram se process karega. Agar queue (bucket) bhar gayi, toh nayi aane wali requests drop (reject) ho jayengi.
* *Use Case:* Jab aap chahte hain ki aapke server par hamesha ek constant load rahe, achanak se koi spike na aaye.

---

## 3. Production me Isko Kaise Banate Hain? (Implementation)
Real-world projects me rate limiting implement karne ke liye **Redis + Middleware** ka combination sabse zyada use hota hai.

* **Redis Ka Use:** Redis ek in-memory database hai jo bohot fast hota hai. Hum har user ka request count (aur time) Redis me store karte hain.
* **Middleware Ka Use:** Backend me ek interceptor (middleware) lagate hain. Jab bhi koi nai request aati hai, middleware pehle Redis se count check karta hai. Agar limit cross nahi hui hai toh request aage bhej deta hai, warna turant **`429 Too Many Requests`** error return kar deta hai.

## Interview Answer

Rate Limiting ek mechanism hai jo ek user ya client ki requests ko specific time period me limit karta hai. Iska use API abuse aur server overload ko prevent karne ke liye hota hai. Isse user/IP based limits, Redis caching, ya Token Bucket jaise algorithms ke through implement kiya ja sakta hai. Limit exceed hone par API `429 Too Many Requests` response return karti hai.

# JWT (JSON Web Token) Complete Flow

JWT ek authentication mechanism hai jisme user login ke baad ek token receive karta hai aur us token ke through protected APIs access karta hai.

## JWT Flow

### 1. User Login Karta Hai

```http
POST /login
```

Request:

```json
{
    "username": "bittu",
    "password": "password123"
}
```

---

### 2. Server Credentials Verify Karta Hai

- Username/password database se verify hote hain.
- Agar valid hain to JWT token generate hota hai.

---

### 3. Server JWT Token Return Karta Hai

```json
{
    "access_token": "eyJhbGciOiJIUzI1NiIs...",
    "refresh_token": "eyJhbGciOiJIUzI1NiIs..."
}
```

---

### 4. Client Token Store Karta Hai

Commonly:
- Local Storage
- Session Storage
- HttpOnly Cookie

---

### 5. Protected API Call

Client har request ke saath token bhejta hai.

```http
GET /api/profile

Authorization: Bearer <access_token>
```

---

### 6. Server Token Verify Karta Hai

Server check karta hai:

- Token valid hai ya nahi
- Signature valid hai ya nahi
- Expire to nahi hua

Agar valid hai to request allow kar deta hai.

---

### 7. Token Expire Ho Jata Hai

Access token generally short-lived hota hai.

Example:

```text
Access Token: 15 minutes
Refresh Token: 7 days
```

---

### 8. Refresh Token Se Naya Access Token

```http
POST /token/refresh
```

Request:

```json
{
    "refresh": "<refresh_token>"
}
```

Response:

```json
{
    "access": "<new_access_token>"
}
```

User ko dobara login karne ki zarurat nahi padti.

---

# 2. JWT Ke 3 Main Components (JWT Structure)

### A. Header (`xxxxx`)
Header token ka "Metadata" hota hai. Yeh server ko batata hai ki is token ko read aur verify kaise karna hai.
Isme mainly 2 cheezein hoti hain:
1. **Type of Token:** Jo ki hamesha "JWT" hota hai.
2. **Algorithm (alg):** Kaunsa encryption/hashing algorithm use hua hai signature banane ke liye (jaise **HMAC SHA256** ya **RSA**).

*Example (JSON me):*
{
  "alg": "HS256",
  "typ": "JWT"
}
*(Is JSON ko **Base64Url** me encode karke JWT ka pehla hissa banaya jata hai).*

### B. Payload (`yyyyy`)
Yeh token ka sabse main part hai jisme actual data (user ki details) hota hai. Is data ko **"Claims"** kaha jata hai.
Claims 3 type ke hote hain:
1. **Registered Claims:** Predefined data jaise `exp` (Expiry time), `iat` (Issued at time), `sub` (Subject).
2. **Public/Private Claims:** Custom data jo hum khud add karte hain jaise `user_id`, `role` (admin/user), `email`.

*Example (JSON me):*
{
  "sub": "1234567890",
  "name": "Rahul",
  "role": "admin",
  "exp": 1712345678
}
*(Is JSON ko bhi **Base64Url** me encode karke JWT ka dusra hissa banaya jata hai).*

🚨 **Warning / Interview Tip:** Payload sirf **Encoded** hota hai, **Encrypted nahi!** Koi bhi insaan base64 decoder use karke payload ka data padh sakta hai. Isliye isme **kabhi bhi sensitive data (jaise Password ya Credit Card Info) nahi dalna chahiye.**

### C. Signature (`zzzzz`)
Yeh token ka **Security Guard** hai. Signature yeh guarantee deta hai ki raaste me kisi hacker ne token ka data (payload) change nahi kiya hai.

**Signature kaise banta hai?**
Server encoded Header aur encoded Payload ko leta hai, aur usme apna ek **Secret Key** (jo sirf server ko pata hota hai) mila kar us algorithm se hash karta hai jo Header me likha tha.

*Formula:*
`HMACSHA256( base64UrlEncode(header) + "." + base64UrlEncode(payload), SECRET_KEY )`

---

## Interview Answer

JWT ek stateless authentication mechanism hai. User login karta hai, server credentials verify karke access aur refresh token generate karta hai. Client access token ko har request ke Authorization header me bhejta hai. Server token verify karke request authorize karta hai. Access token expire hone par refresh token se naya access token generate kiya jata hai bina user ko dobara login karwaye.


# Access Token aur Refresh Token me Difference

## Access Token

- Protected APIs access karne ke liye use hota hai.
- Har request ke saath send kiya jata hai.
- Short expiry time hoti hai (e.g. 15-30 minutes).
- Expire hone ke baad API access nahi kar sakte.

## Refresh Token

- Naya Access Token generate karne ke liye use hota hai.
- Har API request me send nahi kiya jata.
- Long expiry time hoti hai (e.g. 7-30 days).
- User ko dobara login karne se bachata hai.

## Difference

| Access Token | Refresh Token |
|-------------|---------------|
| API access ke liye use hota hai | Naya Access Token generate karne ke liye |
| Short-lived | Long-lived |
| Har request me bheja jata hai | Sirf token refresh ke time use hota hai |
| Compromise hone par limited risk | Compromise hone par zyada risk |

## Interview Answer

Access Token protected APIs ko access karne ke liye use hota hai aur iski expiry short hoti hai. Refresh Token ka use naya Access Token generate karne ke liye hota hai aur iski expiry longer hoti hai. Is approach se security aur user experience dono improve hote hain.

# RBAC (Role Based Access Control) Kya Hota Hai?

RBAC ek authorization mechanism hai jisme permissions directly users ko assign karne ke bajay roles ko assign ki jati hain.

## Example

```text
Admin
 ├── Create User
 ├── Update User
 └── Delete User

Manager
 ├── View User
 └── Update User

Employee
 └── View User
```

User ko role diya jata hai aur role ke according permissions mil jati hain.

## Interview Answer

RBAC ek access control mechanism hai jisme users ko roles assign kiye jate hain aur permissions roles ke through manage hoti hain. Isse permission management easy aur scalable ho jata hai.

---

# OAuth2 Kya Hai?

OAuth2 ek authorization framework hai jo kisi third-party application ko user ka password share kiye bina limited access provide karta hai.
OAuth2 (Open Authorization 2.0) ek aisa standard protocol hai jo ek application ko bina aapka password jaane, aapke data ka mahdoos (limited) access dene ki ijazaat deta hai.

**OAuth2** ek industry-standard framework hai jo **"Delegated Authorization"** ke liye use hota hai.

## Example

```text
Login with Google
Login with GitHub
Login with Facebook
```
## OAuth2 Kaam Kaise Karta Hai? (The Flow)
Maan lijiye aap **Canva** (Client) par **Google** ke zariye login/signup kar rahe hain:

* **Step 1:** Aap Canva par "Continue with Google" par click karte hain.
* **Step 2:** Canva aapko redirect karke **Google ke Authorization Server** par bhej deta hai.
* **Step 3 (Consent Screen):** Google aapse puchta hai: *"Canva wants to access your Name, Email, and Profile Picture. Do you allow?"* Aap "Allow" par click karte hain.
* **Step 4 (Auth Code):** Google Canva ko ek secret **"Authorization Code"** bhejta hai.
* **Step 5 (Access Token):** Canva apne backend se us code ko Google ke paas bhejta hai aur badle me ek **"Access Token"** (aur kabhi-kabhi Refresh Token) mangta hai.
* **Step 6 (Data Access):** Ab Canva us Access Token ka use karke **Google ke Resource Server** se aapki profile detail (Email, Name) fetch kar leta hai.

## Architecture Ke 4 Main Pillars (Components)
OAuth2 ka pura architecture in 4 entities ke aas-paas ghumta hai:
1. **Resource Owner:** Aap (User).
2. **Client:** Woh App jo data access karna chahti hai (e.g., Spotify).
3. **Authorization Server:** Woh server jo user ka login verify karke Token deta hai (e.g., Google Auth Server).
4. **Resource Server:** Woh server jahan user ka actual data/API rakhi hai (e.g., Google Contacts API).

## 2. Standard Architecture Flow (Step-by-Step)
Sabse common aur secure flow ko **"Authorization Code Flow"** kehte hain. Iska architecture sequence kuch aisa dikhta hai:

**[ Client ]  ---- (1. Request Login) ----> [ Authorization Server ]**
* **Step 1:** Client (Spotify) user ko Authorization Server (Google) par bhejta hai. (Sath me apna `client_id` aur `redirect_uri` bhejta hai).

**[ Auth Server ] ---- (2. Ask Permission) ----> [ Resource Owner ]**
* **Step 2:** Google user ko ek "Consent Screen" dikhata hai ki *"Spotify wants your email"*. 

**[ Resource Owner ] ---- (3. Grants Access) ----> [ Auth Server ]**
* **Step 3:** User "Allow" (Yes) par click karta hai.

**[ Auth Server ] ---- (4. Sends Auth Code) ----> [ Client's Backend ]**
* **Step 4:** Google ek temporary **"Authorization Code"** Spotify ke backend ko bhejta hai (via Redirect URI). *Dhyan rahe, abhi token nahi mila hai!*

**[ Client's Backend ] ---- (5. Exchange Code for Token) ----> [ Auth Server ]**
* **Step 5:** Spotify ka backend us *Auth Code* aur apne *Client Secret* ko wapas Google ko bhejta hai. (Yeh backend-to-backend hota hai taaki secure rahe).

**[ Auth Server ] ---- (6. Sends Tokens) ----> [ Client's Backend ]**
* **Step 6:** Google verify karta hai aur final **Access Token** (aur Refresh Token) bhej deta hai.

**[ Client's Backend ] ---- (7. Fetch Data) ----> [ Resource Server ]**
* **Step 7:** Ab Spotify us Access Token ko HTTP header (`Authorization: Bearer <token>`) me daalkar Google Resource Server se data (email) fetch kar leta hai.

## Interview Answer

OAuth2 ek authorization framework hai jo third-party applications ko user ke resources access karne ki permission deta hai bina user credentials share kiye. Isme access tokens ka use hota hai.

---

# SSO (Single Sign-On) Kya Hota Hai?

SSO ek authentication mechanism hai jisme user ek baar login karta hai aur multiple applications access kar sakta hai bina baar-baar login kiye.Ek hi login se sab applications access ho jati hain.

## Example

```text
Google Login
    ↓
Gmail
Google Drive
Google Docs
Google Meet
```

# SSO (Single Sign-On) Architecture & Working - Interview Notes

## 1. SSO Architecture Ke 3 Main Components
SSO ka poora system in 3 pillars par khada hota hai. Interview me inhe zaroor mention karein:

1. **User (The Principal):** Aap aur aapka web browser jo apps access karna chahta hai.
2. **Service Provider (SP):** Woh application jise user use karna chahta hai. (Jaise Slack, Jira, ya Canva).
3. **Identity Provider (IdP):** Yeh central SSO server hota hai jiske paas user ke passwords aur details hoti hain. Yeh user ko verify karta hai. (Jaise Okta, Auth0, Microsoft Entra, ya Google Workspace).

---

## 2. SSO Kaam Kaise Karta Hai? (Step-by-Step Flow)
Maan lijiye aapki company me **Okta** (IdP) use hota hai aur aap **Slack** (SP 1) aur **Jira** (SP 2) access karna chahte hain.

### Phase 1: Pehli App Me Login (Slack)
**[ User ] ---- (1. Access Slack) ----> [ Slack (SP 1) ]**
* **Step 1:** Aap browser me Slack open karte hain. Slack dekhta hai ki aapke paas valid session nahi hai.

**[ Slack ] ---- (2. Redirect to IdP) ----> [ Okta (IdP) ]**
* **Step 2:** Slack aapko login karne ke liye Okta (IdP) par redirect kar deta hai.

**[ User ] ---- (3. Enter Credentials) ----> [ Okta ]**
* **Step 3:** Okta aapse aapka Username aur Password mangta hai. Aap daalte hain.

**[ Okta ] ---- (4. Create Cookie & Token) ----> [ User's Browser ] ----> [ Slack ]**
* **Step 4 (The Most Important):** Okta login verify karta hai. 
  * Fir Okta aapke browser me apne domain ki ek **Session Cookie** save kar deta hai (Yeh yaad rakhne ke liye ki aap Okta par logged in hain). 
  * Sath hi, Okta ek **SSO Token** (SAML ya OIDC JWT) Slack ko bhejta hai.
* **Step 5:** Slack us token ko verify karta hai aur aapko andar aane deta hai. Aap Slack me logged in hain!

---

### Phase 2: Dusri App Me Login (Jira - The SSO Magic)
Ab aap apna kaam karne ke liye naye tab me Jira kholte hain.

**[ User ] ---- (1. Access Jira) ----> [ Jira (SP 2) ]**
* **Step 1:** Jira dekhta hai aap logged in nahi hain. Jira aapko phir se Okta (IdP) par redirect karta hai.

**[ Jira ] ---- (2. Redirect) ----> [ Okta (IdP) ]**
* **Step 2:** Jaise hi request Okta par pahunchti hai, Okta ka server aapke browser ki **Session Cookie** (jo pehle step me bani thi) read kar leta hai.

**[ Okta ] ---- (3. Silent Verification) ----> [ Jira ]**
* **Step 3:** Okta ko pata chal jata hai ki *"Arre, yeh user toh pehle se verify ho chuka hai!"* 
* Isliye Okta aapse login form nahi dikhata, aur seedha **Jira ke liye ek naya SSO Token** bhej deta hai.
* **Step 4:** Jira token verify karta hai aur aapko andar aane deta hai. 
* **Result:** Bina password daale aap Jira me login ho gaye!

---

## Interview Answer

SSO ek authentication process hai jisme user ek baar authenticate hota hai aur uske baad multiple applications ya services ko bina dobara login kiye access kar sakta hai.

# Authentication aur Authorization me Difference

## Authentication

Authentication verify karta hai ki user **kaun hai**.

### Example

```text
Username + Password
JWT Token
OTP
Fingerprint
```

User ki identity verify ki jati hai.

---

## Authorization

Authorization decide karta hai ki authenticated user **kya kar sakta hai**.

### Example

```text
Admin → Create, Update, Delete
Employee → View Only
```

User ke permissions aur access rights check kiye jate hain.

---

## Difference

| Authentication | Authorization |
|---------------|---------------|
| User ki identity verify karta hai | User ke permissions verify karta hai |
| "Who are you?" | "What can you do?" |
| Login process ka part hai | Access control ka part hai |
| Authorization se pehle hota hai | Authentication ke baad hota hai |

## Interview Answer

Authentication user ki identity verify karta hai, yani user kaun hai. Authorization determine karta hai ki authenticated user ko kaunse resources ya actions perform karne ki permission hai. Authentication pehle hota hai, uske baad Authorization.

# Redis Kya Hai?

Redis (Remote Dictionary Server) ek open-source, in-memory key-value data store hai jo bahut fast hota hai kyunki data RAM me store karta hai.

**Redis** ka full form **Remote Dictionary Server** hai. Yeh ek **Open-source, In-memory Data Structure Store** hai.

* **In-memory:** Iska matlab hai ki Redis data ko hard-disk (SSD/HDD) ki jagah **RAM** me store karta hai.
* **Result:** RAM me hone ki wajah se Redis bohot zyada fast hai (microsecond response time). 
* Yeh sirf ek simple database nahi hai, balki yeh **Cache**, **Message Broker**, aur **Database** teeno ki tarah kaam kar sakta hai.

## Redis Kyu Use Karte Hain?

### 1. Caching
Frequently used data cache karne ke liye taaki database hits kam ho aur response fast mile.

### 2. Session Storage
User sessions ko store karne ke liye.

### 3. Rate Limiting
API request counts track karne ke liye.

### 4. Message Queue
Background tasks aur asynchronous processing ke liye (Celery + Redis).

### 5. Real-time Applications
Chat applications, notifications, live counters, leaderboards, etc.

## Example

Without Redis:

```text
User Request
    ↓
Database Query
    ↓
Response
```

With Redis:

```text
User Request
    ↓
Redis Cache
    ↓
Response

(Cache miss hone par DB se fetch karke Redis me store kar dete hain)
```

# Redis Architecture & Working Mechanism

## 1. Redis Ka Architecture (Single-Threaded Event Loop)
Redis ka sabse bada architecture design feature uska **"Single-threaded event loop"** hai. 

* **Single-Threaded Model:** Purane databases multi-threading use karte hain (jisme locking/unlocking ki wajah se complexity badh jati hai). Redis ka core (Command processing) single-threaded hota hai, jiska matlab hai ki yeh ek baar me ek hi request execute karta hai. 
* **Event Loop (I/O Multiplexing):** Yeh `epoll` ya `kqueue` jaise mechanisms ka use karta hai. Iska fayda yeh hai ki Redis ek sath hazaron connections ko handle kar sakta hai bina kisi wait ke, kyunki memory access bohot fast hoti hai.

---

## 2. Redis Kaam Kaise Karta Hai? (Working Flow)

Redis ka kaam karne ka flow 3 main levels par hota hai:

### A. Memory-First Approach
Jab bhi koi client (app) command bhejti hai, Redis use direct **RAM (Main Memory)** se read/write karta hai. Kyunki RAM ki access speed SSD/HDD se kai guna zyada hoti hai, isliye Redis microsecond response deta hai.

### B. Command Execution (The Event Loop)
1. **Request:** Client command bhejta hai (e.g., `SET user:1 "Rahul"`).
2. **Queue:** Commands ek memory queue me aati hain.
3. **Execution:** Redis ka single thread apni memory me jata hai, value update karta hai, aur client ko response bhej deta hai. 
4. **Non-blocking:** Kyunki memory operations itne fast hote hain, single thread ko kabhi wait nahi karna padta.

### C. Data Persistence (Disk par backup)
Redis RAM me chalta hai, toh kya server restart hone par data udd jayega? Nahi! Redis disk par backup ke liye do methods use karta hai:
* **RDB (Redis Database Backup):** Yeh specific time intervals par (e.g., har 5 minute me) RAM ka poora Snapshot disk par save kar deta hai.
* **AOF (Append Only File):** Yeh har ek write command ko ek file me likhta rehta hai. Agar server crash ho jaye, toh Redis is file ko replay karke data wapas restore kar leta hai.

---

## 3. Advanced Architecture: Redis Modes
Interview me architecture ke baare me pucha jaye toh ye 3 modes zaroor batana:

1. **Standalone Mode:** Single Redis server. (Simple but not scalable).
2. **Redis Replication (Master-Slave):** Ek **Master** (jo write handle karta hai) aur kayi **Slaves** (jo sirf read handle karte hain). Agar Master down hua, toh hum Slave ko promote kar sakte hain.
3. **Redis Cluster (Scalable):** Isme data ko multiple servers (shards) me divide kar diya jata hai. Yeh architecture bahut badi applications (jaise Twitter/Instagram) me use hota hai jahan data bahut zyada ho.

---

## 4. Key Takeaways (Interview Points)
* **No Locking:** Single-threaded hone ki wajah se Redis me "Locking" (deadlock) ka jhanjhat nahi hota.
* **Rich Data Structures:** Redis sirf `String` nahi store karta, balki `List`, `Hash`, `Set`, aur `Sorted Set` bhi karta hai, jo server-side processing ko asaan banate hain.
* **Speed:** Kyunki disk I/O ka wait nahi karna padta, isliye performance consistency bani rehti hai.

> 💡 **Pro Interview Tip:**
> Agar interviewer puche: *"Agar Redis single-threaded hai, toh kya yeh multi-core CPU ka fayda nahi utha paata?"*
> **Aapka Answer:** *"Sir, Redis ka core command processing single-threaded hai, par hum ek hi machine par multiple Redis instances chala kar multi-core CPU ka pura use kar sakte hain. Iske alawa, Redis 6.0 ke baad se 'IO Threading' introduce kiya gaya hai, jo network read/write (I/O) ko multi-thread kar deta hai, lekin command processing abhi bhi single-thread hi rehti hai."*

## Interview Answer

Redis ek in-memory key-value data store hai jo extremely fast read/write operations provide karta hai. Iska use caching, session management, rate limiting, message queues aur real-time applications ke liye kiya jata hai taaki application performance improve ho aur database load kam ho.

# Apache Kafka - Interview Notes

## 1. Kafka Kya Hai? (What is it?)
**Apache Kafka** ek **Distributed Event Streaming Platform** hai. 
Simple bhasha me: Yeh ek bohot hi fast aur robust **"Message Queue"** ya **"Pub-Sub System"** ki tarah kaam karta hai, jo ek jagah se data (events) ko dusri jagah par real-time me transfer karta hai.

* **High Throughput:** Kafka ek second me lakho messages handle kar sakta hai.
* **Scalable:** Aap bahut saare servers (brokers) jod kar iski capacity badha sakte hain.
* **Durable:** Kafka data ko disk par store karta hai, isliye agar system crash ho jaye toh data loss nahi hota.

---

## 2. Kafka Ka Core Concept (Analogy)
Isko ek **News Agency** ki tarah samjho:
* **Producers (News Reporters):** Jo news (messages) generate karte hain aur Kafka me bhejte hain.
* **Topics (News Categories):** Kafka me messages "Topics" me divide hote hain (e.g., 'Payments', 'Orders', 'User-logs').
* **Consumers (News Readers):** Jo in topics ko subscribe karte hain aur messages ko read karte hain.
* **Brokers (Kafka Servers):** Yeh wo servers hain jo messages ko store aur distribute karte hain.

---

## 3. Kafka Architecture & Key Terms (VVI)
Interviewer technical depth check karne ke liye ye terms zaroor puchega:

* **Broker:** Kafka cluster ka ek server. 
* **Topic:** Messages ki category (Jaise ek folder).
* **Partition:** Har topic ko chhote-chhote hisson me baanta jata hai jise 'Partition' kehte hain. Yeh Kafka ki **Parallel Processing** ka raaz hai. (Different consumers alag-alag partition se data read kar sakte hain).
* **Offset:** Partition me har message ka ek unique ID/Number hota hai, jise 'Offset' kehte hain. Consumer track karta hai ki usne kaha tak data padh liya hai.
* **Consumer Group:** Jab kayi consumers milkar ek hi topic se data padhte hain (taaki kaam jaldi ho), unhe 'Consumer Group' kehte hain.

---

## 4. Kafka Kyun Use Karte Hain? (Use Cases)
1. **Activity Tracking:** User ki website par clicks aur movements ko track karne ke liye.
2. **Log Aggregation:** Saare servers ke logs ko ek jagah jama karna.
3. **Microservices Communication:** Jab ek service ko dusri service ko batana ho ki "Order create ho gaya", toh Kafka ka use hota hai.
4. **Real-time Analytics:** Data aate hi process karke dashboard update karna.

---

## 5. Kafka vs RabbitMQ (Common Interview Question)
* **Kafka:** Yeh 'Log-based' hai. Data ko store karke rakhta hai (aap purana data dobara read kar sakte ho). Yeh **Heavy Data** ke liye best hai.
* **RabbitMQ:** Yeh 'Message-based' hai. Ek baar message read ho gaya, toh wo queue se delete ho jata hai. Yeh **Complex Routing** ke liye best hai.

---

> 💡 **Pro Interview Tip:**
> Agar interviewer puche: *"Kafka me data delete kyun nahi hota message read hone ke baad?"*
> **Aapka Answer:** *"Sir, Kafka ek **'Distributed Commit Log'** hai. Yeh data ko tab tak store karke rakhta hai jab tak uski **Retention Period** (e.g., 7 days) khatam nahi ho jati. Iska fayda yeh hai ki hum kabhi bhi purana data dobara 're-process' kar sakte hain agar koi bug mil jaye."*

# RabbitMQ vs Kafka

| RabbitMQ | Kafka |
|-----------|--------|
| Message Broker | Event Streaming Platform |
| Queue Based | Topic Based |
| Low to Medium Throughput | Very High Throughput |
| Message delivery par focus | Event streaming par focus |
| Background tasks ke liye best | Real-time data streaming ke liye best |
| Message consume hone ke baad remove ho jata hai | Messages configurable time tak retain rehte hain |

## Interview Answer

RabbitMQ aur Kafka dono messaging systems hain, lekin RabbitMQ traditional message queue hai jo reliable task processing ke liye use hota hai, jabki Kafka high-throughput distributed event streaming platform hai jo real-time data pipelines aur analytics ke liye use hota hai.

# Monolith vs Microservices

## Monolithic Architecture

Monolithic architecture me poora application ek hi codebase aur ek hi deployment unit me hota hai.

### Example

```text
E-Commerce Application

├── User Module
├── Product Module
├── Order Module
├── Payment Module
└── Notification Module

(Sab ek hi application ke andar)
```

### Advantages

- Development simple hoti hai.
- Deployment easy hota hai.
- Small projects ke liye suitable.

### Disadvantages

- Application badi hone par maintain karna difficult ho jata hai.
- Ek chhota change ke liye poori application deploy karni padti hai.
- Scaling granular level par nahi kar sakte.

---

## Microservices Architecture

Microservices me application ko multiple independent services me divide kar diya jata hai.

### Example

```text
User Service
Product Service
Order Service
Payment Service
Notification Service
```

Har service:
- Apna codebase rakh sakti hai.
- Apna database rakh sakti hai.
- Independently deploy ho sakti hai.
- Independently scale ho sakti hai.

### Advantages

- Better scalability
- Independent deployment
- Easy maintenance
- Fault isolation

### Disadvantages

- System complexity badh jati hai.
- Service communication manage karna padta hai.
- Monitoring aur debugging difficult ho sakti hai.

---

## Interview Answer

Monolithic architecture me poora application ek single codebase aur deployment unit hota hai, jabki Microservices architecture me application ko multiple independent services me divide kiya jata hai jo independently develop, deploy aur scale ki ja sakti hain.

---

# Load Balancer Kya Hota Hai?

Load Balancer ek component hota hai jo incoming requests ko multiple servers me distribute karta hai.

## Without Load Balancer

```text
Users
   ↓
Server-1

10000 Requests
↓
Server Crash
```

Saara load ek hi server par aa raha hai.

---

## With Load Balancer

```text
Users
   ↓
Load Balancer
   ↓
 ┌─────────┬─────────┬─────────┐
 ↓         ↓         ↓
Server-1  Server-2  Server-3
```

Requests multiple servers me distribute ho jati hain.

---

## Benefits

### High Availability

Agar ek server down ho jaye:

```text
Server-1 ❌

Load Balancer
     ↓
Server-2 ✅
Server-3 ✅
```

Application phir bhi available rahegi.

### Better Performance

Load evenly distribute hota hai.

### Scalability

Naye servers easily add kar sakte hain.

---

## Interview Answer

Load Balancer incoming requests ko multiple servers me distribute karta hai taaki system par load balance rahe, performance improve ho aur high availability maintain rahe.

---

# Horizontal Scaling vs Vertical Scaling

Scaling ka matlab system ki capacity badhana.

---

## Vertical Scaling (Scale Up)

Existing server ki power increase karna.

### Example

```text
Before:
4 CPU
8 GB RAM

After:
16 CPU
64 GB RAM
```

Server wahi hai, sirf resources badh gaye.

### Advantages

- Easy implementation
- Application changes ki zarurat nahi

### Disadvantages

- Hardware limit aa jati hai.
- Single point of failure.

---

## Horizontal Scaling (Scale Out)

Naye servers add karna.

### Example

```text
Before

Server-1
```

```text
After

Server-1
Server-2
Server-3
Server-4
```

Usually Load Balancer ke saath use hoti hai.

### Advantages

- Practically unlimited scaling
- High availability
- Fault tolerance

### Disadvantages

- Architecture complex ho jati hai.

---

## Comparison

| Vertical Scaling | Horizontal Scaling |
|------------------|-------------------|
| Server ko powerful banate hain | Naye servers add karte hain |
| Limited scalability | High scalability |
| Single point of failure | High availability |
| Easy | More complex |

---

## Interview Answer

Vertical Scaling me existing server ke CPU, RAM ya resources increase kiye jate hain, jabki Horizontal Scaling me multiple servers add kiye jate hain aur load unme distribute kiya jata hai. Large-scale applications generally Horizontal Scaling prefer karti hain.

---

# Stateless API Kya Hoti Hai?

Stateless API wo API hoti hai jahan server client ki previous request ka state store nahi karta.

Har request independent hoti hai aur apne saath saari required information lekar aati hai.

---

## Example

### Stateless API

```http
GET /api/profile

Authorization: Bearer xyz123
```

Har request me token bheja ja raha hai.

Server ko yaad rakhne ki zarurat nahi ki user pehle login kar chuka tha.

---

### Stateful System

```text
Login
 ↓
Server Session Store
 ↓
Profile Request
 ↓
Server Session Check
```

Server session maintain karta hai.

---

## Stateless API Benefits

### Easy Scaling

Koi bhi server request process kar sakta hai.

```text
Load Balancer
      ↓
Server-1
Server-2
Server-3
```

Sab servers independently kaam kar sakte hain.

### Better Performance

Session management overhead nahi hota.

### Fault Tolerance

Ek server down ho jaye to dusra request handle kar sakta hai.

---

## Real Example

JWT Authentication

```http
Authorization: Bearer eyJhbGciOi...
```

Token me hi user information hoti hai.

Server ko session maintain nahi karna padta.

---

## Interview Answer

Stateless API me server client ki previous requests ka state store nahi karta. Har request independent hoti hai aur apne saath required information, jaise JWT token, lekar aati hai. Is approach se APIs scalable, performant aur distributed environments ke liye suitable banti hain.

# Process Kya Hai?

Process ek running program hota hai jiska apna memory space, resources aur execution environment hota hai.

### Example

Agar aap Chrome aur VS Code open karte ho:

```text
Chrome      → Process-1
VS Code     → Process-2
Python App  → Process-3
```

Har process apni memory use karta hai aur ek dusre se isolated hota hai.

## Features

- Apna memory space hota hai.
- Ek process crash ho jaye to dusre process par impact nahi padta.
- Process creation relatively expensive hoti hai.

## Interview Answer

Process ek running instance of program hota hai jiska apna memory space aur system resources hote hain. Operating System processes ko independently manage karta hai.

---

# Thread Kya Hai?

Thread process ke andar execution ki smallest unit hoti hai.

Ek process ke multiple threads ho sakte hain.

### Example

```text
Process (Web Application)

├── Thread-1
├── Thread-2
├── Thread-3
└── Thread-4
```

Sab threads process ki memory share karte hain.

## Features

- Lightweight hote hain.
- Fast create hote hain.
- Shared memory use karte hain.
- Concurrent execution possible hoti hai.

## Real Example

Web Server:

```text
Request-1 → Thread-1
Request-2 → Thread-2
Request-3 → Thread-3
```

Ek hi process multiple requests handle kar sakta hai.

---

# Process vs Thread

| Process | Thread |
|----------|---------|
| Independent execution unit | Process ke andar execution unit |
| Apni memory hoti hai | Shared memory use karta hai |
| Heavyweight | Lightweight |
| Creation expensive | Creation fast |
| More isolated | Less isolated |

## Interview Answer

Process ek independent running program hota hai jiska apna memory space hota hai, jabki Thread process ke andar execution unit hoti hai jo process ki memory share karti hai. Threads lightweight aur faster hote hain.

---

# Celery - Background Task Queue (Interview Notes)

## 1. Celery Kya Hai? (What is it?)
Celery ek **Asynchronous Task Queue/Job Queue** hai jo Python me likha gaya hai. 
Iska main kaam hai "Heavy" ya "Time-consuming" tasks ko main application thread se alag karke background me execute karna.

* **Simple Words:** Agar aapka web server kisi aise kaam me lag jaye jisme der lag rahi hai (jaise Email bhejna, PDF generate karna, ya Machine Learning model chalana), toh aapki website **hang (slow)** ho jayegi. Celery aise kaam ko background worker ko सौंप (assign) deta hai aur server turant user ko response bhej deta hai.

---

## 2. Yeh Kaam Kaise Karta Hai? (Architecture)
Celery ka architecture 3 main components par depend karta hai:

1. **Producer (Client):** Aapka Django/FastAPI app, jo task banata hai.
2. **Message Broker:** Celery task ko directly execute nahi karta, balki use ek "Broker" me daal deta hai. Broker task ko hold karke rakhta hai. (Sabse popular brokers: **Redis** ya **RabbitMQ**).
3. **Worker:** Yeh alag se chalne wale processes hote hain. Yeh Broker se task uthate hain aur execute karte hain.

---

## 3. Celery Ka Workflow (Example)
Maan lijiye user "Signup" karta hai:
1. User ne button dabaya.
2. App ne database me user save kiya.
3. App ne `send_welcome_email.delay()` command chala di. (Yahan `.delay()` matlab hai: *Bhai, ye kaam background me kar dena, mujhe mat batana*).
4. App turant user ko "Signup Successful" ka message dikha deti hai.
5. Celery Worker background me broker se email wala task uthata hai aur email bhej deta hai.

---

## 4. Celery Kyun Zaruri Hai? (Use Cases)
* **Email/SMS Sending:** External API call karne me time lagta hai, isliye background me hona chahiye.
* **Data Processing:** CSV file import karna ya badi images resize karna.
* **Scheduled Tasks (Celery Beat):** Kisi specific time par kaam karna (jaise har raat 12 baje report generate karna).
* **Third-Party API calls:** External services (jaise Payment Gateways) ka response slow ho sakta hai, ise sync me nahi karna chahiye.

---

## 5. Celery vs Message Queue
Interviewer puch sakte hain ki *Celery kya khud broker hai?*
**Answer:** Nahi, Celery sirf ek **Framework/Library** hai jo task manage karti hai. Use message store karne ke liye ek Broker (Redis/RabbitMQ) ki zaroorat padti hai.

---

> 💡 **Pro Interview Tip:**
> Agar interviewer puche: *"Celery Beat kya hai?"*
> **Aapka Answer:** *"Celery Beat ek 'Scheduler' hai. Yeh Celery ka hi hissa hai jo tasks ko periodic intervals (eg: har 10 minute me) par trigger karne ke liye use hota hai. Bina Beat ke, Celery sirf 'on-demand' tasks handle karta hai."*

## Interview Answer

Celery Python ka asynchronous task queue framework hai jo background tasks execute karne ke liye use hota hai. Ye Redis ya RabbitMQ jaise message brokers ke saath kaam karta hai. Celery ka use email sending, report generation, notifications aur long-running tasks ko background me execute karne ke liye kiya jata hai, jisse application ki performance aur user experience improve hoti hai.

# XSS (Cross-Site Scripting) Kya Hai?

XSS ek security vulnerability hai jisme attacker website me malicious JavaScript inject kar deta hai aur wo script dusre users ke browser me execute ho jati hai.

## Example

Suppose comment box me user ye input de:

```html
<script>
alert("Hacked")
</script>
```

Agar application input ko sanitize nahi karti, to ye script page open karne wale har user ke browser me run ho jayegi.

## Risks

- Session cookies chori kar sakta hai.
- User account hijack kar sakta hai.
- Malicious redirects kar sakta hai.
- Sensitive data steal kar sakta hai.

## Prevention

- User input sanitize karo.
- Output encoding use karo.
- HttpOnly cookies use karo.
- Content Security Policy (CSP) implement karo.

## Interview Answer

XSS (Cross-Site Scripting) ek vulnerability hai jisme attacker malicious JavaScript code inject karta hai jo dusre users ke browser me execute hota hai. Isse cookies, sessions aur sensitive data compromise ho sakta hai.

---

# CSRF (Cross-Site Request Forgery) Kya Hai?

CSRF ek attack hai jisme attacker authenticated user ki identity ka misuse karke unwanted requests perform karwa deta hai.

## Example

User banking website me login hai:

```text
bank.com
```

Attacker user ko ek malicious page open karwa deta hai:

```html
<img src="https://bank.com/transfer?amount=10000&to=hacker">
```

Browser automatically authenticated request bhej sakta hai kyunki user pehle se login hai.

Result:

```text
Money Transfer Ho Gaya
```

Bina user ki permission ke.

---

## Risks

- Unauthorized fund transfer
- Password change
- Account settings modification
- Data deletion

---

## Prevention

### CSRF Token

Har form/request ke saath unique token bhejo.

```html
<input type="hidden" name="csrf_token" value="abc123">
```

Server token verify karega.

### SameSite Cookies

Cookies ko cross-site requests me restrict karo.

### Re-authentication

Sensitive actions ke liye password dobara maango.

---

## XSS vs CSRF

| XSS | CSRF |
|------|------|
| Malicious script inject karta hai | User se unwanted request perform karwata hai |
| Browser me JavaScript execute hoti hai | Authenticated session ka misuse hota hai |
| Target user ka browser hota hai | Target application ka trust model hota hai |
| Input sanitization se prevent karte hain | CSRF token se prevent karte hain |

## Interview Answer

CSRF (Cross-Site Request Forgery) ek attack hai jisme attacker authenticated user ki identity ka misuse karke unwanted actions perform karwa deta hai. Isse bachne ke liye CSRF tokens, SameSite cookies aur proper request validation use ki jati hai.

# HTTPS Kyu Use Karte Hain?

HTTPS (HyperText Transfer Protocol Secure) HTTP ka secure version hai jo client aur server ke beech data ko encrypt karke transfer karta hai.

## Problem with HTTP

HTTP me data plain text me transfer hota hai.

```text
Client
   ↓
Username: admin
Password: 123456
   ↓
Server
```

Agar koi attacker network traffic intercept kare, to credentials dekh sakta hai.

---

## HTTPS Solution

HTTPS SSL/TLS encryption use karta hai.

```text
Client
   ↓
Encrypted Data
   ↓
Server
```

Agar koi traffic intercept bhi kare to data readable nahi hoga.

---

## HTTPS Ke Benefits

### 1. Data Encryption

Client aur server ke beech data encrypted rehta hai.

```text
Password
Credit Card
Personal Information
JWT Token
```

Secure rehte hain.

---

### 2. Data Integrity

Data transfer ke dauran modify nahi kiya ja sakta.

```text
Original Data
     =
Received Data
```

---

### 3. Authentication

SSL Certificate verify karta hai ki aap correct server se connect ho rahe ho.

```text
User
  ↓
Verified Website
```

Fake website se bachata hai.

---

## Example

Without HTTPS:

```http
http://example.com/login
```

With HTTPS:

```http
https://example.com/login
```

Browser me 🔒 (lock icon) dikhai deta hai.

---

## Interview Answer

HTTPS HTTP ka secure version hai jo SSL/TLS encryption use karke client aur server ke beech data ko securely transfer karta hai. Iska use data encryption, integrity aur server authentication ke liye kiya jata hai, jisse passwords, tokens aur sensitive information attackers se protected rehti hai.

# Multithreading vs Multiprocessing

Dono techniques ek application me concurrency aur performance improve karne ke liye use hoti hain, lekin unka working model alag hota hai.

---

# Multithreading

Multithreading me ek hi process ke andar multiple threads run karte hain.

```text
Process
├── Thread-1
├── Thread-2
├── Thread-3
└── Thread-4
```

Sab threads same memory share karte hain.

## Use Cases

- I/O Bound Tasks
- API Calls
- File Operations
- Database Queries
- Network Requests

## Advantages

- Lightweight
- Less memory usage
- Fast thread creation
- Shared data access easy

## Disadvantages

- Shared memory ki wajah se race conditions ho sakti hain.
- Python me GIL ki wajah se CPU-bound tasks me limited benefit milta hai.

---

# Multiprocessing

Multiprocessing me multiple independent processes run karte hain.

```text
Process-1
Process-2
Process-3
Process-4
```

Har process ki apni memory hoti hai.

## Use Cases

- CPU Bound Tasks
- Data Processing
- Image Processing
- Video Processing
- Machine Learning Computations

## Advantages

- True parallel execution.
- Multi-core CPUs ka full utilization.
- Ek process crash ho to dusre processes affect nahi hote.

## Disadvantages

- Zyada memory consume karta hai.
- Process creation expensive hoti hai.
- Inter-process communication complex hoti hai.

---

# Multithreading vs Multiprocessing

| Multithreading | Multiprocessing |
|---------------|----------------|
| Multiple threads in one process | Multiple independent processes |
| Memory shared hoti hai | Separate memory hoti hai |
| Lightweight | Heavyweight |
| Less memory usage | More memory usage |
| I/O-bound tasks ke liye best | CPU-bound tasks ke liye best |
| GIL se affected ho sakta hai | GIL issue nahi hota |

---

## Real Example

### Multithreading

```text
100 APIs call karni hain
```

Threads use karke multiple requests ek saath bhej sakte hain.

### Multiprocessing

```text
10 lakh records process karne hain
```

Work ko multiple CPU cores me distribute kar sakte hain.

---

## Interview Answer

Multithreading me ek process ke andar multiple threads concurrently execute hote hain aur memory share karte hain. Ye I/O-bound tasks ke liye suitable hai. Multiprocessing me multiple independent processes execute hote hain jinki alag memory hoti hai. Ye CPU-bound tasks ke liye suitable hai aur multi-core processors ka full utilization karta hai.

# select_related() vs prefetch_related()

Dono Django ORM me database queries optimize karne aur **N+1 Query Problem** ko solve karne ke liye use hote hain.

---

# select_related()

`select_related()` SQL JOIN use karta hai aur related objects ko ek hi query me fetch kar leta hai.

### Use For

- ForeignKey
- OneToOneField

### Example

```python
employees = Employee.objects.select_related("department")
```

Without `select_related()`:

```text
1 Query → Employees
100 Queries → Department

Total = 101 Queries
```

With `select_related()`:

```text
1 Query (JOIN)
```

---

# prefetch_related()

`prefetch_related()` separate queries chalata hai aur Python me data mapping karta hai.

### Use For

- ManyToManyField
- Reverse ForeignKey

### Example

```python
departments = Department.objects.prefetch_related("employees")
```

Without `prefetch_related()`:

```text
1 Query → Departments
100 Queries → Employees

Total = 101 Queries
```

With `prefetch_related()`:

```text
1 Query → Departments
1 Query → Employees

Total = 2 Queries
```

---

# Difference

| select_related() | prefetch_related() |
|------------------|-------------------|
| SQL JOIN use karta hai | Separate queries use karta hai |
| ForeignKey & OneToOne ke liye | ManyToMany & Reverse FK ke liye |
| Single query | Multiple optimized queries |
| Faster for FK relations | Better for M2M relations |

---

## Interview Answer

`select_related()` ForeignKey aur OneToOne relationships ke liye SQL JOIN use karke related data ek hi query me fetch karta hai. `prefetch_related()` ManyToMany aur Reverse ForeignKey relationships ke liye separate queries execute karta hai aur Python me results ko map karta hai. Dono ka purpose database queries ko optimize karna aur N+1 query problem ko avoid karna hai.

# Query Optimization Kaise Karte Ho?

Query Optimization ka purpose database queries ko fast banana aur unnecessary database load ko reduce karna hota hai.

## 1. select_related() Use Karna

ForeignKey aur OneToOne relationships ke liye.

```python
employees = Employee.objects.select_related("department")
```

Multiple queries ki jagah single JOIN query execute hoti hai.

---

## 2. prefetch_related() Use Karna

ManyToMany aur Reverse ForeignKey relationships ke liye.

```python
departments = Department.objects.prefetch_related("employees")
```

N+1 Query Problem avoid hoti hai.

---

## 3. Required Fields Hi Fetch Karna

### values()

```python
User.objects.values("id", "name")
```

### only()

```python
User.objects.only("id", "name")
```

Unnecessary columns fetch nahi hote.

---

## 4. Database Indexing

Frequently searched columns par index lagate hain.

```python
email = models.EmailField(db_index=True)
```

Search queries fast ho jati hain.

---

## 5. Pagination

Large datasets ko chunks me return karna.

```http
GET /users?page=1&limit=20
```

Ek hi request me lakhon records fetch nahi karte.

---

## 6. Aggregation Database Me Karna

Python me loop lagane ke bajay database aggregation use karte hain.

```python
from django.db.models import Count

User.objects.aggregate(total=Count("id"))
```

---

## 7. Avoid Unnecessary Queries

```python
queryset.exists()
```

Instead of:

```python
len(queryset)
```

---

## 8. Caching (Redis)

Frequently used data cache karte hain.

```text
Request
   ↓
Redis Cache
   ↓
Database (Only Cache Miss)
```

Database load significantly reduce hota hai.

---

## 9. Query Analysis

Query inspect karte hain:

```python
print(queryset.query)
```

Ya SQL execution plan dekhte hain:

```sql
EXPLAIN ANALYZE
```

---

## Interview Answer

Query optimization ke liye main `select_related()`, `prefetch_related()`, indexing, pagination, caching (Redis), aggregation functions aur required fields fetching techniques use karta hoon. Saath hi N+1 query problems avoid karta hoon aur `EXPLAIN ANALYZE` ya query inspection se slow queries identify karke optimize karta hoon.

# Middleware Kya Hota Hai?

Middleware Django me ek layer hoti hai jo **Request aur Response ke beech** execute hoti hai.

Ye request ko view tak pahunchne se pehle aur response ko client tak bhejne se pehle process kar sakti hai.

## Flow

```text
Client Request
      ↓
Middleware
      ↓
View
      ↓
Middleware
      ↓
Client Response
```

## Common Use Cases

- Authentication
- Authorization
- Logging
- Request/Response Modification
- Rate Limiting
- Exception Handling

## Example

```python
class RequestLogMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        print("Request Received")

        response = self.get_response(request)

        print("Response Sent")
        return response
```

## Interview Answer

Middleware Django ki ek processing layer hai jo request aur response ke beech execute hoti hai. Iska use authentication, logging, rate limiting, request/response modification aur exception handling jaise cross-cutting concerns ko handle karne ke liye kiya jata hai.

---

# Django Signals Kya Hote Hain?

Signals Django ka Observer Pattern implementation hain jo kisi event ke trigger hone par automatically code execute karne ki facility dete hain.

Simple words me:

```text
Event Hua
   ↓
Signal Trigger Hua
   ↓
Automatic Action Execute Hua
```

## Common Signals

### post_save

Object save hone ke baad.

```python
from django.db.models.signals import post_save
from django.dispatch import receiver

@receiver(post_save, sender=User)
def user_created(sender, instance, created, **kwargs):
    if created:
        print("User Created")
```

### pre_save

Object save hone se pehle.

### pre_delete

Object delete hone se pehle.

### post_delete

Object delete hone ke baad.

---

## Real Example

```text
User Register
      ↓
User Save
      ↓
post_save Signal
      ↓
Send Welcome Email
```

View ya model me extra code likhne ki zarurat nahi.

---

## Advantages

- Loose Coupling
- Reusable Logic
- Automatic Event Handling

---

## Disadvantages

- Debugging difficult ho sakti hai.
- Excessive use code ko complex bana sakta hai.

## Interview Answer

Django Signals event-driven mechanism hain jo specific events jaise `pre_save`, `post_save`, `pre_delete` aur `post_delete` par automatically code execute karne ki facility dete hain. Inka use loosely coupled actions jaise email sending, audit logging aur notifications ke liye kiya jata hai.

=======