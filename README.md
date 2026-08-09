# Ansible Application Configuration Backup

This project contains an Ansible playbook that creates a dated backup of the application's `appsettings.json` configuration file.

## What this playbook does

The playbook:

1. Runs on the local machine.
2. Creates a `/backup` directory.
3. Copies `/opt/app/config/appsettings.json` to the backup directory.
4. Adds the current date to the backup filename.
5. Verifies that the backup file was created.
6. Displays a success message when the backup exists.

## Project Structure

```text
sre-task/
├── README.md
├── backup.yml
└── inventory
```

## Prerequisites

Before running the playbook, make sure:

* Ansible is installed.
* The file `/opt/app/config/appsettings.json` exists.
* The user running Ansible has sufficient privileges to create `/backup` and read the application configuration file.

## Clone the Repository

Clone the repository using:

```bash
git clone https://github.com/18041999akshaykumar/sre-task.git


Then enter the project directory:

```bash
cd sre-task
```

## Inventory

The `inventory` file contains:

```ini
[local]
localhost ansible_connection=local
```

This means Ansible will execute the playbook on the same machine where Ansible is being run.

## Run the Playbook

Run:

```bash
ansible-playbook -i inventory backup.yml
```

The playbook uses privilege escalation (`become: true`), so you may be prompted for your sudo password depending on your system configuration.

## Verify the Backup

After successful execution, check the backup directory:

```bash
ls -l /backup/
```

You should see a file similar to:

```text
appsettings.json_2026-08-09
```

The date in the filename will depend on the day the playbook is executed.

## Expected Result

A successful execution should create a dated backup of:

```text
/opt/app/config/appsettings.json
```

inside:

```text
/backup/
```

and display the success message from the playbook.

