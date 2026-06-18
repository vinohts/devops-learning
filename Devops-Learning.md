# DevOps Learning Project

## Master Learning Document

### Prepared By: Vino

### Date: June 2026

---

# Project Information

Project Name:

```text
DevOps Learning Project
```

Learning Objectives:

```text
Git
GitHub
Jenkins
Groovy Pipeline
Ansible
Packer
Golden AMI
AWS Lambda
Launch Template
Auto Scaling Group (ASG)
Application Load Balancer (ALB)
```

Working Directory:

```text
D:\2026\IAC\devops-learning
```

---

# Current Learning Status

```text
Phase 1 - COMPLETED
Phase 2 - COMPLETED
Phase 3 - IN PROGRESS (Ansible)
Phase 4 - FUTURE (Packer & Golden AMI)
Phase 5 - FUTURE (Launch Template & ASG)
Phase 6 - FUTURE (Lambda Automation)
```

---

# Phase 1 - Project Setup

## Objective

Create a local DevOps project structure and initialize source control using Git.

---

## Environment Setup

Operating System:

```text
Windows 11
```

Installed Software:

```text
Git Version  : 2.51.0.windows.2
Java Version : OpenJDK 21
Jenkins      : Installed
VS Code      : Installed
WSL Ubuntu   : Installed
```

---

## Project Structure

```text
devops-learning

│   Jenkinsfile
│   README.md

├───ami-bake
│       README.md

├───ansible
│       install-nginx.yml
│       inventory.ini

├───app-infra
│       README.md

└───static-infra
        README.md
```

---

## Git Initialization

Commands Executed:

```bash
git init

git add .

git commit -m "Initial DevOps Learning Project"
```

---

## Concepts Learned

### Git Repository

A repository is a directory tracked by Git.

### Git Add

```bash
git add .
```

Moves files into the staging area.

### Git Commit

```bash
git commit -m "message"
```

Creates a snapshot of changes.

---

## Phase 1 Outcome

Successfully Completed:

```text
✓ Project Folder Creation

✓ DevOps Folder Structure Creation

✓ Jenkinsfile Creation

✓ Git Repository Initialization

✓ First Commit Creation
```

---

# Phase 2 - GitHub & Jenkins Integration

## Objective

Connect GitHub with Jenkins and execute a Jenkins Pipeline using a Jenkinsfile stored in GitHub.

---

## GitHub Repository

Repository:

```text
devops-learning
```

Contents:

```text
Jenkinsfile
README.md
ami-bake/
ansible/
app-infra/
static-infra/
```

---

## Jenkins Pipeline Configuration

Job Type:

```text
Pipeline
```

Definition:

```text
Pipeline script from SCM
```

SCM:

```text
Git
```

Branch:

```text
main
```

Pipeline Script:

```text
Jenkinsfile
```

---

## Jenkinsfile

```groovy
pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checkout Stage'
            }
        }

        stage('Validate') {
            steps {
                echo 'Validate Stage'
            }
        }

        stage('Ansible') {
            steps {
                echo 'Ansible Stage'
            }
        }

        stage('AMI Bake') {
            steps {
                echo 'AMI Bake Stage'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy Stage'
            }
        }
    }
}
```

---

## Pipeline Execution Flow

```text
GitHub
   ↓
Jenkins
   ↓
Checkout
   ↓
Validate
   ↓
Ansible
   ↓
AMI Bake
   ↓
Deploy
   ↓
SUCCESS
```

---

## Jenkins Concepts Learned

### Pipeline

Defines the complete CI/CD workflow.

### Stage

Represents a logical section of work.

### Steps

Contains executable actions.

### Echo

Prints messages to Jenkins console output.

### Workspace

Temporary directory where Jenkins downloads code and executes builds.

Flow:

```text
GitHub
    ↓
Workspace
    ↓
Pipeline Execution
```

---

## Phase 2 Outcome

Successfully Completed:

```text
✓ GitHub Repository Integration

✓ Jenkins Job Creation

✓ Jenkinsfile Execution

✓ Pipeline From SCM

✓ Jenkins Workspace Understanding

✓ Basic Groovy Pipeline Syntax
```

---

# Enterprise Deployment Workflow Understanding

## Real Project Architecture

Based on current project analysis:

```text
Developer
    ↓
GitHub
    ↓
Jenkins
    ↓
Run Ansible
    ↓
Run Packer
    ↓
Bake Golden AMI
    ↓
Create New AMI ID
    ↓
Lambda Trigger
    ↓
Update Launch Template
    ↓
ASG Instance Refresh
    ↓
New Windows Servers
    ↓
ALB
    ↓
Users
```

---

# Step 1 - Developer Push

Developer commits code and pushes to GitHub.

Example:

```text
Version 1.0
      ↓
Version 1.1
```

---

# Step 2 - GitHub Trigger

GitHub webhook triggers Jenkins automatically.

```text
Developer Push
      ↓
GitHub
      ↓
Jenkins
```

---

# Step 3 - Jenkins Pipeline

Jenkins acts as the deployment orchestrator.

Typical stages:

```text
Checkout
      ↓
Build
      ↓
Ansible
      ↓
Packer
      ↓
Create AMI
```

---

# Step 4 - Ansible

Important Understanding:

```text
Ansible does NOT deploy directly to Production Servers.
```

Ansible prepares a temporary build machine.

Typical tasks:

```text
Install IIS

Install Security Agents

Install Monitoring Agents

Copy Application

Apply Configurations
```

Result:

```text
Configured Build Server
```

---

# Step 5 - Packer

Packer creates a reusable machine image.

```text
Configured Server
       ↓
Packer
       ↓
Golden AMI
```

Example Files:

```text
windows-golden-ami.pkr.hcl
windows-golden-ami.json
```

---

# Step 6 - Golden AMI

Example:

```text
AMI-001
```

Contains:

```text
Windows OS

Application

Security Tools

Monitoring Tools

Configurations
```

This is called a Golden AMI.

---

# Step 7 - New AMI Version

Example:

```text
AMI-001
      ↓
AMI-002
```

Every deployment creates a new AMI.

---

# Step 8 - Lambda Trigger

Lambda acts as an automation coordinator.

Typical actions:

```text
Read New AMI ID
      ↓
Update Launch Template
      ↓
Start ASG Refresh
      ↓
Send Notifications
```

Lambda does not deploy applications.

---

# Step 9 - Launch Template Update

Before:

```text
Launch Template
      ↓
AMI-001
```

After:

```text
Launch Template
      ↓
AMI-002
```

Launch Template always points to the latest approved AMI.

---

# Step 10 - ASG Instance Refresh

Current State:

```text
EC2-A → AMI-001

EC2-B → AMI-001

EC2-C → AMI-001
```

Refresh Process:

```text
Terminate EC2-A
      ↓
Launch EC2-D
      ↓
AMI-002
```

Then:

```text
Terminate EC2-B
      ↓
Launch EC2-E
      ↓
AMI-002
```

Then:

```text
Terminate EC2-C
      ↓
Launch EC2-F
      ↓
AMI-002
```

Result:

```text
All Servers Running New AMI
```

---

# Step 11 - ALB Validation

ALB performs health checks.

```text
Healthy?
    ↓
YES
    ↓
Send Traffic
```

If unhealthy:

```text
No Traffic
```

This enables rolling deployment with minimal downtime.

---

# Step 12 - Deployment Complete

Final Architecture:

```text
Launch Template
      ↓
Latest AMI
      ↓
ASG
      ↓
New EC2 Instances
      ↓
ALB
      ↓
Users
```

---

# Key Technology Roles

## GitHub

```text
Source Code Repository
```

## Jenkins

```text
Deployment Orchestrator
```

## Ansible

```text
Configuration Management Tool
```

## Packer

```text
Golden AMI Creation Tool
```

## Golden AMI

```text
Preconfigured Machine Image
```

## Lambda

```text
Infrastructure Automation Trigger
```

## Launch Template

```text
EC2 Blueprint
```

## ASG

```text
Server Lifecycle Manager
```

## ALB

```text
Traffic Distribution Layer
```

---

# Most Important Understanding

Traditional Deployment:

```text
Ansible
    ↓
Production Server
```

My Project Deployment Model:

```text
Ansible
    ↓
Temporary Build Server
    ↓
Golden AMI
    ↓
Launch Template
    ↓
ASG
    ↓
Production Servers
```

This deployment strategy is called:

```text
Immutable Infrastructure using Golden AMI Pattern
```

---

# Current Learning Goal

Next Focus Area:

```text
Ansible
      ↓
Packer
      ↓
Golden AMI
```

After that:

```text
Launch Template
      ↓
ASG
      ↓
Lambda
```

This sequence matches the actual enterprise deployment flow used in the project.
