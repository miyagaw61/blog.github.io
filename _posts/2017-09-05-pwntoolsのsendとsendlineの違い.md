**sendは改行が入らず、sendlineは改行が入る。**  

* どういう時に使い分けるのか。

基本的には改行を入れるsendlineで問題無いが、  
**数値がそのままメモリに入る場合**は、改行を入れてはいけないので、sendを使う。  

* 例題

TWCTF2017 swap

入力した2つの数値をアドレスとして、その中身を交換する処理を利用するpwn問。  
入力値を文字列として受け取りatoi関数などを通る場合は普通にsendlineで良いのだが、  
atoi関数をputs関数に書き換えた後は、入力値がatoiを通らずにそのままputsされるため、改行を入れてしまうとリークできなくなってしまう。  
```python
sendline("2")
sendline("A")
```
```
[DEBUG] Received 0x7 bytes:
    00000000  41 0a f4 81  fc 7e 0a 
    00000007
[*] LEAK: libc rw = 0xa41
```
```python
send("2")
send("A")
```
```
[DEBUG] Received 0x7 bytes:
    00000000  41 f6 f4 81  fc 7e 0a 
    00000007
[*] LEAK: libc rw = 0x7efc81f4f641
```

