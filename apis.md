# Employee APIs

## Show User Info

This endpoint retrieves the profile information of a specific user.

**URL:** `/certpro/api/:user/profile`

**Headers:**

- `auth_key` : `[String]` auth_key is generated when the user logged in.

**Path Parameters:**

- `user` (String): Name of the user whose information you want to retrieve.

**Method:** `GET`

**Authentication:** Required

**Permissions:** Current user (Employee)

### **Success Response:**

- **Code:** `200 OK`
- **Content Example:**
  ```json
  {
    "emp_id": "xxx",
    "name": "xxxxx",
    "email": "xxxxx@gmail.com",
    "photo": "emp_id_profile.jpg",
    "dob": "dd/mm/yyyy"
  }
  ```

### **Error Response:**

- Error (Code: `400 Bad Request`, `401 Unauthorized`, etc.)

## Update User Info

This endpoint updates the profile information of a specific user.

**URL:** `/certpro/api/:user/profile/`

**Headers:**

- `auth_key` : `[String]` auth_key is generated when the user logged in.

**Path Parameters:**

- `user` (String): Name of the user whose information you want to update.

**Method:** `PUT`

**Authentication:** Required

**Permissions:** Current user (Employee)

**Data**

**Request payload:**
```json
    {
      "name": "xxxxx",
      "photo": "emp_id_profile.jpg",
      "dob": "dd/mm/yyyy"
    }
  ```

### **Success Response:**

- **Code:** `201 OK`
- **Content Example:**
  ```json
  {
    "emp_id": "xxx",
    "name": "xxxxx",
    "email": "xxxxx@gmail.com",
    "photo": "emp_id_profile.jpg",
    "dob": "dd/mm/yyyy"
  }
  ```

### **Error Responses:**

- **Code:** `202`
- **Example response:**
  ```json
  {
    "error_message": "Requested operation has not been processed."
  }
  ```
- **Code:** `403 FORBIDDEN`
- **Response:**
  ```json
  {
    "error_message": "User is not authorized."
  }
  ```

## Delete User Account

This endpoint allows for the removal of a user account from the system, including all associated profile information.

**URL:** `/certpro/api/:user/profile/`

**Method:** `DELETE`

**Authentication:** Required

**Authentication Header:** `auth_key (String)` - Generated during user login

**Permissions:** Employee (Current User)

**Path Parameters:**

- `user` (String): The username of the profile to be deleted.

### **Success Response:**

- **Code:** `204 NO CONTENT`
- This status code indicates that the request has been successfully processed, and there is no content to return.

### **Error Responses:**

- **Code:** `403 FORBIDDEN`
- **Example Response:**
  ```json
  {
    "error_message": "Access forbidden. You are not authorized to perform this action."
  }
  ```
- **Code:** `404 NOT FOUND`
- **Example Response:**
  ```json
  {
    "error_message": "User not found."
  }
  ```

## Add Certificate

This endpoint enables the user to add certificate to the user's profile.

**URL:** `/certpro/api/:user/certs/`

**Method:** `POST`

**Authentication:** Required

**Authentication Header:** `auth_key (String)` - Generated during user login

**Permissions:** Employee (Current User)

**Path Parameters:**

- `user` (String): The username of the user to whom the certificate will be added.

**Request Body:**
```json
    {
      "name": "Certification Name",
      "issuing_organization": "Organization Name",
      "date_received": "yyyy-mm-dd",
      "expiration_date": "yyyy-mm-dd",
      "credential_id": "Credential ID",
      "credential_url": "Credential URL"
    }
  ```

### **Success Response:**

- **Code:** `201 CREATED`
- This status code indicates that the request has been successfully fulfilled, and a new resource has been returned as a result.
- **Content Example:**
  ```json
  {
    "certification_id": "unique_id",
    "name": "Certification Name",
    "issuing_organization": "Organization Name",
    "date_received": "yyyy-mm-dd",
    "expiration_date": "yyyy-mm-dd",
    "credential_id": "Credential ID",
    "credential_url": "Credential URL"
  }
  ```

### **Error Responses:**

- **Code:** `400 BAD REQUEST`
- **Example Response:**
  ```json
  {
    "error_message": "Invalid input data. Please check your request body."
  }
  ```
- **Code:** `403 FORBIDDEN`
- **Example Response:**
  ```json
  {
    "error_message": "Access forbidden. You are not authorized to perform this action."
  }
  ```
- **Code:** `404 NOT FOUND`
- **Example Response:**
  ```json
  {
    "error_message": "User not found."
  }
  ```

## Update Certificate

This endpoint enables the user to update certificate to the user's profile.

**URL:** `/certpro/api/:user/certs?credential_id=xxx`

**Method:** `PUT`

**Authentication:** Required

**Authentication Header:** `auth_key (String)` - Generated during user login

**Permissions:** Employee (Current User)

**Path Parameters:**

- `user` (String): The username of the user to whom the certificate will be updated.

**Query Parameters:**

- `credential_id` (String): Credential Id of the certificate to be updated

**Example URL:**  
`/certpro/api/johndoe/certs?credential_id=xxx`

**Request Body:**
```json
    {
      "name": "Certification Name",
      "issuing_organization": "Organization Name",
      "date_received": "yyyy-mm-dd",
      "expiration_date": "yyyy-mm-dd",
      "credential_id": "Credential ID",
      "credential_url": "Credential URL"
    }
  ```

### **Success Response:**

- **Code:** `201 CREATED`
- This status code indicates that the request has been successfully fulfilled, and a new resource has been created as a result.
- **Content Example:**
  ```json
  {
    "certification_id": "unique_id",
    "name": "Certification Name",
    "issuing_organization": "Organization Name",
    "date_received": "yyyy-mm-dd",
    "expiration_date": "yyyy-mm-dd",
    "credential_id": "Credential ID",
    "credential_url": "Credential URL"
  }
  ```

### **Error Responses:**

- **Code:** `400 BAD REQUEST`
- **Example Response:**
  ```json
  {
    "error_message": "Invalid input data. Please check your request body."
  }
  ```
- **Code:** `403 FORBIDDEN`
- **Example Response:**
  ```json
  {
    "error_message": "Access forbidden. You are not authorized to perform this action."
  }
  ```
- **Code:** `404 NOT FOUND`
- **Example Response:**
  ```json
  {
    "error_message": "User not found."
  }
  ```

## Search Certificate

This endpoint enables the user to search for certificate.

**URL:** `/certpro/api/:user/certs?`

**Method:** `GET`

**Authentication:** Required

**Authentication Header:** `auth_key (String)` - Generated during user login

**Permissions:** Employee (Current User)

**Path Parameters:**

- `user` (String): The username of the user to whom the certificate will be searched

**Query Parameters:**

- `cert_name` (String): The name of the certificate to retrieve.
- `filter_option` (String, optional): Additional filter options for the search.

**Example URL:**  
`/certpro/api/johndoe/certs?cert_name=AWS Cloud &filter_option=expired`

### **Success Response:**

- **Code:** `200 OK`
- This status code indicates that the request was successful, and the server is returning the requested resource in the response body.
- **Content Example:**
  ```json
  [
    {
      "certification_id": "unique_id_1",
      "name": "AWS Cloud Foundation",
      "issuing_organization": "AWS",
      "date_received": "yyyy-mm-dd",
      "expiration_date": "yyyy-mm-dd",
      "credential_id": "Credential ID 1",
      "credential_url": "Credential URL 1"
    },
    {
      "certification_id": "unique_id_2",
      "name": "AWS Cloud Architecture",
      "issuing_organization": "AWS",
      "date_received": "yyyy-mm-dd",
      "expiration_date": "yyyy-mm-dd",
      "credential_id": "Credential ID 2",
      "credential_url": "Credential URL 2"
    }
  ]
  ```

### **Error Responses:**

- **Code:** `403 FORBIDDEN`
- **Example Response:**
  ```json
  {
    "error_message": "Access forbidden. You are not authorized to perform this action."
  }
  ```
- **Code:** `404 NOT FOUND`
- **Example Response:**
  ```json
  {
    "error_message": "Cert not found."
  }
  ```

## Show Certificates

This endpoint enables retrieval of certificate from the user's profile.

**URL:** `/certpro/api/:user/certs/`

**Method:** `GET`

**Authentication:** Required

**Authentication Header:** `auth_key (String)` - Generated during user login

**Permissions:** Employee (Current User)

**Path Parameters:**

- `user` (String): The username of the user to whom the certificate will be retrieved.

### **Success Response:**

- **Code:** `200 OK`
- This status code indicates that the request was successful, and the server is returning the requested resource in the response body.
- **Content Example:**
  ```json
  [
    {
      "certification_id": "unique_id_1",
      "name": "Certification Name 1",
      "issuing_organization": "Organization Name 1",
      "date_received": "yyyy-mm-dd",
      "expiration_date": "yyyy-mm-dd",
      "credential_id": "Credential ID 1",
      "credential_url": "Credential URL 1"
    },
    {
      "certification_id": "unique_id_2",
      "name": "Certification Name 2",
      "issuing_organization": "Organization Name 2",
      "date_received": "yyyy-mm-dd",
      "expiration_date": "yyyy-mm-dd",
      "credential_id": "Credential ID 2",
      "credential_url": "Credential URL 2"
    }
  ]
  ```

### **Error Responses:**

- **Code:** `403 FORBIDDEN`
- **Example Response:**
  ```json
  {
    "error_message": "Access forbidden. You are not authorized to perform this action."
  }
  ```
- **Code:** `404 NOT FOUND`
- **Example Response:**
  `json
    {
      "error_message": "Cert not found."
    }
    `

## Suggest Certificate Orgs / Certificate Names

This endpoint returns all the certificate organization names.

**URL:** `/certpro/api/:user_id/certs?search_criteria=search_value`

**Method:** `GET`

**Authentication:** Required

**Authentication Header:** `auth_key (String)` - Generated during user login

**Permissions:** Employee (current user)

**Query Parameters:**

- `search_value` (String, optional): To get all the certs/organizations.
- `search_criteria` (String): `org` / `cert`

**Example:**

- `/certpro/api/:user_id/certs?org=xxx`
- `/certpro/api/:user_id/certs?cert=xxx`

**Path Parameters:**

- `user_id` (String): The username of the user to whom the certificate organizations will be searched.

### **Success Response:**

- **Code:** `200 OK`
- This status code indicates that the request was successful, and the server is returning the requested resource in the response body.
- **Content Example:**
  ```json
  {
    "Certificate Organizations": ["xxxx", "xxxx", ...]
  }
  ```
  Or
  ```json
  {
    "data": "query_param_value"
  }
  ```

### **Error Responses:**

- **Code:** `403 FORBIDDEN`
- **Example Response:**
  ```json
  {
    "error_message": "Access forbidden. You are not authorized to perform this action."
  }
  ```

# Employer APIs

## List Employees

This endpoint returns all the employees in an organization who are registered.

**URL:** `/certpro/api/:employer_id/employees?filter_option=xxxx`

**Method:** `GET`

**Authentication:** Required

**Authentication Header:** `auth_key (String)` - Generated during user login

**Permissions:** Employer (Admin)

**Query Parameters:**

- `filter_option` (String, optional): Additional filter options for the list.

**Example:** `/certpro/api/:employer_id/employees?sortby=`

**Path Parameters:**

- `employer_id` (String): The employer ID who is performing the search.

### **Success Response:**

- **Code:** `200 OK`
- **Content Example:**
  ```json
  [
    {
      "emp_id": "xxx",
      "name": "xxxxx",
      "email": "xxxxx@gmail.com",
      "photo": "emp_id_profile.jpg",
      "dob": "dd/mm/yyyy"
    },
    {
      "emp_id": "xxx",
      "name": "xxxxx",
      "email": "xxxxx@gmail.com",
      "photo": "emp_id_profile.jpg",
      "dob": "dd/mm/yyyy"
    }
    // ... more employees
  ]
  ```

### **Error Response:**

- Error (Code: `400 Bad Request`, `401 Unauthorized`, etc.)

## Search Certificate

This endpoint enables the user to search who did a specific certificate.

**URL:** `/certpro/api/:employee_id/certs?cert_name=xxx`

**Method:** `GET`

**Authentication:** Required

**Authentication Header:** `auth_key (String)` - Generated during user login

**Permissions:** Employer (Admin)

**Query Parameters:**

- `cert_name` (String): Name of the certificate the employer wanted to search.

### **Success Response:**

- **Code:** `200 OK`
- **Content Example:**
  ```json
  [
    {
      "certification_id": "unique_id_1",
      "name": "AWS Cloud Foundation",
      "issuing_organization": "AWS",
      "date_received": "yyyy-mm-dd",
      "expiration_date": "yyyy-mm-dd",
      "credential_id": "Credential ID 1",
      "credential_url": "Credential URL 1"
    },
    {
      "certification_id": "unique_id_2",
      "name": "AWS Cloud Architecture",
      "issuing_organization": "AWS",
      "date_received": "yyyy-mm-dd",
      "expiration_date": "yyyy-mm-dd",
      "credential_id": "Credential ID 2",
      "credential_url": "Credential URL 2"
    }
    // ... more certs
  ]
  ```

### **Error Response:**

- Error (Code: `400 Bad Request`, `401 Unauthorized`, etc.)

## Search Employee

This endpoint returns the employees in an organization.

**URL:** `/certpro/api/:employer_id/search_employee?filter_option=xxxx`

**Method:** `GET`

**Query Parameters:**

- `filter_option`: emp_name or emp_id.
  - `emp_name` : Name of the employee, employer want to search.
  - `emp_id` : Unique id of every employee.

**Authentication:** Required

**Authentication Header:** `auth_key (String)` - Generated during user login

**Permissions:** Employer (Admin)

### **Success Response:**

- **Code:** `200 OK`
- **Content Example:**
  ```json
  [
    {
      "emp_id": "xxx",
      "name": "xxxxx",
      "email": "xxxxx@gmail.com",
      "photo": "emp_id_profile.jpg",
      "dob": "dd/mm/yyyy"
    },
    {
      "emp_id": "xxx",
      "name": "xxxxx",
      "email": "xxxxx@gmail.com",
      "photo": "emp_id_profile.jpg",
      "dob": "dd/mm/yyyy"
    }
    // ... more employees
  ]
  ```

### **Error Response:**

- Error (Code: `400 Bad Request`, `401 Unauthorized`, etc.)

## Add New Certificate Organization

This endpoint allows administrators to add a new certificate organization to the CertPro system.

**URL:** `/certpro/api/:employer_id/cert_orgs`

**Method:** `POST`

**Request Body:**

- `name` (String, required): The name of the new certificate organization.
- `description` (String, optional): A brief description of the certificate organization.
- `website` (String, optional): The website URL of the certificate organization.

**Authentication:** Required

**Authentication Header:** `auth_key (String)` - Generated during administrator login

**Permissions:** Administrator

**Example Request:**
```json
    {
      "org_name": "AWS",
      "cert_name": "AWS"
    }
  ```

### **Success Response:**

- **Status Code:** `201 CREATED`
- **Content Example:**
  ```json
  {
    "message": "Certification organization added successfully.",
    "cert_org_id": "123456789"
  }
  ```

### **Error Responses:**

- **Status Code:** `400 BAD REQUEST`
- **Example Response:**
  ```json
  {
    "error_message": "Invalid request. Please provide a valid name for the certificate organization."
  }
  ```
- **Status Code:** `403 FORBIDDEN`
- **Example Response:**
  ```json
  {
    "error_message": "Access forbidden. You are not authorized to perform this action."
  }
  ```

# Authentication API

## Login

This endpoint allows users to authenticate and obtain an authentication token for accessing other protected resources(certs).

**URL:** `/certpro/api/login`

**Method:** `POST`

**Request Body:**

- `username` (String, required): The username of the user.
- `password` (String, required): The password associated with the user's account.

**Example Request:**
```json
    {
      "username": "Rajesh16",
      "password": "*****"
    }
  ```

**Authentication:** Not required

**Permissions:** None

### **Success Response:**

- **Status Code:** `200 OK`
- **Content Example:**
  ```json
  {
    "message": "Login successful.",
    "auth_key": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjoiMTIzNDU2Nzg5MCIsImlhdCI6MTYyMzE1NjEzOSwiZXhwIjoxNjIzMTU5NzM5fQ.QqM2Yb_4Y3RL3FlvRg74BpA16UueQIPlXziq2tGElZw"
  }
  ```

### **Error Responses:**

- **Status Code:** `401 UNAUTHORIZED`
- **Example Response:**
  ```json
  {
    "error_message": "Invalid username or password."
  }
  ```
- **Status Code:** `400 BAD REQUEST`
- **Example Response:**
  ```json
  {
    "error_message": "Invalid request. Please provide a username and password."
  }
  ```

## Signup

This endpoint allows users to create a new account.

**URL:** `/certpro/api/signup`

**Method:** `POST`

**Request Body:**

- `username` (String, required): The desired username for the new account.
- `email` (String, required): The email address of the user.
- `password` (String, required): The password for the new account.
- `emp_name` (String, required): The name of the employee.
- `emp_id` (String, required): The employee id.

**Example Request:**
```json
    {
      "username": "example_user",
      "email": "user@example.com",
      "password": "example_password",
      "emp_name": "xxx",
      "emp_id": "xxx"
    }
  ```

**Authentication:** Not required

**Permissions:** None

### **Success Response:**

- **Status Code:** `201 CREATED`
- **Content Example:**
  ```json
  {
    "message": "Account created successfully. Please check your email for verification instructions."
  }
  ```

### **Error Responses:**

- **Status Code:** `400 BAD REQUEST`
- **Example Response:**

  ```json
  {
    "error_message": "Invalid request. Please provide all required fields."
  }
  ```

- **Status Code:** `409 CONFLICT`
- **Example Response:**
  ```json
  {
    "error_message": "Username or email already exists."
  }
  ```

## Change Password

This endpoint allows users to change their password.

**URL:** `/certpro/api/change_password`

**Method:** `PUT`

**Request Body:**

- `username` (String, required): The username of the user.
- `current_password` (String, required): The user's current password.
- `new_password` (String, required): The new password for the user's account.

**Example Request:**
```json
    {
      "username": "example_user",
      "current_password": "old_password",
      "new_password": "new_password"
    }
  ```

**Authentication:** Required

**Authentication Header:** `auth_key (String)` - Generated during user login

**Permissions:** None

### **Success Response:**

- **Status Code:** `200 OK`
- **Content Example:**
  ```json
  {
    "message": "Password changed successfully."
  }
  ```

### **Error Responses:**

- **Status Code:** `400 BAD REQUEST`
- **Example Response:**
  ```json
  {
    "error_message": "Invalid request. Please provide all required fields."
  }
  ```
- **Status Code:** `401 UNAUTHORIZED`
- **Example Response:**
  ```json
  {
    "error_message": "Unauthorized. Please provide a valid authentication token."
  }
  ```
- **Status Code:** `403 FORBIDDEN`
- **Example Response:**
  ```json
  {
    "error_message": "Access forbidden. You are not authorized to perform this action."
  }
  ```
- **Status Code:** `409 CONFLICT`
- **Example Response:**
  ```json
  {
    "error_message": "Current password does not match."
  }
  ```

## Forgot Password

This endpoint allows users to initiate the process of resetting their password if they have forgotten it. A verification code will be sent to the user's email address for verification before proceeding with the password reset.

**URL:** `/certpro/api/forgot_password`

**Method:** `POST`

**Request Body:**

- `email` (String, required): The email address associated with the user's account.

**Example Request:**
```json
    {
      "email": "mail_id@example.com"
    }
  ```
**Authentication:** Not required

**Permissions:** None

### **Success Response:**

- **Status Code:** `200 OK`
- **Content Example:**
  ```json
  {
    "message": "Verification code sent to your email address. Please check your inbox."
  }
  ```

### **Error Responses:**

- **Status Code:** `400 BAD REQUEST`
- **Example Response:**
  ```json
  {
    "error_message": "Invalid request. Please provide a valid email address."
  }
  ```
- **Status Code:** `404 NOT FOUND`
- **Example Response:**
  ```json
  {
    "error_message": "Email address not found."
  }
  ```

## Verify Code

This endpoint allows users to verify the verification code sent to their email address during the password reset process.

**URL:** `/certpro/api/verify_code`

**Method:** `POST`

**Request Body:**

- `email` (String, required): The email address associated with the user's account.
- `verification_code` (String, required): The verification code sent to the user's email address.

**Example Request:**
```json
    {
      "email": "user@example.com",
      "verification_code": "123456"
    }
  ```

**Authentication:** Not required

**Permissions:** None

### **Success Response:**

- **Status Code:** `200 OK`
- **Content Example:**
  ```json
  {
    "message": "Verification code is valid. You can now proceed to change your password."
  }
  ```

### **Error Responses:**

- **Status Code:** `400 BAD REQUEST`
- **Example Response:**
  ```json
  {
    "error_message": "Invalid request. Please provide a valid email address and verification code."
  }
  ```
- **Status Code:** `404 NOT FOUND`
- **Example Response:**
  ```json
  {
    "error_message": "Email address not found."
  }
  ```
- **Status Code:** `401 UNAUTHORIZED`
- **Example Response:**
  ```json
  {
    "error_message": "Invalid verification code."
  }
  ```


## 
$$
---End---
$$ 
