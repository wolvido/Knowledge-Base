how to set one local to push identically into two repos?

```bash
git remote set-url --add --push origin https://github.com/YourSecondRepo.git
```

then check by using:
```bash
git remote -v
```
if there is two push origins, then it works.

also works on github desktop. very neat.