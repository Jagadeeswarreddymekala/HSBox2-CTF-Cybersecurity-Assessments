# TrustNet Secure – HSBox2 CTF Walkthrough

A penetration-testing writeup from a cybersecurity internship CTF challenge
against a deliberately vulnerable lab target (HSBox2).

## Summary
Starting from a single Nmap scan, this walkthrough shows how an anonymous
FTP misconfiguration exposed a network capture file containing cleartext
login credentials — which were then reused to gain full administrative
access to the target's Drupal CMS.

## Chain of compromise
1. **Recon** – Nmap scan reveals SSH, HTTP (Drupal 7), and FTP open on the target.
2. **Initial access** – FTP allows anonymous login; a `.pcap` network capture is downloaded.
3. **Traffic analysis** – Wireshark reveals cleartext HTTP login credentials inside the capture.
4. **Credential reuse** – Recovered credentials are used to log into a demo banking app.
5. **Second capture** – A second set of cleartext credentials (CMS admin) is found in the same capture.
6. **Full compromise** – Admin credentials grant complete control of the Drupal CMS.

## Tools used
Nmap · FTP client · Wireshark · Web browser (Kali Linux)

## Key takeaways
- Anonymous FTP access should be disabled unless deliberately intended as public.
- All login traffic must run over HTTPS, never plain HTTP.
- Default/weak admin passwords (e.g. `admin@123`) are trivially guessable even without capture.

 This exercise was performed in an authorized, isolated lab environment for training purposes only.
