# jwt-service-handler

This library can be used in any js service for jwt token validation (for m2m and frontend tokens), caching and refreshing jwt_enabled_services list in your service.

## Table of Contents

- [Getting Started](#getting-started)
- [Additional Configuration](#additional-configuration)

## Getting Started

To install jwt-service-handler package add the following section to your `package.json`:

```json
"jwt-service-handler": "theorchard/jwt-service-handler.git#v0.1.0",
```

Import the library in your file:

```javascript
import TokenHandler from 'jwt-tokenhandler';
```

To validate your jwt token add the below validation code:

```javascript
const tokenHandlerInst = new TokenHandler.TokenHandler();
const bearerToken = tokenHandlerInst.isBearerToken(jwtToken);
if (bearerToken)
    await tokenHandlerInst.verifyAndDecodeToken(bearerToken);
```

To cache jwt_enabled_services in your service add the below code:

```javascript
const tokenHandlerInst = new TokenHandler.CacheHandler(yourCacheObject, yourServiceName);
tokenHandlerInst.cacheJwtEnabledServices();
```

To retrieve jwt_enabled_services from cache in your service add the below code:

```javascript
const jwtenabledServiceslist = tokenHandlerInst.retriveCache('jwt_enabled_services');
```

To start a refresh job for updating jwt_enabled_services list in your service cache add the below code:

```javascript
const cacheRefreshInst = new TokenHandler.CacheRefreshHandler(yourCacheObject, yourServiceName);
cacheRefreshInst.cacheRefreshSchedulerJob();
```

## Additional Configuration

### Access to jwt_enabled_services secret

Your service should have read and update access to jwt_enabled_services secret.
This requires that your service is terraformed with latest terraform-fargate version (>=1.5.1).
