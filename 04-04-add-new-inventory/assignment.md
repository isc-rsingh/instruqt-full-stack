---
slug: 04-add-new-inventory
id: o9crvqeawauj
type: challenge
title: Add your own inventory
teaser: Finally, add more inventory on your own.
notes:
- type: text
  contents: Finally, add more inventory on your own.
tabs:
- title: VSCode
  type: service
  hostname: vscode
  path: /?folder=/opt/intersystems/src/setup
  port: 8080
- title: Terminal
  type: terminal
  hostname: vscode
difficulty: basic
timelimit: 900
---
Edit the `order_manifest.json` file in VSCode.

Change the values as you like and save the file.

Switch to the "Terminal" tab and run `manifest_importer.py` again.
```
python3 manifest_importer.py
```