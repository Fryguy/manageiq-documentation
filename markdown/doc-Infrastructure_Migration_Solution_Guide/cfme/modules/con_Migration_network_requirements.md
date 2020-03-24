The network communication between the VMware environment, the Red Hat
environment, the conversion hosts, and CloudForms must be uninterrupted
and reliable.

The firewall rules must enable the following ports for migration.

| Port | Protocol | Source           | Destination       |
| ---- | -------- | ---------------- | ----------------- |
| 22   | TCP      | CloudForms       | Conversion hosts  |
| 443  | TCP      | CloudForms       | VMware ESXi hosts |
| 902  | TCP      | CloudForms       | VMware ESXi hosts |
| 902  | TCP      | Conversion hosts | VMware ESXi hosts |
| 5480 | TCP      | Conversion hosts | VMware vCenter    |

Firewall rules for migration
