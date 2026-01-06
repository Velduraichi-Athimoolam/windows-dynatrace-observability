📜 Windows EC2 User Data Script – Dynatrace OneAgent Installation

This PowerShell script automates the installation of Dynatrace OneAgent on Windows-based Kubernetes nodes during instance bootstrap.
It is designed to be used as EC2 user data or during Windows node initialization to enable observability for Windows pods.

🎯 Purpose

Install Dynatrace OneAgent on Windows nodes

Enable log monitoring and observability for Windows Kubernetes pods

Ensure consistent and automated agent installation across environments

⚙️ What the Script Does

Defines a temporary location for the OneAgent installer

Downloads the Dynatrace OneAgent MSI from internal object storage

Installs the agent silently using msiexec

Verifies that the Dynatrace service is successfully installed


✅ Expected Outcome

Dynatrace OneAgent is installed on the Windows node

Dynatrace service is running

Windows host and pod logs become visible in Dynatrace

📝 Usage Notes

Requires administrative privileges

AWS CLI must be available on the instance

Intended for automated environments (EC2 user data / launch templates)
