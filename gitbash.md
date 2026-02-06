1. If output GitBash for Windows command "git status" contains cyrillic symbols in coding like _\320\260\320\277\321\202\320 then it needs the setting
```bash
 git config --global core.quotePath false
```
