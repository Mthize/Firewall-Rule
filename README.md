# Firewall Rule Management for Cymbal Bank's Demo Web Server

## Project Overview

This project involves configuring and testing firewall rules to secure Cymbal Bank's demo web server deployed on a Virtual Private Cloud (VPC). The goal is to manage inbound network traffic effectively by creating appropriate firewall rules.

## Prerequisites

- Access to a custom-mode network VPC named `vpc-net`.
- A subnet named `vpc-subnet`.
- A VM instance named `web-server` with an Apache web server installed.
- The VM instance is tagged with `http-server`.
- VPC Flow Logs are enabled in the default region.
- Access to the default zone.

## Objectives

1. Create a firewall rule to allow inbound HTTP traffic to the web server.
2. Generate HTTP network traffic to test the rule and analyze network logs.
3. Create and test a firewall rule to deny HTTP traffic to the web server.
4. Analyze firewall logs to ensure the deny rule is working correctly.

## Tasks

### 1. Create a Firewall Rule to Allow Network Traffic

**Steps:**

1. **Navigate to Firewall Rules:**
   - Open your cloud provider's console.
   - Go to the **Networking** section and select **Firewall Rules**.

2. **Create a New Rule:**
   - **Name**: `allow-http-traffic`
   - **Network**: `vpc-net`
   - **Priority**: 1000 (lower numbers are higher priority)
   - **Direction**: Ingress
   - **Action**: Allow
   - **Source IP Ranges**: `0.0.0.0/0` (or restrict to specific IP ranges if necessary)
   - **Protocols and Ports**: `tcp:80`
   - **Target Tags**: `http-server`

3. **Save and Apply the Rule.**

**Verification:**

- Access the web server via a browser or `curl`: `http://<web-server-ip>`.
- Ensure the server responds correctly to HTTP requests.

### 2. Generate HTTP Network Traffic and Analyze Logs

**Steps:**

1. **Generate HTTP Traffic:**
   - Open a web browser or use `curl` to send HTTP requests to the server: `http://<web-server-ip>`.
   - Browse through different pages to generate sufficient traffic.

2. **Analyze Network Logs:**
   - Navigate to the VPC Flow Logs section in the cloud console.
   - Look for entries related to the web server’s IP and port 80.
   - Verify that HTTP traffic is being logged correctly and reaching the server.

**Troubleshooting:**

- If you don’t see logs, ensure VPC Flow Logs are enabled and correctly configured for `vpc-net`.
- Confirm that the firewall rule was applied correctly by checking the rule list.

### 3. Create and Test a Firewall Rule to Deny HTTP Traffic

**Steps:**

1. **Navigate to Firewall Rules:**
   - Open the **Firewall Rules** section in your cloud provider's console.

2. **Create a New Rule:**
   - **Name**: `deny-http-traffic`
   - **Network**: `vpc-net`
   - **Priority**: 2000 (ensure this rule has a lower priority than the allow rule)
   - **Direction**: Ingress
   - **Action**: Deny
   - **Source IP Ranges**: `0.0.0.0/0`
   - **Protocols and Ports**: `tcp:80`
   - **Target Tags**: `http-server`

3. **Save and Apply the Rule.**

4. **Test the Rule:**
   - Attempt to access the web server again using a browser or `curl`.
   - Confirm that HTTP traffic is blocked and you receive a connection error.

**Troubleshooting:**

- If HTTP traffic is not blocked, ensure the deny rule has a higher priority (lower number) than the allow rule.
- Check for any conflicting rules that might affect traffic.

### 4. Analyze Firewall Logs to Verify the Rule

**Steps:**

1. **Access Firewall Logs:**
   - Go to the **Firewall Logs** section in your cloud console.

2. **Review the Logs:**
   - Look for entries indicating that HTTP traffic is being denied.
   - Verify that the `deny-http-traffic` rule is actively blocking traffic as expected.

**Troubleshooting:**

- If the deny rule is not working, double-check the rule configuration and priority settings.
- Ensure that logs are properly configured and associated with the correct network.

## Best Practices

- **Regularly Review Firewall Rules:** Periodically review and update firewall rules to adapt to changing security requirements and operational needs.
- **Least Privilege Principle:** Always apply the principle of least privilege by allowing only the necessary traffic and blocking everything else.
- **Automate Monitoring:** Use automated tools to monitor and alert on unusual traffic patterns or changes in firewall rule effectiveness.
- **Document Changes:** Keep detailed records of all changes made to firewall rules for auditing and troubleshooting purposes.

## Conclusion

By following these steps, you will effectively configure, test, and manage firewall rules to secure Cymbal Bank's demo web server. Ensure to review and adjust firewall configurations regularly to maintain a robust security posture.


