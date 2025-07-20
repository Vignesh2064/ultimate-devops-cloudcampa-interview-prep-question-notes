

### 🔹 **🧠 Basic to Intermediate Shell Scripting Questions**

---

#### 1. **What is a shell script?**

A shell script is a text file containing a sequence of commands for a UNIX-based shell to execute.

---

#### 2. **How do you make a script executable?**

```bash
chmod +x script.sh
```

---

#### 3. **What is the difference between `sh` and `bash`?**

* `sh` is Bourne Shell (older).
* `bash` is Bourne Again Shell (advanced, supports arrays, functions, etc.).

---

#### 4. **How do you pass arguments to a script?**

```bash
#!/bin/bash
echo "First argument: $1"
echo "All arguments: $@"
```

---

#### 5. **What does `$?` return?**

Exit status of the last executed command (0 = success, non-zero = failure).

---

#### 6. **How do you loop over a list in bash?**

```bash
for i in apple banana mango; do
   echo $i
done
```

---

#### 7. **How to check if a file exists?**

```bash
if [ -f "file.txt" ]; then
  echo "Exists"
fi
```

---

#### 8. **What is the use of `set -e`?**

Script exits immediately if any command fails (non-zero exit).

---

#### 9. **How to debug a shell script?**

Use:

```bash
bash -x script.sh
```

Or include:

```bash
#!/bin/bash -x
```

---

#### 10. **How do you read user input inside a script?**

```bash
read -p "Enter name: " name
echo "Hello $name"
```

---

### 🔹 **🔥 Advanced & Real-Time Scenario-Based Questions**

---

#### 11. **How do you handle errors in bash scripts gracefully?**

```bash
command || { echo "Command failed"; exit 1; }
```

---

#### 12. **Write a script to monitor disk usage and send alert**

```bash
#!/bin/bash
THRESHOLD=80
USAGE=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')

if [ "$USAGE" -gt "$THRESHOLD" ]; then
   echo "Disk usage is above threshold: $USAGE%" | mail -s "Disk Alert" admin@example.com
fi
```

---

#### 13. **How do you find and delete files older than 7 days?**

```bash
find /var/log -type f -mtime +7 -exec rm -f {} \;
```

---

#### 14. **What is a Here Document?**

Used for multi-line strings:

```bash
cat <<EOF
This is a
multi-line string
EOF
```

---

#### 15. **Difference between `$@` and `$*`?**

* `$@` treats each quoted argument as separate.
* `$*` treats them as a single string.

---

#### 16. **Write a script to check if a process is running and restart if not**

```bash
#!/bin/bash
if ! pgrep nginx > /dev/null; then
   echo "Nginx not running, restarting..."
   systemctl start nginx
fi
```

---

#### 17. **What are traps in shell scripting?**

Used to catch signals (like SIGINT):

```bash
trap 'echo "Script interrupted"; exit' INT
```

---

#### 18. **How to use functions in bash?**

```bash
greet() {
  echo "Hello, $1"
}
greet Vignesh
```

---

#### 19. **How to export and use environment variables in scripts?**

```bash
export NAME="Vignesh"
echo "My name is $NAME"
```

---

#### 20. **How do you create a cron job to run your script every hour?**

Edit crontab with `crontab -e` and add:

```
0 * * * * /path/to/script.sh
```

---

### 🔹 **💼 Real-World Use Case Examples for DevOps**

---

#### ✅ CI/CD Automation:

Automate builds:

```bash
#!/bin/bash
git pull origin main
docker build -t myapp .
docker run -d -p 80:80 myapp
```

---

#### ✅ Backup Script:

```bash
#!/bin/bash
tar -czf backup_$(date +%F).tar.gz /etc
aws s3 cp backup_$(date +%F).tar.gz s3://mybucket/
```

---

#### ✅ Log Rotation:

```bash
#!/bin/bash
mv /var/log/app.log /var/log/app_$(date +%F).log
touch /var/log/app.log
```

---


## 🟢 **Intermediate Shell Script Interview Questions**

1. **What is the difference between `$*` and `$@`?**

   * `$*` treats all arguments as a single word.
   * `$@` treats each quoted argument as a separate word.

2. **How to pass arguments to a shell script?**

   * Example: `./script.sh arg1 arg2`
   * Access via `$1`, `$2`, etc.

3. **How to check if a file exists and is readable?**

   ```bash
   if [ -r filename ]; then
     echo "File is readable"
   fi
   ```

4. **How do you handle errors in Shell?**

   * Using `set -e` to exit on any command failure.
   * Check with `$?`, or use traps.

5. **How to create a function in Shell?**

   ```bash
   my_function() {
     echo "Hello from function"
   }
   ```

---

## 🔵 **Advanced Shell Script Interview Questions**

1. **Explain trap usage in Shell scripting.**

   ```bash
   trap 'echo "Signal caught. Cleaning up..."; exit' SIGINT SIGTERM
   ```

2. **How to debug a shell script?**

   * Add `set -x` for tracing execution.
   * `bash -x script.sh` to run with debug.

3. **Difference between `[[ ... ]]`, `[ ... ]`, and `(( ... ))`?**

   * `[[...]]`: advanced test command.
   * `[ ... ]`: POSIX test.
   * `((...))`: arithmetic evaluation.

4. **How to schedule a shell script to run every 5 minutes?**

   * Use crontab:

     ```
     */5 * * * * /path/to/script.sh
     ```

5. **How to use arrays in shell scripts?**

   ```bash
   arr=(one two three)
   echo ${arr[1]}  # two
   ```

---

## 🔴 **Scenario-Based Shell Script Questions**

1. **Scenario: Log file rotation**

   * Write a script to archive logs older than 7 days.

   ```bash
   find /var/log/myapp/ -type f -mtime +7 -exec gzip {} \;
   ```

2. **Scenario: Disk space alert**

   * Script to send an alert if disk usage exceeds 90%.

   ```bash
   THRESHOLD=90
   USAGE=$(df / | grep / | awk '{print $5}' | sed 's/%//')
   if [ "$USAGE" -gt "$THRESHOLD" ]; then
     echo "Disk usage critical: $USAGE%" | mail -s "Alert" user@example.com
   fi
   ```

3. **Scenario: Backup a directory**

   ```bash
   tar -czf /backup/app-$(date +%F).tar.gz /opt/app/
   ```

4. **Scenario: Monitor if a process is running**

   ```bash
   if pgrep myapp > /dev/null; then
     echo "Process running"
   else
     echo "Process not running"
   fi
   ```

5. **Scenario: Compare two files line by line**

   ```bash
   while read -r line1 && read -r line2 <&3; do
     [ "$line1" != "$line2" ] && echo "Mismatch: $line1 | $line2"
   done <file1.txt 3<file2.txt
   ```

6. **Scenario: Auto-remediation script for service crash**

   ```bash
   if ! pgrep nginx > /dev/null; then
     systemctl start nginx
     echo "nginx restarted at $(date)" >> /var/log/nginx-restart.log
   fi
   ```

---

## 🧠 Bonus Advanced Tasks (Common in Real Interviews)

1. **Script to extract failed login attempts**

   ```bash
   grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr
   ```

2. **Parse JSON in bash (via `jq`)**

   ```bash
   cat data.json | jq '.users[] | select(.active == true)'
   ```

3. **Automate Kubernetes rollout check**

   ```bash
   kubectl rollout status deployment/myapp -n dev
   ```

---

## ✅ Key Tips for Shell Script Interviews

* Use `#!/bin/bash` at the start.
* Always handle errors.
* Validate inputs and handle missing arguments.
* Know common file, string, and array operations.
* Be prepared to write live code in the interview.

---


