
# SSH Brute Force Attack — Analysis

## What Is SSH Brute Force

SSH — Secure Shell — is a protocol that allows remote access 
into a machine through the command line. Attackers target SSH 
because if they can guess the password they gain full remote 
control of the machine.

Brute force doesn't exploit any specific bug or loophole — 
it works purely by volume. Instead of a human guessing 
manually, tools like Hydra automate this — trying hundreds 
of combinations per minute without stopping until something 
works.

---

## Attack Setup

Kali Linux was configured with a Bridged Adapter network 
setting — changing from NAT (Oracle's internal network) to 
a real IP address on the same network as VM2. This matters 
because machines on different networks can't reach each other 
directly — Kali needed to be on the same network as VM2 to 
launch the attack.

Hydra was run from Kali targeting VM2's SSH service using 
rockyou.txt — a wordlist containing 14 million real passwords 
leaked in a 2009 data breach. Hydra attempted approximately 
240 password combinations per minute against the root account.

**Command used:**
```bash
hydra -l root -P /usr/share/wordlists/rockyou.txt 10.126.241.208 ssh
```

---

## What Wazuh Detected

The Wazuh agent on VM2 detected every failed login attempt 
in real time and shipped the logs to VM1. The dashboard 
showed a massive spike in authentication failures almost 
immediately.

| Metric | Value |
|--------|-------|
| Total events | 4,773 |
| Authentication failures | 4,106 |
| Authentication successes | 32 |

---

## SOC Analyst Response

If this was a real corporate environment a SOC analyst would:

1. **Block the source IP** — add a firewall rule blocking all 
incoming traffic from the attacker's IP on port 22 immediately
2. **Limit SSH attempts** — configure fail2ban to automatically 
block IPs after a set number of failed attempts
3. **Enforce password compliance** — require strong passwords 
or switch to SSH key based authentication which eliminates 
password brute force entirely
4. **Investigate the successful authentications** — verify 
none of those 32 successes were the attacker gaining access
5. **Check for lateral movement** — determine if the attacker 
attempted connections to any other machines on the network
