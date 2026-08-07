# picoCTF - DISKO 1

## challenge 
<img width="272" height="104" alt="Screenshot 2026-08-08 at 00 22 55" src="https://github.com/user-attachments/assets/30f49d9c-f1d1-49b6-bdb8-e2b651df0464" />

## initial thoughts
disko-1.dd.gz <- .gz indicates a gzip-compressed file, to confirm we run 
```bash
file disko-1.dd.gz
```
in return, we get;

```text
disko-1.dd.gz: gzip compressed data, was "disko-1.dd", last modified: Thu May 15 18:48:28 2025, from Unix, original size modulo 2^32 52428800
```

since it was compressed, I decompressed it using gunzip while keeping the original using -k:

```bash
gunzip -k disko-1.dd.gz
```

then, since we already know the format of the flag (picoCTF), we search for readable strings;

```bash
strings disko-1.dd | grep picoCTF
```

which revealed the flag.

## lessons learned
- .dd.gz is a compressed disk image
- gunzip -k preserves the original file and decompresses a copy
- strings extracts printable text from binaries
- grep is useful when you already know the flag format
