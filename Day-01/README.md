📘 Day 01 – Creating a User with Non-Interactive Shell
🔹 Task

On App Server 2, the security team requested creating a user named kirsty with a non-interactive shell. This is to ensure the user account exists for process ownership or automation purposes but cannot log in interactively to the server.

🔹 Solution
# Connect to App Server 2 from the jumpserver
ssh steve@stapp02.stratos.xfusioncorp.com 
Enter password: Am3ric@

# Create user with a non-interactive shell
sudo useradd -s /sbin/nologin kirsty


🔹 Explanation

useradd → Command used to create a new user.

-s /sbin/nologin → Assigns a non-interactive shell. This prevents the user from accessing a terminal session.

kirsty → The username to be created.

Why?

Some users are required for service accounts, automation, or process ownership, but they should not log in like normal users.

Assigning /sbin/nologin ensures security: if someone tries to log in as kirsty, the system immediately denies access without starting a shell.

This is a best practice in system hardening, especially in DevOps environments where least-privilege access is critical.

🔹 Verification

To confirm user creation and shell assignment:

grep kirsty /etc/passwd


Expected output:

kirsty:x:1002:1002::/home/kirsty:/sbin/nologin


This shows:

Username: kirsty

Default home directory /home/kirsty

Shell is /sbin/nologin → confirming no interactive login.

🔹 Reflection

Today I learned how to create restricted system users in Linux. Such accounts are commonly used in DevOps for automation, scheduled jobs, or to run applications securely. By giving them a non-interactive shell, we reduce the attack surface and maintain system integrity.
