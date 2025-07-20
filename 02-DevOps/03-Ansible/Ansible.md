## 🚀 **Ansible Interview Questions and Answers**

---

### 🧩 **Basic Ansible Interview Questions**

---

#### 1. **What is Ansible?**

**Answer:**
Ansible is an open-source automation tool for configuration management, application deployment, and task automation. It uses **SSH** and **YAML-based playbooks**.

---

#### 2. **What language is used to write Ansible playbooks?**

**Answer:**
**YAML (Yet Another Markup Language)**

---

#### 3. **Is Ansible agent-based or agentless?**

**Answer:**
**Agentless** – it uses **SSH** or **WinRM** to connect to nodes.

---

#### 4. **What are the components of Ansible?**

* **Inventory** – List of target hosts
* **Modules** – Units of work (e.g., `yum`, `copy`, `file`)
* **Playbooks** – YAML file describing automation tasks
* **Tasks** – Actual work inside a playbook
* **Roles** – Reusable collections of tasks
* **Facts** – System info collected from nodes
* **Handlers** – Triggered tasks on conditions

---

#### 5. **How do you run a simple ad-hoc command in Ansible?**

```bash
ansible all -m ping
```

---

#### 6. **What is the Ansible inventory file?**

**Answer:**
A file that lists all the target nodes (hosts) for playbooks. Example:

```ini
[webservers]
server1 ansible_host=192.168.1.100
```

---

#### 7. **What are modules in Ansible?**

**Answer:**
Modules are predefined units of code that do a specific task (e.g., `file`, `copy`, `service`, `yum`).

---

#### 8. **What is the difference between `play` and `task`?**

* **Play**: A group of tasks for a host/group
* **Task**: A single unit of action

---

#### 9. **How do you check the syntax of a playbook?**

```bash
ansible-playbook playbook.yml --syntax-check
```

---

#### 10. **How do you run an Ansible playbook?**

```bash
ansible-playbook site.yml -i inventory
```

---

### 🧪 **Intermediate Ansible Interview Questions**

---

#### 11. **What are variables in Ansible and where can you define them?**

**Answer:**
Variables can be defined in:

* `vars` section of playbook
* Inventory file
* Host/group vars directories
* Role defaults/vars
* Extra vars (`--extra-vars`)

---

#### 12. **What are facts in Ansible?**

**Answer:**
Facts are system details (OS, IP, memory, etc.) automatically gathered with the `setup` module.

---

#### 13. **How do you disable fact gathering?**

```yaml
gather_facts: no
```

---

#### 14. **How do you pass extra variables at runtime?**

```bash
ansible-playbook site.yml -e "version=1.2.3"
```

---

#### 15. **What is a role in Ansible?**

**Answer:**
A structured way to organize playbooks using folders: `tasks/`, `vars/`, `defaults/`, `handlers/`, etc.

---

#### 16. **What is a handler in Ansible?**

**Answer:**
A handler is a task triggered only when notified. Used for conditional actions like restarting services.

---

#### 17. **How do you reuse playbooks or tasks?**

* Include tasks: `include_tasks`, `import_tasks`
* Use roles

---

#### 18. **What is idempotency in Ansible?**

**Answer:**
Idempotency ensures that applying the same playbook multiple times doesn't change the system after the first run.

---

#### 19. **What is Ansible Vault?**

**Answer:**
It encrypts sensitive data like passwords or API keys in playbooks.

```bash
ansible-vault encrypt secrets.yml
```

---

#### 20. **How do you prompt for a password during runtime?**

```bash
ansible-playbook site.yml --ask-vault-pass
```

---

### 🔧 **Advanced Ansible Interview Questions**

---

#### 21. **How do you manage multiple environments (dev/stage/prod)?**

**Answer:**

* Use group\_vars and host\_vars
* Define inventory files per environment
* Use dynamic inventories

---

#### 22. **What is a dynamic inventory in Ansible?**

**Answer:**
An external script or plugin (e.g., AWS EC2 plugin) that generates inventory dynamically.

---

#### 23. **How do you conditionally execute tasks?**

```yaml
when: ansible_os_family == 'Debian'
```

---

#### 24. **How do you loop over tasks?**

```yaml
with_items:
  - apache
  - nginx
```

---

#### 25. **How do you notify handlers conditionally?**

```yaml
notify: restart nginx
when: nginx_status.changed
```

---

#### 26. **How do you use templates in Ansible?**

**Answer:**
Use the `template` module with **Jinja2** files:

```yaml
- name: Copy config
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf
```

---

#### 27. **What is the difference between `include_tasks` and `import_tasks`?**

| include\_tasks      | import\_tasks           |
| ------------------- | ----------------------- |
| Dynamic import      | Static import           |
| Executed at runtime | Executed during parsing |

---

#### 28. **How do you debug in Ansible?**

* Use `debug` module

```yaml
- debug: var=my_variable
```

---

#### 29. **What are filters in Ansible?**

**Answer:**
Jinja2 filters used to manipulate variables.
Example:

```yaml
{{ mylist | length }}
{{ 'Hello' | upper }}
```

---

#### 30. **How do you handle errors in Ansible?**

```yaml
ignore_errors: yes
```

Use `block`, `rescue`, and `always` for advanced error handling.

---

### 🔥 **Scenario-Based / Real-Time Ansible Interview Questions**

---

#### ✅ Scenario 1: *You need to deploy Nginx to 100 servers only if it's not installed.*

```yaml
- name: Ensure Nginx is installed
  yum:
    name: nginx
    state: present
```

---

#### ✅ Scenario 2: *Restart service only if config file is changed.*

```yaml
- name: Deploy config
  template:
    src: config.j2
    dest: /etc/nginx/nginx.conf
  notify: restart nginx

handlers:
  - name: restart nginx
    service:
      name: nginx
      state: restarted
```

---

#### ✅ Scenario 3: *Store credentials securely and use them in a playbook.*

* Encrypt with Vault:

```bash
ansible-vault encrypt secrets.yml
```

* Use in playbook:

```yaml
vars_files:
  - secrets.yml
```

---

#### ✅ Scenario 4: *Deploy different Java versions based on environment.*

```yaml
- name: Install Java
  yum:
    name: "{{ java_package }}"
    state: present
  vars:
    java_package: "{{ 'java-1.8.0-openjdk' if env == 'prod' else 'java-11-openjdk' }}"
```

---

#### ✅ Scenario 5: *Generate a configuration file dynamically using facts.*

```yaml
- name: Generate hosts file
  template:
    src: hosts.j2
    dest: /etc/hosts
```

`hosts.j2`:

```jinja
{% for host in ansible_play_hosts %}
{{ hostvars[host]['ansible_default_ipv4']['address'] }} {{ host }}
{% endfor %}
```

---

#### ✅ Scenario 6: *Run different tasks for Ubuntu and RHEL hosts.*

```yaml
tasks:
  - name: Install packages on Ubuntu
    apt: name=nginx state=present
    when: ansible_os_family == 'Debian'

  - name: Install packages on RHEL
    yum: name=nginx state=present
    when: ansible_os_family == 'RedHat'
```

---

#### ✅ Scenario 7: *Use role-based deployment structure.*

```yaml
site.yml:
- hosts: web
  roles:
    - nginx
    - deploy_app
```

Roles folder:

```
roles/
├── nginx/
│   └── tasks/main.yml
├── deploy_app/
│   └── tasks/main.yml
```

---

## ✅ **1. Basic Ansible Interview Questions**

### Q1. What is Ansible?

**Answer:**
Ansible is an open-source automation tool for configuration management, application deployment, orchestration, and provisioning using SSH and YAML-based playbooks.

---

### Q2. What language is used to write Ansible playbooks?

**Answer:**
YAML (YAML Ain’t Markup Language)

---

### Q3. How does Ansible work?

**Answer:**
Ansible uses SSH to communicate with remote machines and pushes configurations via modules defined in playbooks. It is agentless and uses an inventory file to manage nodes.

---

### Q4. What is an inventory file?

**Answer:**
A file that lists the IPs or hostnames of machines that Ansible manages. It can be static or dynamic.

---

### Q5. What are modules in Ansible?

**Answer:**
Modules are units of work like `copy`, `yum`, `service`, `file`, `shell`, etc., used in playbooks to execute tasks.

---

## 🔷 **2. Intermediate Level Questions**

### Q6. What is a playbook in Ansible?

**Answer:**
A playbook is a YAML file containing one or more "plays" that define the tasks and roles to be executed on target hosts.

---

### Q7. What are roles in Ansible?

**Answer:**
Roles are a way to organize playbooks into reusable components. They contain tasks, variables, handlers, templates, and files.

---

### Q8. What is the difference between `vars`, `defaults`, and `extra_vars`?

**Answer:**

* `defaults` (lowest precedence)
* `vars` (in playbooks or roles)
* `extra_vars` (passed via command line) – **highest precedence**

---

### Q9. How do you handle secrets in Ansible?

**Answer:**
Using **Ansible Vault** to encrypt sensitive data like passwords or keys:

```bash
ansible-vault encrypt secrets.yml
```

---

### Q10. What is a handler in Ansible?

**Answer:**
Handlers are tasks triggered by `notify` when something changes. Commonly used for restarting services after config updates.

---

## 🔶 **3. Advanced Questions**

### Q11. How do you debug a failing Ansible playbook?

**Answer:**

* Use `ansible-playbook -vvv playbook.yml` for verbose output
* Use the `debug` module in tasks
* Check `register` variables for command output
* Use `block/rescue/always` for exception handling

---

### Q12. How to register output of a task and use it in the next task?

**Answer:**

```yaml
- name: Get hostname
  command: hostname
  register: result

- name: Print hostname
  debug:
    msg: "The hostname is {{ result.stdout }}"
```

---

### Q13. What is the difference between `include_tasks`, `import_tasks`, and `include_role`?

**Answer:**

* `import_tasks`: Static import; evaluated at playbook parse time.
* `include_tasks`: Dynamic import; evaluated at runtime.
* `include_role`: Dynamically include a role.

---

### Q14. What are facts in Ansible?

**Answer:**
Facts are system properties gathered by Ansible like OS, IP, memory, etc. You can disable fact gathering using:

```yaml
gather_facts: false
```

---

### Q15. Explain Ansible pull mode.

**Answer:**
Instead of pushing configs from a control node, the target machine pulls configs from a Git repository using `ansible-pull`.

---

## 🟣 **4. Real-Time Scenario-Based Questions**

### Q16. You deployed a config change to 50 servers, but 10 failed. How do you retry?

**Answer:**
Use Ansible's `--limit @/path/to/last_failed.retry` to re-run the playbook on failed hosts.

---

### Q17. How do you loop through a list of users to create accounts?

**Answer:**

```yaml
- name: Create multiple users
  user:
    name: "{{ item }}"
    state: present
  loop:
    - user1
    - user2
    - user3
```

---

### Q18. How do you perform conditional execution?

**Answer:**

```yaml
when: ansible_os_family == 'Debian'
```

---

### Q19. A service restart breaks in production, how do you prevent playbook from stopping?

**Answer:**
Use `ignore_errors: yes` or `block/rescue`.

```yaml
- block:
    - name: Try to restart service
      service:
        name: nginx
        state: restarted
  rescue:
    - name: Notify team
      debug:
        msg: "Service restart failed"
```

---

### Q20. How do you find which task caused the failure in a big playbook?

**Answer:**

* Run with `-vvv` to get task-wise output.
* Use `tags` and run selective tasks.
* Use `--start-at-task="task name"`.

---

## 🧱 **5. Skeleton of Ansible Playbook**

```yaml
---
- name: Setup Web Server
  hosts: webservers
  become: yes
  vars:
    pkg_name: nginx

  tasks:
    - name: Install Nginx
      apt:
        name: "{{ pkg_name }}"
        state: present
        update_cache: yes

    - name: Start Nginx
      service:
        name: nginx
        state: started
        enabled: yes

    - name: Print service status
      shell: systemctl status nginx
      register: nginx_status

    - debug:
        var: nginx_status.stdout_lines
```

---

## 🧪 **6. Error Handling Examples**

### Error: `"msg": "The task includes an option with an undefined variable"`

**Fix:** Ensure variables are defined or use defaults:

```yaml
{{ my_var | default('default_value') }}
```

---

### Error: `"Failed to connect to the host via ssh"`

**Fix:**

* Check SSH access
* Update inventory file
* Use `ansible_user`, `ansible_ssh_private_key_file` if needed

---
