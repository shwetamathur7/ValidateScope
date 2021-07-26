### Verify the scope of the user

_API is called only if user has right scopes_

```         IAuthenticationResult result = authHelper.getAuthResultBySilentFlow(httpRequest, authHelper.configuration.clientDefaultScope);
            String scope = JWTParser.parse(result.accessToken()).getJWTClaimsSet().getStringClaim("scp");
            if(scope.equals("access_as_user"))
                clientApiCallResult = callClientService(result.accessToken());
            else
            httpResponse.sendError(HttpServletResponse.SC_UNAUTHORIZED,
                    "You are not authorized to access the application");
  ```


##To verify the User's scope 

1. Parse the JWT token to get the scope of the user.
2. Validate the scope with the assigned scopes.
3. If user has right scope , then only call the application otherwise prompt User is unauthorized.
 

**To validate the changes, Remove API permission(scope = access_as_user) from Azure Portal and hit the application.**


_Another way to verify scope in spring boot is using @Authorization annotation_
Define the scope and roles in application file and verify the scope if authorization scheme is OAuth2 using @RolesAllowed and scope 
to authorize the resource in the application.
