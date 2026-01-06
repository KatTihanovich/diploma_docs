# API Reference

## Overview

Base URL: `https://game-progress-api.onrender.com`

Authentication: `Bearer Token`

## Endpoints

### Public (unauthenticated) endpoints:
- /api/users/register
- /api/users/login
- /actuator/**
- /v3/api-docs/**
- /swagger-ui/**
- /swagger-ui.html

### Private endpoints: all not mentioned endpoints are private

### Public endpoints that requires secret team password to use:
- /api/achievements/create
- /api/achievements/update/**
- /api/achievements/delete/**
- /api/levels/create
- /api/levels/update/**
- /api/levels/delete/**

**Note:**  
Instead of implementing a full admin role system, these endpoints are protected using a shared secret password. This approach simplifies development and testing, allowing the team to add or modify data in the database without creating separate admin accounts. It is intended for internal use by the development team only and should not be exposed publicly.

## Error Responses

| Error Code | Message | Description |
|------------|---------|-------------|
| 400 | Bad Request | Validation failed, missing parameters, type mismatches, illegal arguments, or malformed JSON requests. |
| 401 | Unauthorized | Invalid credentials, expired or malformed JWT tokens, or UnauthorizedException triggered. |
| 403 | Forbidden | AccessDeniedException triggered when user lacks permission for the requested resource. |
| 404 | Not Found | Requested endpoint does not exist (NoHandlerFoundException). |
| 500 | Internal Server Error | Any unexpected errors not caught by specific handlers; general server failure. |


## Rate Limiting
Using Render(Free tier) to host my game API.

| Tier | Requests/Minute | Requests/Day | Notes |
|------|-----------------|--------------|-------|
| Free | Depends on service usage | Limited by 750 free instance hours/month | Render spins down a Free web service after 15 minutes of inactivity and spins it back up on the next request. Spin-up can take up to a few minutes, causing a temporary delay in request processing. If all free instance hours are consumed, services are suspended until the next month. |

## Swagger/OpenAPI
Full API documentation available at: `https://game-progress-api.onrender.com/swagger-ui/index.html#/`
