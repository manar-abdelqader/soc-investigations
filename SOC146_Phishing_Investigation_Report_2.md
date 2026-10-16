# SOC146 – Phishing Mail Detected (Excel 4.0 Macros)

**Investigation report · LetsDefend (simulated SOC environment)**

> This is a training exercise on the LetsDefend platform. I followed a guided
> *Phishing Playbook – Security Analyst*. It is not a real company incident.
> Email addresses, IPs and host names are masked on purpose.

---

## 1. Summary

| Item | Value |
|---|---|
| Alert | SOC146 – Phishing Mail Detected – Excel 4.0 Macros |
| Severity | High |
| Type | Exchange (email) |
| Difficulty | Easy |
| Playbook | Phishing Playbook – Security Analyst |
| MITRE ATT&CK | T1566 – Phishing (Initial Access) |
| My verdict | **True Positive** |
| Playbook success rate | 100% |
| Investigation time | 27 minutes |

A phishing email with a malicious Excel attachment reached an internal user.
The user opened the file, and the infected host contacted the attacker's
command-and-control (C2) address. I confirmed the alert as a True Positive,
removed the email, and contained the host.

---

## 2. Alert details (masked)

| Field | Value |
|---|---|
| Email subject | `RE: Meeting Notes` |
| Sender | external address (masked) |
| Recipient | internal user (masked) |
| SMTP IP | `24.213.xxx.xxx` (masked) |
| Device action | **Allowed** (the email was not blocked) |

The subject looks like a normal reply in an existing conversation. This is a
common trick to make the email look trusted.

---

## 3. Investigation steps

I followed the playbook step by step:

1. **Checked for attachments or URLs.** The email contained an attachment.
2. **Analyzed the attachment.** I classified it as malicious.
   *Tool I used:* the **Email Security** section in LetsDefend, to review the email and its attachment.
3. **Checked if the email was delivered to the user.** It was delivered.
4. **Checked if someone opened the malicious file.** The file was opened.
   *Tool I used:* the **Endpoint Security** section in LetsDefend, to check the user's host and see that it contacted the C2 address.
5. **Decided the result.** True Positive.

---

## 4. Mapping to Cyber Kill Chain and MITRE ATT&CK

| Stage | What happened in this case |
|---|---|
| Delivery | Phishing email with a malicious Excel attachment reached the user |
| Exploitation | The user opened the file and the malicious macro ran |
| Command and Control | The infected host connected to the C2 address |

**MITRE ATT&CK:** T1566 – Phishing, listed in the case. Tactic: Initial Access.

---

## 5. Actions taken

- Deleted the phishing email from the user's mailbox.
- Contained the affected host after confirming it contacted the C2 address.
- Recorded the SMTP IP as an artifact (indicator of compromise).

---

## 6. Recommendations

- Block the sender and the SMTP IP at the email gateway.
- Search other mailboxes for emails from the same sender.
- Restrict macros in files that come from email or the internet.
- Run phishing awareness training for users.
- Review why the email was *Allowed* by the email security device.

---

## 7. What I learned

I learned that it is important to check if the user opened the file, not only
if the email was delivered.

---

## 8. Skills practiced

Phishing analysis · alert triage · following an IR playbook · True/False
Positive classification · writing an analyst note · mapping to Cyber Kill
Chain and MITRE ATT&CK

---

*Author: Manar AbdelQader · Platform: LetsDefend (training environment)*
