Edit `/usr/local/bin/send_logs_email.py` with your Gmail and app password.

```python
sender = "your_email@gmail.com"
receiver = "receiver_email@gmail.com"
password = "your_app_password"  # Use Gmail App Password
```

> 📌 **Use Gmail App Passwords** (required for 2FA accounts): [Google App Passwords](https://myaccount.google.com/apppasswords)

---

## 📆 Scheduling with `cron`

Edit crontab:

```bash
crontab -e
```

Add this line to run daily at 11:59 PM:

```cron
59 23 * * * /usr/local/bin/daily_log_report.sh && /usr/bin/python3 /usr/local/bin/send_logs_email.py
```

---

## 📬 Example Email Output

```text
===== Firewall Logs =====
[ UFW/iptables logs from dmesg ]

===== Network Status =====
ip a
netstat -tulnp

===== Syslog =====
/var/log/syslog content
```

---

## ✅ Final Checks

- Make sure `cron` is running:
  ```bash
  sudo systemctl status cron
  ```
- Run scripts manually to test:
  ```bash
  sudo /usr/local/bin/daily_log_report.sh
  python3 /usr/local/bin/send_logs_email.py
  ```

---

## 🧹 Log Cleanup

Logs older than 7 days are automatically deleted from:

```
/var/log/daily_reports/
```

---

## 📜 License

This project is licensed under the MIT License. Feel free to use and modify.

---

## 🤝 Contributing

Feel free to open issues or submit pull requests if you have improvements, feature requests, or bug reports!
