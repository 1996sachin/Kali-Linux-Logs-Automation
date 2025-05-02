Edit `/usr/local/bin/send_logs_email.py` with your Gmail and app password.

```python
sender = "your_email@gmail.com"
receiver = "receiver_email@gmail.com"
password = "your_app_password"  # Use Gmail App Password
```


![image](https://github.com/user-attachments/assets/12bcf575-a869-4fbc-a280-723cd0c3454a)


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

![image](https://github.com/user-attachments/assets/64f58af7-3876-4c00-8576-f9e78c2ca46e)


---

## 📬 Example Email Output

```text
===== Firewall Logs =====
[ UFW/iptables logs from dmesg ]

![image](https://github.com/user-attachments/assets/b4563616-50ed-41ea-94b6-2160b46beaab)


===== Network Status =====
ip a
netstat -tulnp

![image](https://github.com/user-attachments/assets/54051e1f-5d3c-43b9-b29e-6a216209a1de)


===== Syslog =====
/var/log/syslog content
```
![image](https://github.com/user-attachments/assets/f33a056e-e133-4479-bb4d-0b6f0f18bbe2)


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
