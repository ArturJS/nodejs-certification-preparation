# 13. Security (Basics only) 5%

## Security checklist:

1. Embrace linter security rules:

    - https://github.com/nodesecurity/eslint-plugin-security

2. Limit concurrent requests using a middleware:

    - https://github.com/nfriedly/express-rate-limit

3. Extract secrets from config files or use packages to encrypt them:

    - https://github.com/mozilla/sops
    - https://github.com/hashicorp/vault

4. Prevent query injection vulnerabilities with ORM/ODM libraries.

The following libraries have built-in protection agains injection attacks:

    - https://github.com/sequelize/sequelize
    - https://github.com/tgriesser/knex
    - https://github.com/Automattic/mongoose

5. Avoid DOS attacks by explicitly setting when a process should crash.

6. Adjust the HTTP response headers for enhanced security:

    - https://github.com/helmetjs/helmet

7. Constantly and automatically inspect for vulnerable dependencies:

    - https://github.com/RetireJS/retire.js
    - https://docs.npmjs.com/cli/audit
    - https://snyk.io/

8. Avoid using the Node.js crypto library for handling passwords, use Bcrypt:

    - https://www.npmjs.com/package/bcryptjs

9. Escape HTML, JS and CSS output

10. Validate incoming JSON schemas:

    - https://www.npmjs.com/package/ajv
    - https://www.npmjs.com/package/@hapi/joi

11. Support blacklisting JWT tokens:

    - https://www.npmjs.com/package/express-jwt-blacklist
    - https://github.com/i0natan/nodebestpractices/blob/security-best-practices-section/sections/security/expirejwt.md

12. Limit the allowed login requests of each user

13. Run Node.js as non-root user:

    - https://github.com/i0natan/nodebestpractices/blob/security-best-practices-section/sections/security/non-root-user.md

14. Limit payload size using a reverse-proxy or a middleware:

    - https://github.com/i0natan/nodebestpractices/blob/security-best-practices-section/sections/security/requestpayloadsizelimit.md

15. Avoid JavaScript eval statements

16. Prevent evil RegEx from overloading your single thread execution:

    - https://github.com/substack/safe-regex
    - use https://github.com/chriso/validator.js instead of custom RegEx-es

17. Avoid module loading using a variable

18. Run unsafe code in a sandbox:

    - https://www.npmjs.com/package/isolated-vm

19. Take extra care when working with child processes:

    - https://github.com/i0natan/nodebestpractices/blob/master/sections/security/childprocesses.md

20. Hide error details from clients:

    - https://github.com/i0natan/nodebestpractices/blob/security-best-practices-section/sections/security/hideerrors.md

21. Configure 2FA for npm or Yarn

22. Modify session middleware settings:

    - https://github.com/i0natan/nodebestpractices/blob/security-best-practices-section/sections/security/sessions.md

23. A list of 40 generic security advice (not specifically Node.js-related):
    - Require MFA/2FA for root account
    - Rotate passwords and access keys frequently, including SSH keys
    - Apply strong password policies, both for ops and in-application user management, see OWASP password recommendation
    - Do not ship or deploy with any default credentials, particularly for admin users
    - se only standard authentication methods like OAuth, OpenID, etc. — avoid basic authentication
    - Auth rate limiting: Disallow more than X login attempts (including password recovery, etc.) in a period of Y minutes
    - On login failure, don’t let the user know whether the username or password verification failed, just return a common auth error
    - Consider using a centralized user management system to avoid managing multiple account per employee (e.g. GitHub, AWS, Jenkins, etc) and to benefit from a battle-tested user management system

For more information see also https://github.com/i0natan/nodebestpractices/tree/security-best-practices-section#-65-collection-of-common-generic-security-best-practices-15-items
