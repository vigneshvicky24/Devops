# SYSTEM ADMINISTRATOR

## sudo – Super User Do
- The special key is `sudo`, which temporarily grants you permission to perform an action that requires elevated privileges.

### Feature Comparison Table

| Feature            | root       | sudo                       |
|-------------------|------------|----------------------------|
| Is it a user?      | Yes        | No (it's a command)        |
| Unlimited power?   | Yes        | Yes, but temporarily       |
| Security           | Risky      | Safer                      |
| Logging of actions | No         | Yes                        |
| Can be restricted? | No         | Yes (sudoers file)         |
| Typical use        | System admin | Regular users doing admin tasks |
