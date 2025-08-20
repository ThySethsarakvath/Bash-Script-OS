# 🗑️ Safe Deletion System

This project replaces the default `rm` command with a safe deletion system that moves files and directories to `/tmp/trash/` instead of permanently deleting them. It includes two scripts:

---

## 🔧 How the Scripts Work

### `rm` Script
- Accepts one or more files or directories.
- Supports recursive deletion with `-r`.
- Moves each item to `/tmp/trash/` and appends a timestamp to avoid name conflicts.
- Logs each deletion to `/tmp/trash/trash.log` with:
  - Original path
  - Trash path
  - Timestamp

### `restore` Script
- Accepts a filename or partial match.
- Finds the most recent matching entry in the log.
- Restores the file or directory to its original location.
- Creates missing destination directories if needed.
- Renames restored files if a naming conflict occurs.

---

## 🧪 How Edge Cases Were Handled

### Nonexistent Files
- The `rm` script checks if each target exists.
- If not, it prints an error and skips that item.

### Directory Deletion Without `-r`
- If a directory is passed without the `-r` flag, the script rejects it and shows an error message.

### Unsupported Flags
- Any flags other than `-r` are rejected with a usage message.

### Name Conflicts During Restore
- If the original path already exists, the restored file is renamed with a `_restored` suffix to avoid overwriting.

### Multiple Deletions of the Same Filename
- The `restore` script uses the most recent match from the log to ensure correct recovery.

---

## 📁 Trash Directory Structure

---
``` 
/tmp/trash/
      ├── trash.log
      ├── filename_timestamp
      └── foldername_timestamp/

```
---
## ✅ Example Usage

```bash
./rm.sh -r my_folder
./restore.sh my_folder

