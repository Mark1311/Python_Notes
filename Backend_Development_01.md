# RESTful API Kya Hoti Hai?

RESTful API ek web service architecture hai jo HTTP methods (GET, POST, PUT, PATCH, DELETE) ka use karke client aur server ke beech data exchange karti hai.

### Example
```http
GET /api/users/1
POST /api/users
PUT /api/users/1
DELETE /api/users/1
```

---

# PUT vs PATCH

## PUT
Resource ko completely update karta hai.

```json
PUT /users/1

{
    "name": "Bittu",
    "email": "bittu@example.com"
}
```

Saari fields bhejni padti hain.

## PATCH
Resource ko partially update karta hai.

```json
PATCH /users/1

{
    "name": "Bittu"
}
```

Sirf required fields bhejni padti hain.

## Difference

| PUT | PATCH |
|------|------|
| Full Update | Partial Update |
| Saari fields bhejni padti hain | Sirf changed fields bhejni padti hain |
| Resource replace karta hai | Specific fields update karta hai |

### Interview Answer

PUT ka use resource ko completely update karne ke liye hota hai, jabki PATCH ka use sirf required fields ko update karne ke liye hota hai.

# API Versioning Kaise Karte Hain?

API Versioning ka use API me changes introduce karne ke liye kiya jata hai bina existing clients ko break kiye.

## Common Methods

### URL Versioning (Most Common)

```http
/api/v1/users/
/api/v2/users/
```

### Header Versioning

```http
Accept: application/vnd.company.v1+json
```

### Query Parameter Versioning

```http
/api/users?version=v1
```

## Django REST Framework Example

```python
REST_FRAMEWORK = {
    'DEFAULT_VERSIONING_CLASS': 'rest_framework.versioning.URLPathVersioning'
}
```

```python
path('api/<str:version>/users/', UserListAPIView.as_view())
```

## Interview Answer

API Versioning ka use backward compatibility maintain karne ke liye kiya jata hai. Sabse common approach URL Versioning hai, jaise `/api/v1/users/` aur `/api/v2/users/`, jisse naye changes add kar sakte hain bina existing clients ko affect kiye.

# Filtering, Searching, Sorting Kaise Implement Karoge? (API Design Perspective)

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

## Example

Agar limit hai:

```text
100 requests / minute
```

Aur user 101st request bhejta hai, to API response de sakti hai:

```http
429 Too Many Requests
```

## Kaise Implement Karoge?

### 1. User Based Rate Limiting

```text
100 requests/minute per user
```

Authenticated users ke liye.

### 2. IP Based Rate Limiting

```text
50 requests/minute per IP
```

Anonymous users ke liye.

### 3. Token Bucket / Leaky Bucket Algorithm

Production systems me commonly use hote hain request count track karne ke liye.

### 4. Redis + Middleware

Request count Redis me store kar sakte hain aur limit exceed hone par request block kar sakte hain.

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

## JWT Structure

JWT 3 parts se milkar banta hai:

```text
Header.Payload.Signature
```

Example:

```text
xxxxx.yyyyy.zzzzz
```

### Header

```json
{
    "alg": "HS256",
    "typ": "JWT"
}
```

### Payload

```json
{
    "user_id": 1,
    "username": "bittu",
    "exp": 1234567890
}
```

### Signature

Header + Payload ko secret key se sign kiya jata hai.

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

## Example

```text
Login with Google
Login with GitHub
Login with Facebook
```

Yahan application user ka password nahi dekhti, balki provider se access token receive karti hai.

## Interview Answer

OAuth2 ek authorization framework hai jo third-party applications ko user ke resources access karne ki permission deta hai bina user credentials share kiye. Isme access tokens ka use hota hai.

---

# SSO (Single Sign-On) Kya Hota Hai?

SSO ek authentication mechanism hai jisme user ek baar login karta hai aur multiple applications access kar sakta hai bina baar-baar login kiye.

## Example

```text
Google Login
    ↓
Gmail
Google Drive
Google Docs
Google Meet
```

Ek hi login se sab applications access ho jati hain.

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

## Interview Answer

Redis ek in-memory key-value data store hai jo extremely fast read/write operations provide karta hai. Iska use caching, session management, rate limiting, message queues aur real-time applications ke liye kiya jata hai taaki application performance improve ho aur database load kam ho.

# RabbitMQ Kya Hai?

RabbitMQ ek Message Broker hai jo producer aur consumer ke beech messages ko queue me store karke reliably deliver karta hai.

## Use Cases

- Background Jobs
- Email Sending
- Order Processing
- Task Queues
- Microservices Communication

### Flow

```text
Producer
    ↓
RabbitMQ Queue
    ↓
Consumer
```

## Interview Answer

RabbitMQ ek message broker hai jo producers aur consumers ke beech messages ko queue karke reliable delivery provide karta hai. Ye background task processing aur service communication ke liye use hota hai.

---

# Kafka Kya Hai?

Kafka ek Distributed Event Streaming Platform hai jo high-volume real-time data streams ko handle karne ke liye design ki gayi hai.

## Use Cases

- Log Processing
- Event Streaming
- Real-time Analytics
- Monitoring Systems
- Data Pipelines

### Flow

```text
Producer
    ↓
Kafka Topic
    ↓
Consumer
```

## Interview Answer

Kafka ek distributed event streaming platform hai jo millions of messages ko high throughput aur fault tolerance ke saath process kar sakta hai. Ye real-time data streaming aur analytics systems me use hota hai.

---

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

# Celery Kya Hai?

Celery Python ka distributed task queue framework hai jo background aur asynchronous tasks execute karne ke liye use hota hai.

Simple words me:

```text
Jo kaam user ko wait karaye,
wo background me Celery se kara do.
```

---

## Problem Without Celery

Suppose user order place karta hai.

```text
Place Order
    ↓
Send Email
    ↓
Generate Invoice PDF
    ↓
Send SMS
    ↓
Response
```

User ko response milne me 10-15 seconds lag sakte hain.

---

## Solution With Celery

```text
Place Order
    ↓
Task Queue
    ↓
Immediate Response
```

Background me:

```text
Celery Worker

├── Send Email
├── Generate PDF
└── Send SMS
```

User ko instantly response mil jata hai.

---

## Celery Architecture

```text
Application
     ↓
Celery
     ↓
Broker (Redis/RabbitMQ)
     ↓
Celery Worker
     ↓
Execute Task
```

### Components

#### Producer

Task create karta hai.

```python
send_email.delay(user_id)
```

#### Broker

Task ko queue me store karta hai.

Common brokers:

- Redis
- RabbitMQ

#### Worker

Queue se task uthakar execute karta hai.

---

## Common Use Cases

### Email Sending

```text
Welcome Email
Password Reset Email
Invoice Email
```

### Report Generation

```text
PDF Generation
Excel Export
```

### Notifications

```text
SMS
Push Notifications
WhatsApp Messages
```

### Heavy Data Processing

```text
Image Processing
Video Processing
Data Import
```

---

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