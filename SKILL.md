---
name: pocketagent-files
description: Create, read, list, update and delete small named text documents in the PocketAgent sandbox. Use when the user asks to manage a test text file. This does not access the iPhone Files app.
---
# PocketAgent Files v1

Use `run_js` for file operations. Script name: `index.html`.
Pass `data` as a JSON string containing:
- `action`: one of `create`, `read`, `list`, `update`, `delete`, `diagnose`
- `name`: filename, for all except list and diagnose
- `content`: text content for create or update

Examples:
- `{"action":"create","name":"test.txt","content":"Hello from PocketAgent"}`
- `{"action":"read","name":"test.txt"}`
- `{"action":"list"}`

Rules:
1. Invoke the actual `run_js` tool. Do not simulate its response.
2. After creating or updating, call `read` separately and compare returned text with requested text.
3. Report the tool's actual result, including any errors. Never claim a file was saved to iPhone Files; this skill only tests webview-local storage.
4. Ask for user confirmation before `delete` or overwriting an existing name. The script rejects create if the name already exists.
5. Do not store personal data, passwords or sensitive documents in this experimental skill.
6. The storage might not persist between webview executions. If `read` or `list` fails after a successful create, report this limitation.
