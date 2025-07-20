### 🧠 **Beginner Python Interview Questions**

1. **What is Python?**

   * A high-level, interpreted, general-purpose programming language known for readability.

2. **What are Python’s key features?**

   * Interpreted, dynamically typed, object-oriented, vast standard library, supports functional programming.

3. **What are Python data types?**

   * `int`, `float`, `str`, `list`, `tuple`, `dict`, `set`, `bool`, `NoneType`

4. **What is the difference between list and tuple?**

   * `List`: Mutable, slower. `Tuple`: Immutable, faster.

5. **How is memory managed in Python?**

   * Through reference counting and garbage collection (`gc` module).

6. **What is PEP 8?**

   * Python Enhancement Proposal for coding style guidelines.

7. **What is the difference between `is` and `==`?**

   * `is`: object identity. `==`: value equality.

8. **How do you handle exceptions in Python?**

   ```python
   try:
       # risky code
   except Exception as e:
       print(e)
   finally:
       # always run
   ```

9. **Explain indentation in Python.**

   * Python uses indentation (4 spaces) to define code blocks, not `{}`.

10. **What is a function in Python?**

    * A reusable block of code defined using `def`.

---

### ⚙️ **Intermediate Python Interview Questions**

1. \*\*What are \*args and **kwargs?**

   ```python
   def demo(*args, **kwargs):
       print(args)
       print(kwargs)
   ```

2. **What are lambda functions?**

   * Anonymous functions: `lambda x: x + 1`

3. **What is list comprehension?**

   ```python
   squares = [x*x for x in range(10)]
   ```

4. **What are generators?**

   ```python
   def gen():
       yield 1
   ```

5. **Difference between `deepcopy()` and `copy()`?**

   * `copy()`: shallow copy. `deepcopy()`: recursive copy.

6. **What are Python decorators?**

   * Functions that modify the behavior of other functions.

   ```python
   def decorator(fn):
       def wrapper():
           print("Before")
           fn()
           print("After")
       return wrapper
   ```

7. **What is a Python module vs package?**

   * Module: `.py` file. Package: folder with `__init__.py`.

8. **Explain Python’s GIL.**

   * Global Interpreter Lock – allows only one thread to execute at a time.

9. **How does Python manage multithreading?**

   * Using `threading` or `concurrent.futures`, but GIL limits CPU-bound use cases.

10. **What are Python’s built-in data structures?**

    * `list`, `dict`, `set`, `tuple`

---

### 🧪 **Advanced Python Interview Questions**

1. **What is metaclass in Python?**

   * A class of a class. Used to customize class creation.

2. **How do you implement caching in Python?**

   ```python
   from functools import lru_cache
   @lru_cache(maxsize=128)
   def expensive_fn(n):
       return n**n
   ```

3. **How does Python handle memory leaks?**

   * Through cyclic garbage collector; still possible if using global vars or circular refs.

4. **Explain monkey patching.**

   * Dynamically changing a module or class at runtime.

5. **What is context manager in Python?**

   ```python
   with open("file.txt") as f:
       data = f.read()
   ```

6. **How would you debug a memory issue in Python?**

   * Use `tracemalloc`, `objgraph`, `gc`, `memory_profiler`.

7. **What are coroutines and `async/await`?**

   * Used for asynchronous programming.

   ```python
   async def main():
       await some_coroutine()
   ```

8. **How do you serialize Python objects?**

   * Using `pickle`, `json`, or `marshal`.

9. **How would you profile a Python application?**

   * Using `cProfile`, `line_profiler`, `timeit`.

10. **What is the difference between `@classmethod`, `@staticmethod`, and instance method?**

* `classmethod`: receives class, `staticmethod`: no implicit arg, instance method receives object.

---

### 🔍 **Real-Time Scenario-Based Python Questions**

1. **How would you design a retry mechanism in Python for a failing API call?**

   ```python
   import time
   for _ in range(3):
       try:
           call_api()
           break
       except:
           time.sleep(2)
   ```

2. **How do you process large files line-by-line without loading into memory?**

   ```python
   with open("large.log") as f:
       for line in f:
           process(line)
   ```

3. **How to read config from `.env` file securely?**

   ```python
   from dotenv import load_dotenv
   import os
   load_dotenv()
   secret = os.getenv("API_KEY")
   ```

4. **How to build a REST API with Python?**

   * Use **FastAPI** or **Flask**

   ```python
   from fastapi import FastAPI
   app = FastAPI()

   @app.get("/")
   def read_root():
       return {"msg": "Hello"}
   ```

5. **How to implement logging instead of print statements?**

   ```python
   import logging
   logging.basicConfig(level=logging.INFO)
   logging.info("Started")
   ```

---

## ✅ **Most Common Python Questions for Experienced DevOps Engineers**

### 🟢 **Basic to Intermediate**

1. **What are Python virtual environments, and why are they useful in DevOps?**
   Virtual environments allow you to manage dependencies for different projects in isolation, which is crucial in CI/CD pipelines to avoid version conflicts.

2. **How do you read/write files in Python?**

   ```python
   with open('file.txt', 'r') as file:
       data = file.read()

   with open('output.txt', 'w') as file:
       file.write("Hello World")
   ```

3. **What’s the difference between a list and a tuple?**

   * List: Mutable (`[]`)
   * Tuple: Immutable (`()`)

4. **How do you handle exceptions in Python?**

   ```python
   try:
       result = 10 / 0
   except ZeroDivisionError:
       print("Cannot divide by zero")
   ```

---

### 🔵 **Advanced & Real-Time (DevOps Specific)**

5. **How do you automate repetitive tasks using Python in DevOps pipelines?**
   Examples:

   * Deploying code (with `subprocess` or `fabric`)
   * Parsing YAML (for Helm/K8s)
   * Writing Ansible dynamic inventory scripts

6. **How do you parse JSON, YAML, or INI config files in Python?**

   ```python
   import yaml
   with open("values.yaml") as f:
       config = yaml.safe_load(f)
   ```

7. **How do you monitor log files in real-time using Python?**
   Tail a file:

   ```python
   import time
   with open('/var/log/syslog') as f:
       f.seek(0, 2)  # Move to EOF
       while True:
           line = f.readline()
           if line:
               print(line.strip())
           time.sleep(1)
   ```

8. **How would you write a health-check API in Python (FastAPI/Flask)?**
   Flask example:

   ```python
   from flask import Flask
   app = Flask(__name__)

   @app.route("/health")
   def health():
       return {"status": "ok"}

   if __name__ == "__main__":
       app.run(host="0.0.0.0", port=5000)
   ```

---

## ⚙️ **Python + DevOps Real-World Project Ideas**

| Project Name                     | Description                                                                      | Tools Involved                           |
| -------------------------------- | -------------------------------------------------------------------------------- | ---------------------------------------- |
| **1. CI/CD Validator**           | A Python script that validates YAML/JSON CI pipelines before pushing.            | Python, GitHub/GitLab CI                 |
| **2. Log Analyzer**              | Parse system/app logs, filter error logs, and send email/slack alerts.           | Python, logging, SMTP/Slack APIs         |
| **3. Dynamic Ansible Inventory** | Auto-fetch AWS/GCP resources & generate dynamic Ansible inventory.               | Boto3, Python, Ansible                   |
| **4. Kubernetes Auto-Restarter** | Monitor unhealthy pods and restart based on labels.                              | Python, `kubectl`, `subprocess`, k8s API |
| **5. Infra Cost Reporter**       | Python script to fetch cloud usage (AWS Cost Explorer) and email a daily report. | Boto3, SMTP                              |
| **6. Helm Template Validator**   | Script to validate multi-env Helm chart values.yaml files.                       | `pyyaml`, subprocess, `helm`             |
| **7. Custom Monitoring API**     | Build a REST API to fetch system metrics (CPU, memory, disk).                    | FastAPI, psutil                          |

---

## 🔴 **Common DevOps Interview Python Questions (Experienced)**

1. **How do you interact with Kubernetes using Python?**
   Use the official [kubernetes-client/python](https://github.com/kubernetes-client/python).

   ```python
   from kubernetes import client, config
   config.load_kube_config()
   v1 = client.CoreV1Api()
   print([pod.metadata.name for pod in v1.list_pod_for_all_namespaces().items])
   ```

2. **How do you securely manage secrets in Python?**
   Use `dotenv` or `os.environ`. Avoid hardcoding.

   ```python
   import os
   os.environ['AWS_SECRET_ACCESS_KEY']
   ```

3. **How do you test your Python automation scripts?**

   * Use `pytest` for testing
   * Use `moto` for mocking AWS
   * Use `unittest.mock` for mocking shell commands

4. **How do you write idempotent Python scripts in infrastructure automation?**
   Ensure the script checks resource existence before acting (e.g., check if a user exists before creating).

---

## ✅ Should You Know More?

Here’s what you **should definitely prepare additionally**:

| Topic                    | Why It Matters                       |
| ------------------------ | ------------------------------------ |
| Python with AWS (boto3)  | For provisioning, inventory, alerts  |
| YAML/JSON parsing        | CI/CD, Kubernetes, Ansible           |
| Python subprocess        | Running shell commands inside Python |
| REST API scripting       | Monitoring, automation, integrations |
| Error Handling & Logging | Real-time debugging and alerts       |
| Python + GitHub API      | Auto PRs, commit validations, etc.   |

---

