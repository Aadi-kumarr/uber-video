# /users/register Endpoint Documentation

## Endpoint

`POST /users/register`

## Description

Registers a new user in the system. Requires user details in the request body. On success, returns a JWT token and the created user object.

## Request Body

Send a JSON object with the following structure:

```
{
  "fullname": {
    "firstname": "string (min 3 chars, required)",
    "lastname": "string (optional, min 3 chars if provided)"
  },
  "email": "string (valid email, required)",
  "password": "string (min 6 chars, required)"
}
```

### Example

```
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.doe@example.com",
  "password": "secret123"
}
```

## Validation Rules
- `fullname.firstname`: Required, at least 3 characters
- `fullname.lastname`: Optional, at least 3 characters if provided
- `email`: Required, must be a valid email
- `password`: Required, at least 6 characters

## Responses

- **201 Created**: Registration successful. Returns `{ token, user }`.
- **400 Bad Request**: Validation failed. Returns `{ errors: [...] }`.

## Status Codes
- `201`: User registered successfully
- `400`: Invalid input data

## Notes
- Passwords are securely hashed before storage.
- Email must be unique.
