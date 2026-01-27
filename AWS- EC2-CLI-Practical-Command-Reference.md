# AWS EC2 CLI – Practical Command Reference

![AWS EC2 overview](https://docs.aws.amazon.com/images/AWSEC2/latest/UserGuide/images/ec2-instance.png)

This is a practical, curated list of the most commonly used AWS EC2 commands (via the AWS CLI). These focus on core instance lifecycle management, monitoring, security, and related resources.

The commands are grouped by category and presented roughly in a logical order of typical usage for a basic workflow:

- Prepare access (key pairs)
- Launch/query instances
- Manage instance state
- Configure security/networking
- Manage storage/images (advanced)
- Troubleshooting/monitoring

Importance scale (1–5): 5 = essential for almost every user; 1 = niche/specialized.

---

## Prepare Access (Key Pairs)

![EC2 key pairs](https://docs.aws.amazon.com/images/AWSEC2/latest/UserGuide/images/key-pair.png)

### `aws ec2 create-key-pair`
Creates a new SSH key pair and downloads the private key.

How it works — Generates key material in AWS; you save the `.pem` file.

When to use — Before launching instances that require SSH/RDP access (Linux/Windows).

Importance — 5 (critical for secure access).

Order — Often first step in manual setups.

---

### `aws ec2 describe-key-pairs`
Lists available key pairs in your account/region.

How it works — Returns key names, fingerprints, etc.

When to use — To check existing keys before referencing one in launch.

Importance — 4.

---

## Launch and Query Instances

![EC2 instance lifecycle](https://docs.aws.amazon.com/images/AWSEC2/latest/UserGuide/images/instance_lifecycle.png)

### `aws ec2 run-instances`
Launches one or more new EC2 instances from an AMI.

How it works — Specify `--image-id` (AMI), `--instance-type`, `--key-name`, `--subnet-id`, `--security-group-ids`, user data, etc.

When to use — To create new virtual servers (on-demand, spot, etc.).

Importance — 5 (core creation command).

Order — Primary launch step after prep.

---

### `aws ec2 describe-instances`
Retrieves detailed info about instances (state, IP, type, tags, etc.).

How it works — Use `--instance-ids`, `--filters` (e.g., `Name=tag:Name,Values=MyServer`), `--query` for formatted output.

When to use — Inventory checks, status monitoring, scripting, troubleshooting.

Importance — 5 (most frequently run command).

Order — Right after launch to confirm success/get IDs/IPs.

---

## Manage Instance State

![Start and stop instances](https://docs.aws.amazon.com/images/AWSEC2/latest/UserGuide/images/stop-start.png)

### `aws ec2 start-instances`
Starts one or more stopped instances.

How it works — `--instance-ids i-xxx` (retains IP, EBS data).

When to use — Resume paused workloads to save costs.

Importance — 4.

---

### `aws ec2 stop-instances`
Stops running instances (graceful shutdown).

How it works — Stops the OS; EBS volumes remain attached.

When to use — Cost saving or maintenance (EBS charges continue).

Importance — 4.

---

### `aws ec2 reboot-instances`
Reboots running instances.

How it works — Equivalent to OS reboot command.

When to use — Apply OS updates or resolve transient issues.

Importance — 3.

---

### `aws ec2 terminate-instances`
Permanently deletes instances.

How it works — Irreversible; EBS volumes deleted unless configured otherwise.

When to use — Cleanup unused resources.

Importance — 4 (use with caution).

---

## Configure Security and Networking

![Security groups](https://docs.aws.amazon.com/images/AWSEC2/latest/UserGuide/images/security-group-rules.png)

### `aws ec2 describe-security-groups`
Lists security groups and their rules.

How it works — Filter by `--group-ids`, VPC, etc.

When to use — Audit firewall rules.

Importance — 4.

---

### `aws ec2 authorize-security-group-ingress` / `authorize-security-group-egress`
Adds inbound/outbound rules to a security group.

How it works — Specify `--group-id`, `--protocol`, `--port`, `--cidr`.

When to use — Open ports (e.g., SSH 22, HTTP 80).

Importance — 5 (essential for connectivity).

Order — Often before or after launch if default SG is insufficient.

---

### `aws ec2 revoke-security-group-ingress` / `revoke-security-group-egress`
Removes rules from a security group.

How it works — Mirror of authorize but removes matching rule.

When to use — Tighten security or fix errors.

Importance — 4.

---

## Manage Storage and Images (Advanced)

![EBS volumes](https://docs.aws.amazon.com/images/AWSEC2/latest/UserGuide/images/ebs-volume.png)

### `aws ec2 create-volume`
Creates an EBS volume.

How it works — Specify size, type (`gp3`, `io2`), availability zone.

When to use — Add extra storage.

Importance — 3.

---

### `aws ec2 attach-volume`
Attaches an EBS volume to an instance.

How it works — Specify volume ID, instance ID, device name (e.g., `/dev/sdf`).

When to use — After creation or moving volumes.

Importance — 3.

---

### `aws ec2 describe-volumes`
Lists EBS volumes and status.

How it works — Filter by attachment, tags, etc.

Importance — 3.

---

### `aws ec2 create-image`
Creates an AMI from a running/stopped instance.

How it works — Captures instance as reusable image.

When to use — For backups, cloning, or golden images.

Importance — 3 (common in automation).

---

### `aws ec2 describe-images`
Lists available AMIs (owned, public, etc.).

How it works — Filter by owner, name, etc.

When to use — Find AMIs for launch.

Importance — 4.

---

## Troubleshooting and Monitoring

![CloudWatch metrics](https://docs.aws.amazon.com/images/AmazonCloudWatch/latest/monitoring/images/cloudwatch-metrics.png)

### `aws ec2 monitor-instances` / `unmonitor-instances`
Enables/disables detailed CloudWatch monitoring (5-min vs 1-min).

When to use — For higher-resolution metrics.

Importance — 2.

---

### `aws ec2 get-console-output`
Retrieves recent console (boot) logs from an instance.

When to use — Debug boot failures or issues.

Importance — 3 (troubleshooting).

---

## Typical Workflow Order

![EC2 workflow](https://docs.aws.amazon.com/images/AWSEC2/latest/UserGuide/images/ec2-workflow.png)

1. `create-key-pair` (if needed)
2. `describe-instances` / `describe-images` (scout resources)
3. `run-instances`
4. `describe-instances` (wait for running state, get IP)
5. `authorize-security-group-ingress` (if needed for access)
6. `start` / `stop` / `reboot` as needed
7. `terminate-instances` (cleanup)

---

These commands cover ~80–90% of day-to-day EC2 CLI usage. For advanced setups (Auto Scaling, Spot, VPC networking), additional commands like those for VPCs, subnets, or launch templates apply. Always use `--region`, `--profile`, or filters to target specific resources, and `--dry-run` to test without changes. Refer to official AWS CLI EC2 reference for full parameters and options.
