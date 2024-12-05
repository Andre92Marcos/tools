# impacket-secretdump

## Overview

SecretDumps is a tool often used in the context of Windows privilege escalation and post-exploitation activities. It allows an attacker (or penetration tester) to extract sensitive information from a compromised system, such as password hashes, Kerberos tickets, and other credentials stored in Windows' LSASS (Local Security Authority Subsystem Service).

SecretDumps allows attackers to dump credentials from Windows systems by extracting data from LSASS, the service responsible for managing user authentication. Specifically, SecretDumps can be used to:

Extract NTLM password hashes of user accounts.
Dump Kerberos tickets from memory, which could allow for Pass-the-Ticket (PTT) attacks.
Obtain plaintext passwords if available, especially if they were cached in memory.
Extract secrets stored in the SAM (Security Accounts Manager) database or LSASS.

## How SecretDumps Works

SecretDumps works by dumping credential information from Windows system memory, particularly from LSASS, SAM, or NTDS.dit (in domain controllers). Here's a general flow of how it works:

Target Process: SecretDumps focuses on the LSASS process, which is responsible for authentication in Windows systems. This process stores various credentials, such as password hashes and tickets.

Extracting Credentials: SecretDumps connects to the LSASS process and extracts the credentials stored within it. This can include:

NTLM password hashes for local users and domain accounts.
Kerberos tickets, which can be used for lateral movement or Pass-the-Ticket attacks.
Cached credentials (if applicable).
No Need for Direct LSASS Interaction: Unlike tools such as Mimikatz, which often require interacting directly with LSASS via memory injection or debugging, SecretDumps is typically designed to avoid direct memory access and can work with remote systems by utilizing SMB or WMI (Windows Management Instrumentation).

Remotely Dumping Credentials: SecretDumps can dump credentials from remote systems without requiring interactive access to the target. It works over network protocols like SMB or WMI, meaning you can execute SecretDumps from a remote system to pull credentials from another machine, often used to escalate privileges on a network.

Output Format: Once credentials are extracted, SecretDumps often outputs them in a format that includes NTLM hashes, Kerberos tickets, or other relevant credential data, which attackers can then use to authenticate to other systems in the network.

## How SecretDumps Differs from Other Tools (e.g., Mimikatz)


Mimikatz is a tool that works by directly interacting with LSASS's memory in order to extract credentials. It is highly powerful and flexible but requires debug privileges (SeDebugPrivilege) to access and dump LSASS memory.

SecretDumps, on the other hand, often works without needing to directly inject into LSASS memory. Instead, it interacts with LSASS through more traditional network-based methods, using protocols like SMB or WMI, allowing it to dump credentials remotely or from a running system without having to interact directly with the LSASS process.

## Usage

    impacket-secretdump -sam <target_ip> -user <username> -password <password>
    impacket-secretdump -ntds <target_ip> -user <username> -password <password>

## Permissions Required

| Privilege               | Local Machine (SAM)  | Domain Controller (NTDS.dit) |
|-------------------------|----------------------|-----------------------------|
| **Local Administrator**  | Required             | Optional (but needed for local access) |
| **Domain Administrator** | Not required         | Required (for domain access) |
| **SeDebugPrivilege**     | Required             | Required                    |
| **SeBackupPrivilege**    | Optional             | Optional                    |
| **SeTakeOwnershipPrivilege** | Optional        | Optional                    |
| **Remote Execution Permissions** | Optional (if running remotely) | Required (if running remotely) |