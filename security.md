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

8. Avoid using the Node.js crypto library for handling passwords, use Bcrypt

9. Escape HTML, JS and CSS output

10. Validate incoming JSON schemas

11. Support blacklisting JWT tokens

12. Limit the allowed login requests of each user

13. Run Node.js as non-root user

14. Limit payload size using a reverse-proxy or a middleware

15. Avoid JavaScript eval statements

16. Prevent evil RegEx from overloading your single thread execution

17. Avoid module loading using a variable

18. Run unsafe code in a sandbox

19. Take extra care when working with child processes

20. Hide error details from clients

21. Configure 2FA for npm or Yarn

22. Modify session middleware settings

23. A list of 40 generic security advice (not specifically Node.js-related)
