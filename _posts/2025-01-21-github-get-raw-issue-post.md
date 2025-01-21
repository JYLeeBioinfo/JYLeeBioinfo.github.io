---
title: "GitHub Misc Usage 1 : Get raw markdown text for issue comments"
output:
  html_document: default
date: "2025-01-21"
---

# 1. Quote replies

Usually, to get the raw markdown text of a comment to reply to it, just select "..." and then "Quote reply" works.
![image](https://github.com/user-attachments/assets/29aa5401-33eb-4cd2-8977-5694d5b3672e)

# 2. Long and problematic quotes

"Quote reply" may return markdown with broken format and it may be tedious to fix it.

In that case, you can follow these instructions to get the actual raw markdown text.


## 2.1 Get the link to comment

![image](https://github.com/user-attachments/assets/7c532d34-ba2c-4148-8951-a4c9f86b9720)

 - Select "..." and then "Copy link" to get the address to the comment you want to get markdown raw text from.

```
https://github.com/<USERNAME>/<REPONAME>/issues/<issue_number>#issuecomment-<comment_number>
```

 - Convert it to api url like this and go to this url on the web browser
```
https://api.github.com/repos/<USERNAME>/<REPONAME>/issues/comments/<comment_number>
```

 - You get a json-formatted text. Copy the values of "body", i.e. the quoted string following '"body" :'

```
"body": "abcde.....fghhr"
```

 - Make a python script using the copied body.

```{python}
text = "abcde.....fghhr"
print(text.replace("\t","  "))
```

 - Run the python script and you will get the raw markdown text.
