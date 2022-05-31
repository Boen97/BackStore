## free when moving cursor in a big file
[url](https://emacs.stackexchange.com/questions/506/debugging-a-frozen-emacs/507#507)
```
ps aux | grep -ie emacs | grep -v grep | awk '{print $2}' | xargs kill -SIGUSR2
```
