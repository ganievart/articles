# How to store passwords that depend on environment (TBD)

## Ways
* Storing secrets in your code.

  This highly increases the risk that this secret could leak.

* Storing secrets in the environment.

  There are still some problems: a simple misconfiguration (such as running a production server in debug mode) or a security bug could result in the leak of all the environment variables.

* Storing secrets in the database.

  You will still need to have your database credentials outside somewhere.

* Using a secrets syncing service.

  We’re still facing the same issue as the previous method: you’ll need a very secret API key in order to get all your API keys.

* Storing secrets in your code …but encrypted.

  To decrypt those secrets, the server still needs to manage a key.

## Solution
[IAM authenticated API](https://serverless-stack.com/chapters/connect-to-api-gateway-with-iam-auth.html)

In a nutshell, we can create a micro-service (accessible via, you guessed it, an IAM authenticated API Gateway) that will create credentials on-the-fly for the desired services. For exemple: if the micro-service is asked for PostgreSQL credentials, it can issue a CREATE ROLE command with a randomly generated password. Additionally, the role could have a time-to-live using the VALID UNTIL property.

## References
* https://medium.com/poka-techblog/the-best-way-to-store-secrets-in-your-app-is-not-to-store-secrets-in-your-app-308a6807d3ed
