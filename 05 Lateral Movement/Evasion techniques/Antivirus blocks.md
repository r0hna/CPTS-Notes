>Program 'winpeas.exe' failed to run: The program is blocked by group policy. For more information, contact you system administrator......
# Read app-locker policy
```
get-applockerpolicy -effective -xml
```
#### Read the 'exception' list (blocked list)

#### You can check the [writable dir from here](https://gist.github.com/mattifestation/5f9de750470c9e0e1f9c9c33f0ec3e56) or search on internet.
