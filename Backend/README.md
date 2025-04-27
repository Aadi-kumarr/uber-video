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

# /users/login Endpoint Documentation

## Endpoint

`POST /users/login`

## Description

Authenticates a user and returns a JWT token if the credentials are valid.

## Request Body

Send a JSON object with the following structure:

```
{
  "email": "string (valid email, required)",
  "password": "string (min 6 chars, required)"
}
```

### Example

```
{
  "email": "john.doe@example.com",
  "password": "secret123"
}
```

## Validation Rules
- `email`: Required, must be a valid email
- `password`: Required, at least 6 characters

## Responses

- **200 OK**: Login successful. Returns `{ token, user }`.
- **400 Bad Request**: Validation failed. Returns `{ errors: [...] }`.
- **401 Unauthorized**: Invalid email or password. Returns `{ message: 'Invalid Email or Password' }`.

## Status Codes
- `200`: User authenticated successfully
- `400`: Invalid input data
- `401`: Authentication failed

## Notes
- Passwords are compared securely using hashing.
- Ensure the email exists in the system before attempting to log in.
