🧩 Windows Dynatrace Observability
Windows EKS Node Bootstrap Script for Dynatrace OneAgent

This repository contains a PowerShell bootstrap script used to install Dynatrace OneAgent on Windows-based Kubernetes nodes during instance initialization.
It enables log monitoring and observability for Windows pods, addressing the limitation that the Dynatrace Operator natively supports Linux nodes only.

📌 Overview

Dynatrace provides native container observability for Linux nodes via the Operator, but Windows Kubernetes nodes require an OS-level agent installation.

This project demonstrates how I enabled end-to-end observability for Windows workloads by installing Dynatrace OneAgent during Windows node bootstrap, ensuring consistent monitoring across mixed OS Kubernetes clusters.

🎯 Purpose

Install Dynatrace OneAgent on Windows Kubernetes nodes

Enable log monitoring for Windows-based pods

Automate agent installation during node provisioning

Achieve unified observability across Linux and Windows workloads

⚙️ What the Script Does

Defines a temporary location for the OneAgent installer

Downloads the Dynatrace OneAgent MSI from internal object storage

Installs the agent silently using msiexec

Verifies that the Dynatrace service is successfully installed and running

📜 PowerShell Script
$installerPath = "C:\Windows\Temp\Dynatrace-OneAgent.msi"

# Download installer from internal storage
aws s3 cp s3://<bucket>/Dynatrace-OneAgent.msi $installerPath

# Install Dynatrace OneAgent silently
Start-Process msiexec.exe `
  -ArgumentList "/i `"$installerPath`" /quiet /norestart" `
  -Wait

# Verify Dynatrace service
Get-Service | Where-Object { $_.DisplayName -like "*Dynatrace*" }

✅ Expected Outcome

Dynatrace OneAgent installed on the Windows node

Dynatrace service running successfully

Windows hosts and Kubernetes pod logs visible in Dynatrace

Improved troubleshooting and observability for Windows workloads

📝 Usage Notes

Requires administrative privileges

AWS CLI must be available on the instance

Intended for:

EC2 user data

Launch templates

Automated Windows node provisioning

🚀 Use Cases

EKS clusters with Windows worker nodes

Windows-based microservices (.NET, IIS, background services)

Enterprises requiring unified observability across platforms

🧠 Key Learnings

Windows Kubernetes observability requires OS-level instrumentation

Dynatrace OneAgent integrates effectively with Windows container runtimes

Automating agent installation during bootstrap ensures scalability and consistency

📄 About

This project demonstrates how I enabled log monitoring and observability for Windows-based Kubernetes pods using Dynatrace OneAgent, overcoming the limitation of Linux-only Dynatrace Operator support. By installing OneAgent at the OS level during Windows node bootstrap, I achieved end-to-end visibility for Windows workloads running in Kubernetes.

🏷 Tags

kubernetes · windows-containers · dynatrace · observability · devops · sre · eks
