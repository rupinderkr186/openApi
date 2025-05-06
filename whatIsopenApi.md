## 🧾 What is `openapi.yaml`?

`openapi.yaml` is a **YAML-formatted file** that defines your API using the **OpenAPI Specification (OAS)** — a standard format for describing RESTful APIs.

---

### 📌 Purpose

- Acts as a contract between frontend and backend
- Enables auto-generated documentation, client SDKs, and mock servers
- Can be imported directly into platforms like **Azure API Management**, **Swagger UI**, **Postman**, or used to generate boilerplate server code

---

## 🔍 Line-by-Line Explanation of Sample `openapi.yaml`

Here’s a simplified version of an `openapi.yaml`:

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
## 🧩 Explanation of Each Section
`openapi: 3.0.1`  
Declares the version of the OpenAPI Specification used.  
📌 Most widely supported version.

## `info`
Metadata about the API.
```yaml
info:
  title: Truck Parking Club API     # Display name for your API
  version: 1.0.0                    # Current version of the API
```

## `servers`
Defines the base URLs where the API is hosted.
```yaml
servers:
  - url: https://your-api.azurewebsites.net  # Where requests are sent (Azure-hosted API)
```
## `paths`
Lists all available endpoints and HTTP methods (GET, POST, etc.).
```yaml
paths:
  /bookings:     # Route path of the API
    get:         # HTTP GET method
      summary: Get all bookings
      responses:
        '200':                  # HTTP status code
          description: OK      # Description of the response
```
`summary`: Short explanation of what this endpoint does  
`responses`: Defines possible HTTP responses  
`'200'`: Standard success (OK)  
`'201'`: Created (for POST)  

## `post` and `requestBody`
Defines how POST requests work.
```yaml
    post:
      summary: Create a booking
      requestBody:                 # Defines what the client must send
        content:
          application/json:       # Content-Type
            schema:
              $ref: '#/components/schemas/Booking'  # Reuse a schema
```
## `components`
Reusable components for schema definitions, security, parameters, etc.
```yaml
components:
  schemas:
    Booking:            # Defines a Booking object schema
      type: object      # It's a JSON object
      properties:
        id:
          type: string
        truckId:
          type: string
        parkingSpot:
          type: string
        date:
          type: string
          format: date   # ISO format date string
```
You define models here once and reuse them across multiple endpoints using $ref.
