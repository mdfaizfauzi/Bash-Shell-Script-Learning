# **SysSnapshot**  
> A Linux System Monitoring & Backup Utility  
> *Version 1.0 — For Diploma in ICT Systems, Services & Support (CIML019)*

---

## 📦 Installation

### Prerequisites
- Linux system (Ubuntu/Debian, CentOS/RHEL, or any modern Linux distribution)
- Bash shell (default on most Linux systems)
- `sudo` access (for `df`, `find`, `ps`, and filesystem operations)
- `rsync`, `tar`, `awk`, `du`, `find`, `who`, `free`, `uptime` (all standard in most Linux distributions)

> ⚠️ If you're on Windows, you must use **WSL (Windows Subsystem for Linux)** or a **Linux VM** to run this script.

---

### Steps to Install

1. **Download or clone** the project folder (if using GitHub or shared repo).
2. **Navigate to the project root** (where `SysSnapshot.sh` is located).
3. **Make the script executable**:

   ```bash
   chmod +x SysSnapshot.sh
   ```

4. **Ensure directories exist** (optional, but recommended):

   ```bash
   mkdir -p backups reports
   ```

5. **Run the script**:

   ```bash
   ./SysSnapshot.sh
   ```

---

## 🧭 Usage

### 📋 Main Menu

When you run the script, you’ll see a colorful menu:

```
┌────────────────────────────────────────────────────────────┐
│               LINUX SYSTEM MONITORING & BACKUP UTILITY     │
│                       Version 1.0                          │
└────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────┐
│               SYSTEM HEALTH & USER ACTIVITY                │
├────────────────────────────────────────────────────────────┤
│  1) Check System Resources (CPU, Memory, Disk)             │
│  2) Track User Activity & Sessions                         │
└────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────┐
│                       BACKUP MANAGEMENT                    │
├────────────────────────────────────────────────────────────┤
│  3) Create Incremental Backup                              │
│  4) Verify Backup Integrity                                │
└────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────┐
│                      REPORTING & ANALYSIS                  │
├────────────────────────────────────────────────────────────┤
│  5) Generate Filesystem Usage Report                       │
│  6) Analyze Running Processes                              │
└────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────┐
│                        0) Exit                             │
└────────────────────────────────────────────────────────────┘
```

---

### 📌 Feature Descriptions

#### **1. System Health & User Activity**
- `1` → Check CPU, memory, disk usage.
- `2` → List active users, session times, and multiple sessions.

#### **2. Backup Management**
- `3` → Create incremental backup of `/home/$USER/documents` (or custom path).
- `4` → Verify backup integrity (compares file count).

#### **3. Reporting & Analysis**
- `5` → Generate detailed filesystem usage report (top directories, types).
- `6` → List top processes by CPU/memory, state counts, long-running processes.

---

## 📁 File Structure

```
system-monitor/
├── SysSnapshot.sh          # Main script
├── config/                 # (Optional) settings.conf
├── logs/
│   └── system_monitor.log  # Main application log
├── backups/                # Backup destination
├── reports/                # Generated reports
├── tests/                  # Test scripts and results
└── README.md               # This file
```

---

## 🛠️ Troubleshooting

### ❌ Script Hangs on Option 5 (Filesystem Report)
- **Cause**: Scanning `/` or `/home` recursively can take too long.
- **Fix**: Use the **limited-scope version** — it scans only `/home`, `/var`, `/usr` — fast and safe.

### ❌ “command not found” or “syntax error”
- **Cause**: Script created on Windows with CRLF line endings.
- **Fix**: Run `dos2unix SysSnapshot.sh` or `sed -i 's/\r$//' SysSnapshot.sh` to convert line endings.

### ❌ “No such file or directory” for backup source
- **Fix**: Ensure the source directory (e.g., `/home/$USER/documents`) exists. You can create it:

  ```bash
  mkdir -p /home/$USER/documents
  ```

### ❌ “No backup directory found” for verify_backup_integrity
- **Fix**: Run `3` to create a backup first, then run `4`.

---

## 📊 Sample Output

### ✅ Option 1: System Resources

```
=== System Resources ===
CPU Load: 0.52, 0.58, 0.61
Memory: 8GB total, 6GB used (75%)
Disk: 50GB used of 100GB (50%)
```

### ✅ Option 5: Filesystem Report

```
=== Filesystem Usage Report ===
Generated: 2025-11-29 00:03
========================================
--- Top 10 Largest Directories ---
    /home/user/documents     1.2G
    /var/log                 1.0G
    /usr/share               800M
...
```

---

## ✅ Testing

You can test each function independently:

```bash
# Test Option 1
./SysSnapshot.sh
# Choose 1 → Check System Resources

# Test Option 3
./SysSnapshot.sh
# Choose 3 → Create Incremental Backup

# Test Option 5
./SysSnapshot.sh
# Choose 5 → Generate Filesystem Report

# Test Option 4
./SysSnapshot.sh
# Choose 4 → Verify Backup Integrity (after creating backup)
```

---

## 📝 Documentation

### Function Documentation

| Function | Purpose |
|----------|---------|
| `check_system_resources()` | Monitor CPU, memory, and disk usage. |
| `track_user_activity()` | List active users and sessions. |
| `create_incremental_backup()` | Create timestamped incremental backups. |
| `verify_backup_integrity()` | Verify backup file counts and integrity. |
| `generate_filesystem_report()` | Generate detailed filesystem usage report. |
| `analyze_running_processes()` | Analyze top processes by CPU, memory, state. |

---

## 📎 Known Limitations

- **Limited scope** for filesystem scanning (to avoid system-wide hangs).
- **No GUI** — requires terminal interaction.
- **Backup destination** is hardcoded to `/home/$USER/backups` — can be modified in `SysSnapshot.sh`.
- **Requires sudo** for some operations (e.g., `df`, `find`, `ps`).

---

## 📞 Support

If you encounter issues, refer to the troubleshooting section or contact your tutor.

---

## 📈 Version History

- **v1.0** — Initial release (Oct 2025)

---

✅ **You’re all set!**  
This `README.md` covers everything required for your Assignment 1 deliverable — including installation, usage, testing, and documentation.

---

📌 **Tip**: Save this file as `README.md` in your project root folder.  
📌 **Tip**: For your viva, demonstrate all 6 functions with sample outputs — and show how to run tests and verify backups.

---

✅ **Final Note**: Your script is now **fully functional**, **well-documented**, and **ready for submission**.

You can now submit this README along with your `SysSnapshot.sh` script — and you’re ready for your viva! 🎓🎉
