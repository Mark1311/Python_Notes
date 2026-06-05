# Django Model Lifecycle Explain Karo

Django Model Lifecycle batata hai ki ek model object create hone se lekar database me save, update aur delete hone tak kaise process hota hai.

## Create Flow

```text
Object Create
      ↓
pre_save Signal
      ↓
Database Save
      ↓
post_save Signal
```

### Example

```python
user = User(name="Bittu")
user.save()
```

Events:

```text
1. pre_save
2. INSERT Query
3. post_save
```

---

## Update Flow

```python
user.name = "Kumar"
user.save()
```

Events:

```text
1. pre_save
2. UPDATE Query
3. post_save
```

---

## Delete Flow

```python
user.delete()
```

Events:

```text
1. pre_delete
2. DELETE Query
3. post_delete
```

---

## Complete Lifecycle

```text
Object Creation
      ↓
Model Instance Created
      ↓
pre_save
      ↓
Database Insert/Update
      ↓
post_save
      ↓
Business Operations
      ↓
pre_delete
      ↓
Database Delete
      ↓
post_delete
```

---

## Common Methods in Lifecycle

### save()

Object create/update karta hai.

```python
user.save()
```

### delete()

Object delete karta hai.

```python
user.delete()
```

### clean()

Custom validation ke liye.

```python
def clean(self):
    pass
```

### full_clean()

Model validations run karta hai.

```python
instance.full_clean()
```

---

## Real Example

```text
User Registration
       ↓
User.save()
       ↓
pre_save
       ↓
User Stored in DB
       ↓
post_save
       ↓
Welcome Email Send
```

---

## Interview Answer

Django Model Lifecycle me model object create, update aur delete hone ke dauran multiple stages hoti hain. Save operation ke time `pre_save` signal trigger hota hai, phir database query execute hoti hai aur uske baad `post_save` signal trigger hota hai. Delete operation ke liye `pre_delete` aur `post_delete` signals execute hote hain. Is lifecycle ka use validation, logging, notifications aur business logic execute karne ke liye kiya jata hai.

# Django Me Performance Improve Kaise Karte Ho?

Django application ki performance improve karne ke liye main database optimization, caching aur asynchronous processing techniques use karta hoon.

## 1. Query Optimization

- `select_related()` use karta hoon ForeignKey ke liye.
- `prefetch_related()` use karta hoon ManyToMany aur Reverse FK ke liye.
- N+1 Query Problem avoid karta hoon.

```python
User.objects.select_related("department")
```

---

## 2. Database Indexing

Frequently searched columns par indexing lagata hoon.

```python
email = models.EmailField(db_index=True)
```

---

## 3. Required Fields Hi Fetch Karna

```python
User.objects.only("id", "name")
```

Ya

```python
User.objects.values("id", "name")
```

---

## 4. Pagination

Large datasets ko ek saath load nahi karta.

```http
GET /users?page=1&limit=20
```

---

## 5. Redis Caching

Frequently accessed data Redis me cache karta hoon.

```text
Request
   ↓
Redis
   ↓
Database (Only Cache Miss)
```

Database load aur response time dono improve hote hain.

---

## 6. Celery for Background Tasks

Heavy tasks background me execute karta hoon.

### Examples

- Email Sending
- PDF Generation
- Notifications
- Report Exports

```python
send_email.delay(user_id)
```

---

## 7. API Response Optimization

- Unnecessary fields avoid karta hoon.
- Proper serialization use karta hoon.
- Large payloads reduce karta hoon.

---

## 8. Static & Media Optimization

- CDN use kar sakte hain.
- Static files ko efficiently serve karte hain.

---

## 9. Monitoring Slow Queries

```sql
EXPLAIN ANALYZE
```

Aur Django Debug Toolbar jaise tools use karke slow queries identify karta hoon.

---

## Interview Answer

Django performance improve karne ke liye main query optimization (`select_related`, `prefetch_related`), database indexing, pagination, Redis caching, Celery background tasks aur API response optimization use karta hoon. Saath hi slow queries monitor karke N+1 query issues aur unnecessary database hits ko eliminate karta hoon.


# ModelSerializer vs Serializer

Dono Django REST Framework me data serialization aur validation ke liye use hote hain, lekin unka use-case alag hai.

## Serializer

`Serializer` me hume fields aur create/update methods manually define karne padte hain.

### Example

```python
class UserSerializer(serializers.Serializer):
    id = serializers.IntegerField()
    name = serializers.CharField()
    email = serializers.EmailField()
```

### Pros

- Full control milta hai.
- Non-model data ke liye useful hai.
- Custom APIs ke liye suitable.

### Cons

- Zyada boilerplate code likhna padta hai.

---

## ModelSerializer

`ModelSerializer` model ke basis par automatically fields aur create/update methods generate kar deta hai.

### Example

```python
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = "__all__"
```

### Pros

- Kam code likhna padta hai.
- Automatic field generation.
- Automatic create/update methods.

### Cons

- Customization me kabhi-kabhi extra work karna pad sakta hai.

---

## Difference

| Serializer | ModelSerializer |
|------------|----------------|
| Fields manually define karni padti hain | Fields automatically model se generate hoti hain |
| create/update manually likhne padte hain | Auto generate ho jate hain |
| Non-model data ke liye useful | Model-based APIs ke liye best |
| More control | Less boilerplate |

---

## Interview Answer

`Serializer` me fields aur validation logic manually define karni padti hai aur ye non-model data ke liye useful hota hai. `ModelSerializer` model ke basis par automatically fields, validations aur create/update methods generate kar deta hai, isliye CRUD APIs ke liye commonly use kiya jata hai.


# Authentication aur Authorization me Difference

## Authentication

Authentication verify karta hai ki user **kaun hai**.

### Example

```text
Username + Password
JWT Token
OTP
```

Question:

```text
Who are you?
```

---

## Authorization

Authorization verify karta hai ki user **kya kar sakta hai**.

### Example

```text
Admin   → Create, Update, Delete
Employee → View Only
```

Question:

```text
What can you do?
```

---

## Interview Answer

Authentication user ki identity verify karta hai, jabki Authorization determine karta hai ki authenticated user ko kaunse resources ya actions perform karne ki permission hai.

---

# DRF Me Authentication Ke Types

## 1. Session Authentication

Django session-based authentication use karta hai.

```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.SessionAuthentication',
    ]
}
```

Mostly web applications ke liye use hota hai.

---

## 2. Basic Authentication

Username aur password har request ke saath bheje jate hain.

```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.BasicAuthentication',
    ]
}
```

Production me rarely use hota hai.

---

## 3. Token Authentication

User ko ek token assign kiya jata hai.

```http
Authorization: Token abc123
```

---

## 4. JWT Authentication

Most commonly used authentication for REST APIs.

```http
Authorization: Bearer <jwt_token>
```

Stateless authentication provide karta hai.

---

## Interview Answer

DRF me common authentication types Session Authentication, Basic Authentication, Token Authentication aur JWT Authentication hain. Modern REST APIs me JWT Authentication sabse zyada use hoti hai kyunki ye stateless aur scalable hoti hai.

---

# JWT Kya Hai?

JWT (JSON Web Token) ek stateless authentication mechanism hai jisme user login ke baad token receive karta hai aur us token ke through protected APIs access karta hai.

## Flow

```text
Login
   ↓
Server Verify Credentials
   ↓
Access Token + Refresh Token
   ↓
Client Store Token
   ↓
Authorization: Bearer <token>
   ↓
Protected APIs Access
```

## JWT Structure

```text
Header.Payload.Signature
```

Example:

```text
eyJhbGciOi...eyJ1c2VyX2lkIjox...abcxyz
```

## Benefits

- Stateless
- Scalable
- Fast
- Mobile & Web APIs ke liye suitable

## Interview Answer

JWT ek stateless authentication mechanism hai jisme user login ke baad Access Token aur Refresh Token receive karta hai. Client Access Token ko Authorization header me bhejta hai aur server token verify karke request authorize karta hai.

# Pagination Kya Hai?

Pagination ek technique hai jisme large dataset ko chhote-chhote pages me divide karke client ko return kiya jata hai. Isse response size kam hota hai, performance improve hoti hai aur database par load kam padta hai.

### Interview Answer

Pagination large data ko pages me divide karke return karne ki technique hai, jisse performance aur user experience better hota hai.

---

# Throttling Kya Hai?

Throttling ek mechanism hai jo kisi user ya client ki API requests ki rate ko limit karta hai taaki API abuse, excessive traffic aur server overload ko prevent kiya ja sake.

### Interview Answer

Throttling API requests ki frequency ko control karti hai aur ensure karti hai ki koi user defined limit se zyada requests na bhej sake.

---

# Nested Serializer Kya Hai?

Nested Serializer ka use related model data ko ek hi API response me represent karne ke liye kiya jata hai. Isse related objects ka data alag API call kiye bina ek hi response me mil jata hai.

### Interview Answer

Nested Serializer related models ka data ek hi serialized response me include karne ke liye use hota hai, jisse API response zyada structured aur convenient ban jata hai.

# PUT vs PATCH vs POST

## POST

POST ka use naya resource create karne ke liye hota hai.

### Interview Answer

POST request ka use server par naya resource create karne ke liye kiya jata hai.

---

## PUT

PUT ka use existing resource ko completely update ya replace karne ke liye hota hai.

### Interview Answer

PUT request existing resource ko full update ya replace karti hai. Generally saari fields bhejni padti hain.

---

## PATCH

PATCH ka use existing resource ko partially update karne ke liye hota hai.

### Interview Answer

PATCH request sirf required fields ko update karti hai aur poora resource replace nahi karti.

---

## Difference

| Method | Purpose |
|----------|----------|
| POST | Naya resource create karna |
| PUT | Existing resource ko completely update karna |
| PATCH | Existing resource ko partially update karna |

---

# HTTP Status Codes

## 200 OK

Request successfully complete ho gayi.

### Use Case

- Data fetch successfully ho gaya.
- Update successful hai.

### Interview Answer

200 status code successful request ko indicate karta hai.

---

## 201 Created

Naya resource successfully create ho gaya.

### Use Case

- User create hua.
- Order create hua.

### Interview Answer

201 status code tab return kiya jata hai jab naya resource successfully create ho jaye.

---

## 204 No Content

Request successful hai lekin response body me koi data return nahi karna.

### Use Case

- Delete operation successful.

### Interview Answer

204 status code successful operation ko indicate karta hai jahan response body me koi content nahi hota.

---

## 400 Bad Request

Client ne invalid request bheji hai.

### Use Case

- Validation error.
- Missing required fields.

### Interview Answer

400 status code invalid request ya validation failure ko indicate karta hai.

---

## 401 Unauthorized

User authenticated nahi hai.

### Use Case

- Invalid token.
- Missing token.

### Interview Answer

401 status code tab return hota hai jab authentication required ho aur user authenticated na ho.

---

## 403 Forbidden

User authenticated hai lekin permission nahi hai.

### Use Case

- Normal user admin action perform kar raha hai.

### Interview Answer

403 status code tab return hota hai jab user authenticated ho lekin requested resource access karne ki permission na ho.

---

## 404 Not Found

Requested resource exist nahi karta.

### Use Case

- User ID exist nahi karti.
- Invalid endpoint.

### Interview Answer

404 status code tab return hota hai jab requested resource ya endpoint nahi milta.

---

## 500 Internal Server Error

Server side par unexpected error aa gaya.

### Use Case

- Unhandled exception.
- Database failure.
- Application bug.

### Interview Answer

500 status code server-side error ko indicate karta hai jab request process karte waqt unexpected exception aa jaye.

