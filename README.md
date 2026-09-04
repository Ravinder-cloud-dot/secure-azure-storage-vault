Building a Secure Cloud Storage Vault with an IP-based Firewall Restriction
Overview

This project implements a network-restricted Azure Storage Account to demonstrate how sensitive business data (e.g. backups, financial files, contracts) can be protected from public internet exposure using Azure Storage's built-in firewall, rather than relying on access keys or SAS tokens alone.

By default, Azure Storage accounts are reachable from any network. This project shows how to lock that down to a specific, approved IP address only — a common real-world requirement for compliance and data protection.


Architecture

        Public Internet
              │
     ┌────────┴─────────┐
     │  Storage Firewall  │   ← default: Deny all
     │  (Selected Networks)│
     └────────┬─────────┘
              │  allow only
     ┌────────▼─────────┐
     │  Whitelisted IP    │
     │  (Admin laptop)     │──✅ Access granted
     └────────────────────┘

     Any other IP (e.g. mobile hotspot) ──❌ Access denied

     
     Azure Services Used
     
Azure Storage Account (Blob Storage, LRS redundancy)
Storage Account Networking / Firewall rules ("Selected Networks")
Blob container with public/anonymous access disabled

Implementation Steps

Provisioned a Storage Account with Blob Storage, selecting Locally-Redundant Storage (LRS) to minimize cost for a lab/demo environment.
Created a private container (company-backup-vault) with anonymous/public blob access explicitly disabled at both the account and container level.
Configured the Networking firewall, switching from the default "All Networks" setting to "Selected Networks," and added a single approved public IPv4 address to the allow list.
Uploaded a test file from the whitelisted device to confirm authorized access worked end-to-end through the Azure Portal.

Validation / Testing

To confirm the firewall was actually enforcing access control (not just configured), I tested from two different network locations:

Test Device	Network	Result
Admin laptop	Whitelisted IP	✅ Successfully viewed and managed container contents
Mobile device	Different network (non-whitelisted IP)	❌ Access denied — Azure returned an authorization error, confirming the firewall actively blocks non-approved sources

This confirms the storage account is not relying on "security by obscurity" — it actively rejects requests from any IP not on the allow list, even with valid portal credentials.
