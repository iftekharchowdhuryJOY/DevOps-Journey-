> Question: The company needs a way to authorize API calls within Amazon API Gateway while also having built-in user management. Your job as a Solutions Architect is to recommend the best authentication/authorization mechanism that AWS offers.
**Answer: Amazon Cognito User Pools**

## Why is "Amazon Cognito User Pools" the Best Answer?
Amazon Cognito User Pools is an AWS service that provides user authentication and management. It is designed for applications where you need to authenticate users before granting access to APIs.

## Built-In User Management: Amazon Cognito User Pools provides pre-built user directories to handle:

* User registration, login, and password management.
* Multi-factor authentication (MFA), email/phone verification, and account recovery.
* No need to build custom user databases or authentication workflows.
* Native Integration with API Gateway: API Gateway can directly use Cognito User Pools as an authorizer. When a user logs in via Cognito, they receive a JWT token, which API Gateway validates to grant/deny access to the API.
* Social & Enterprise Identity Federation: Supports logins via Google, Facebook, SAML, or OIDC providers (e.g., Azure AD) alongside native user pools.
* Scalability & Security: Fully managed service with automatic scaling and compliance (e.g., GDPR, HIPAA). Tokens are signed with RSA keys, ensuring secure API authorization.

## How Cognito Works with API Gateway
* Users sign up and log in using Amazon Cognito.
* Cognito issues JWT tokens (ID & Access tokens).
* The client includes the JWT token in API requests to API Gateway.
* API Gateway validates the token using Cognito.
* If the token is valid, the request is authorized and passed to the backend.
## Cost Calculation
1. Free Tier: 50,000 Monthly Active Users (MAUs) free every month. MAU Definition: A user who signs in (authenticates) at least once in a calendar month. Includes standard features like user sign-up, sign-in, password management, and basic security.

Cognito User Pools charges per Monthly Active User (MAU)

3. Example Cost Calculation
Scenario: 70,000 MAUs in a month (US-East-1 region).
* Cost: First 50,000 MAUs → $0 (free tier). Next 20,000 MAUs → 20,000 × 0.0055 = 0.0055=∗∗110**. Total: $110/month.

### Another Scenario:
1. 300,000 MAUs: First 50k → $0.

* 50k–100k → 50k × 0.0055 =0.0055=275.
* 100k–300k → 200k ×  0.0046= 0.0046=920.

Total: 275+275+920 = $1,195/month.

## Real-World Scenario
A fitness app uses Cognito User Pools to let users create accounts and log in. The app’s API (hosted on API Gateway) uses Cognito as an authorizer to ensure only authenticated users can access workout data. Users can reset passwords via Cognito’s email/SMS workflows, and the app later adds Google/Facebook login options without changing the API auth logic.

