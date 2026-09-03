# Ansible Linux Training Lab

## What this project teaches

- Inventory and target hosts
- YAML playbook structure
- Variables and facts
- Modules and task results
- Loops and conditions
- Jinja templates
- Handlers and notifications
- Tags and selective execution
- Check mode and idempotency

## Open the project

```bash
ssh rhel-lab
cd ~/ansible-lab
ls -la
```

## Read the files

```bash
cat inventory.ini
cat linux_basics.yml
cat templates/system-report.j2
```

For easier reading:

```bash
less linux_basics.yml
```

Press `q` to exit `less`.

## Validate and run

```bash
ansible-playbook --syntax-check linux_basics.yml
ansible-playbook --check --diff linux_basics.yml
ansible-playbook linux_basics.yml
```

Run it again to prove idempotency. The second recap should show `changed=0`:

```bash
ansible-playbook linux_basics.yml
```

## Inspect what Ansible created

```bash
find ~/ansible-training -maxdepth 2 -type f -print
cat ~/ansible-training/configs/training.conf
cat ~/ansible-training/reports/system-report.txt
```

## Run selected tags

```bash
ansible-playbook linux_basics.yml --list-tags
ansible-playbook linux_basics.yml --tags information
ansible-playbook linux_basics.yml --tags report
```

## Edit safely

Create a backup, then edit:

```bash
cp linux_basics.yml linux_basics.yml.backup
nano linux_basics.yml
```

In Nano, save with `Ctrl+O`, press `Enter`, and exit with `Ctrl+X`.

After every edit:

```bash
ansible-playbook --syntax-check linux_basics.yml
ansible-playbook --check --diff linux_basics.yml
ansible-playbook linux_basics.yml
```

## Practise changing a variable

Change this line:

```yaml
student_name: Ahmed
```

Or override it without editing:

```bash
ansible-playbook linux_basics.yml -e student_name=trollmego
```

## AAP limitation

This local project does not automatically appear in cloud AAP. AAP projects synchronize playbooks from a Git repository. When you create your own GitHub repository, push this project there and connect an AAP Project to that URL. Cloud AAP will run it against its own inventory; it cannot directly reach the private Hyper-V address without approved company networking.
