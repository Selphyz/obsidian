___
Comprueba los ultimos commits y los mezcla en uno solo
```bash
git --no-pager log --oneline -3
git reset --soft HEAD~2
git commit -m "new commit message"
```
