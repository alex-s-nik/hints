1. Different text indent for multiple languages, different formatter: black for python, prettier for html

settings.json
  
  ```json
  {
    "black-formatter.args": [
        "--skip-string-normalization",
        "--line-length=120"
    ],
    "[python]": {
        "editor.tabSize": 4,
        "editor.defaultFormatter": "ms-python.black-formatter",
        "editor.formatOnSave": true
    },
    "[html]": {
        "editor.tabSize": 2,
        "editor.defaultFormatter": "esbenp.prettier-vscode",
        "editor.formatOnSave": true
    },
    "editor.codeActionsOnSave": {

    },
    "[css]": {
        "editor.defaultFormatter": "vscode.html-language-features",
        "editor.tabSize": 2
    },
    "[django-html]": {    
        "editor.tabSize": 2
    }
}
```
