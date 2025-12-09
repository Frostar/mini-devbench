# Mini Developer Bench

This ansible playbook configures an Alpine container for interactive development or debugging.
Ideal for CTF play in catogories reverse engineer or pwn.

**Highligthed features**
- Low privileged user `developer` with zsh shell with custom configuration and aliases (can be configured in [vars](vars.yml)).
- SSH login with public key authentication (see [vars](vars.yml) for to specify host public key)
- doas (`sudo` alternative) configured for privilege escalation
- tmux with pre-configured setup
- QoL CLI tools: `zoxide` (smart cd), `eza` (modern ls), and `delta` (git diff viewer)
- Docker and Docker Compose with user added to docker group
- Network tools: `nmap`, `netcat-openbsd`, `socat`, `httpie`, and `mitmproxy`
- Debugging tools: `gdb` with `peda` (Python Exploit Development Assistance), `strace`, and `ltrace`
- Other various essentials: `git`, `vim`, `curl`, `wget`, `rsync`, `tree`, `htop`, `ripgrep`, `xxd`, and `alpine-sdk`


## Prerequisites

###  Host setup

1. Install Ansible and Ansible Lint in a virtual environment (recommended)
   ```sh
   python3 -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   pip install ansible ansible-lint
   ```

2. Install Ansible collections
   ```sh
   ansible-galaxy collection install -r requirements.yml
   ```

### Target Setup
SSH access with key pair to Alpine with Python.

This can be bootstrapped with following in the target container
```sh
apk add openssh-server
service sshd start
apk add python3
```

## Run the playbook

1. First setup a `host.ini` file with target IP.
There is a example in [host.ini.example](hosts.ini.example).

2. Add password file `user_password.txt`
There is a example in [user_password.txt.example](user_password.txt.example).

3. Run playbook
`ansible-playbook -i hosts.ini playbook.yml`

4. Enjoy.
SSH into the target container with the public key and password you set in the [vars](vars.yml) and use `doas` to run commands as root.


---


**Disclaimer**: This repository was developed with the assistance of an AI assistant.
Please review all code and configurations before use in production environments.