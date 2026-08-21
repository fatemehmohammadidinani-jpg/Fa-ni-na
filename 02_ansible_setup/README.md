# 02 — Ansible Setup

این پوشه برای آماده‌سازی سرور Ubuntu با Ansible است.

## اطلاعات سرور

- Host alias: `ubuntu_deploy`
- IP: `192.168.200.54`
- SSH user: `rahmati`
- Python interpreter: `/usr/bin/python3`
- Operating system: Ubuntu 22.04 LTS

## نکته معماری Nginx

در این پروژه Nginx روی Host با APT نصب نمی‌شود. یک کانتینر اولیه با نام
`bootstrap-nginx` توسط Docker Compose اجرا می‌شود. در فاز استقرار اپلیکیشن،
این کانتینر با Stack نهایی شامل Application و Nginx Reverse Proxy جایگزین خواهد شد.

## 1. نصب Ansible روی Controller

روش پیشنهادی با `pipx`:

```bash
sudo apt update
sudo apt install -y pipx
pipx ensurepath
source ~/.profile
pipx install --include-deps ansible
ansible --version
```

سپس Collectionهای مورد نیاز را نصب کنید:

```bash
cd 02_ansible_setup
ansible-galaxy collection install -r requirements.yml
```

## 2. بررسی SSH و sudo

ابتدا اتصال مستقیم را بررسی کنید:

```bash
ssh rahmati@192.168.200.54
```

در سرور مقصد مطمئن شوید کاربر اجازه sudo دارد:

```bash
sudo -v
python3 --version
```

برای استفاده از SSH Key:

```bash
ssh-copy-id rahmati@192.168.200.54
```

## 3. بررسی Inventory

```bash
ansible-inventory -i inventory --graph
```

## 4. ایجاد ping_test.txt

برای SSH Key:

```bash
ansible -i inventory deployment_servers \
  -m ansible.builtin.ping 2>&1 | tee ping_test.txt
```

برای SSH Password:

```bash
ansible -i inventory deployment_servers \
  -m ansible.builtin.ping -k 2>&1 | tee ping_test.txt
```

## 5. ایجاد facts.txt

برای SSH Key:

```bash
ansible -i inventory deployment_servers \
  -m ansible.builtin.setup 2>&1 | tee facts.txt
```

برای SSH Password:

```bash
ansible -i inventory deployment_servers \
  -m ansible.builtin.setup -k 2>&1 | tee facts.txt
```

## 6. بررسی Syntax

```bash
ansible-playbook -i inventory server_setup.yml --syntax-check
```

## 7. اجرای Playbook و ایجاد playbook_output.txt

اگر SSH با Key است و sudo رمز می‌خواهد:

```bash
ansible-playbook -i inventory server_setup.yml \
  --ask-become-pass 2>&1 | tee playbook_output.txt
```

اگر SSH و sudo هر دو با Password هستند:

```bash
ansible-playbook -i inventory server_setup.yml \
  --ask-pass --ask-become-pass 2>&1 | tee playbook_output.txt
```

## 8. ایجاد verification.txt

اگر sudo رمز می‌خواهد:

```bash
ansible-playbook -i inventory verification.yml \
  --ask-become-pass 2>&1 | tee verification.txt
```

اگر SSH و sudo هر دو با Password هستند:

```bash
ansible-playbook -i inventory verification.yml \
  --ask-pass --ask-become-pass 2>&1 | tee verification.txt
```

## خروجی نهایی مورد انتظار

```text
02_ansible_setup/
├── ansible.cfg
├── inventory
├── requirements.yml
├── server_setup.yml
├── verification.yml
├── ping_test.txt
├── facts.txt
├── playbook_output.txt
└── verification.txt
```

چهار فایل TXT باید با اجرای واقعی دستورات روی سرور تولید شوند؛ آن‌ها را با
خروجی نمونه یا ساختگی پر نکنید.

