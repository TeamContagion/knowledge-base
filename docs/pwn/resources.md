# Resources/Tools

The following is a hastily put-together list of relevant tools and resources.

- [Libc database search](https://libc.blukat.me)
- [YT playlist on pwn basics](https://www.youtube.com/playlist?list=PLHUKi1UlEgOIc07Rfk2Jgb5fZbxDPec94)
- [ROP leaking libc address - HackTricks](https://book.hacktricks.xyz/reversing-and-exploiting/linux-exploiting-basic-esp/rop-leaking-libc-address)
- [tutorials on various pwn techniques](https://tc.gts3.org/cs6265/tut/tut00-intro.html)
- [pyjail resource](https://zhuanlan.zhihu.com/p/578986988) - literally in mandarin

- Funny payload:

```python
  (__builtins__:=__import__('code'))==(lambda:interact())()
__import__("os").system("cat flag*")
```

- [Zeratool](https://github.com/ChrisTheCoolHut/Zeratool) - automatic exploit generation
- [remenissions](https://github.com/guyinatuxedo/remenissions) - simple autopwner
- [Reverse TCP Shellcode](https://rastating.github.io/creating-a-reverse-tcp-shellcode/)
- [format1](https://github.com/VulnHub/ctf-writeups/blob/master/2016/angstrom-ctf/format-1.md) - example format string challenge writeup