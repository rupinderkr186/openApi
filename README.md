# 📘 Truck Parking Club API - OpenAPI Spec

This project uses the **OpenAPI 3.0.1 specification** to define a RESTful API for managing truck parking bookings. This document serves as the technical contract for frontend/backend teams and is importable into tools like Azure API Management, Swagger, and Postman.

---

## 📂 File: `openapi.yaml`

This file contains a full definition of the API in YAML format, adhering to the OpenAPI 3.0.1 specification.

---

## 🔍 What is OpenAPI?

**OpenAPI** is a standardized, machine-readable way to describe your REST APIs. It enables:
- 📄 Auto-generated API documentation
- ⚙️ Code generation for client/server stubs
- 🧪 Mock server support for frontend development
- 🔐 Easy integration into tools like Azure API Management (APIM)

---

## ✍️ Structure Overview

```yaml
openapi: 3.0.1
info:
  title: Truck Parking Club API
  version: 1.0.0
servers:
  - url: https://your-api.azurewebsites.net
paths:
  /bookings:
    get:
      summary: Get all bookings
      responses:
        '200':
          description: OK
    post:
      summary: Create a booking
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Booking'
      responses:
        '201':
          description: Created
components:
  schemas:
    Booking:
      type: object
      properties:
        id:
          type: string
        truckId:
          type: string
        parkingSpot:
          type: string
        date:
          type: string
          format: date
```

Here's a working example scaffold for a RESTful API designed with **OpenAPI**, deployed on **Azure App Service**, and managed via **Azure API Management (APIM)**.

## 🚀 Example Project: Truck Parking API
### Stack:
 * **API Design:** OpenAPI 3.0 (YAML)

 * **Backend**: Node.js + Express

 * **API Management**: Azure API Management (APIM)

 * **Hosting**: Azure App Service

 * **Auth (Optional)**: JWT / Azure AD

## ✅ Folder Structure
```
pgsql
truck-parking-api/
├── api-spec/
│   └── openapi.yaml
├── server/
│   ├── package.json
│   ├── app.js
│   └── routes/
│       └── bookings.js
├── Dockerfile (optional)
└── README.md
```
---
## 1. 📘 openapi.yaml (API Contract Example)

```
yaml
openapi: 3.0.1
info:
  title: Truck Parking Club API
  version: 1.0.0
servers:
  - url: https://your-api.azurewebsites.net
paths:
  /bookings:
    get:
      summary: Get all bookings
      responses:
        '200':
          description: OK
    post:
      summary: Create a booking
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Booking'
      responses:
        '201':
          description: Created
components:
  schemas:
    Booking:
      type: object
      properties:
        id:
          type: string
        truckId:
          type: string
        parkingSpot:
          type: string
        date:
          type: string
          format: date
```

## 2. 💻 server/app.js (Express Server)
```
js
const express = require("express");
const app = express();
const bookings = require("./routes/bookings");

app.use(express.json());
app.use("/bookings", bookings);

app.listen(process.env.PORT || 3000, () => {
  console.log("API running...");
});
```

## 3. 📁 server/routes/bookings.js
```
js
const express = require("express");
const router = express.Router();

const bookings = [];

router.get("/", (req, res) => {
  res.json(bookings);
});

router.post("/", (req, res) => {
  const booking = req.body;
  bookings.push(booking);
  res.status(201).json(booking);
});

module.exports = router;
```

## 4. 🚀 Deploy to Azure
### Option A: With Azure CLI
```
bash
az login
az webapp up --name truck-parking-api --resource-group myResourceGroup --runtime "NODE|18-lts"
```

### Option B: With Docker
```
dockerfile
# Dockerfile
FROM node:18
WORKDIR /app
COPY server/ .
RUN npm install
CMD ["node", "app.js"]
```

## 5. 🔐 Import OpenAPI into Azure API Management
1. Go to **Azure Portal > API Management > APIs**  
2. Click + **Add API > OpenAPI**  
3. Upload your `openapi.yaml` or import from URL  
4. Azure will create:
    * Developer documentation  
    * API versioning  
    * Analytics  
    * Security policies  

## 6. 🛡 Secure with JWT (Optional)
In Azure APIM:  
  * Add a **validate-jwt** policy under inbound policy  
  * Use **Azure AD** or **Auth0** as the identity provider  

