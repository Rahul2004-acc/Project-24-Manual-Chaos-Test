# Project 24: Manual Chaos Test – Service Failure and Recovery

## 🎯 Project Objective

To simulate an application service failure, observe its impact, manually recover the service, and verify that the application becomes operational again. This project demonstrates controlled failure simulation and chaos engineering principles in a production-like AWS environment.

---

## 🛠️ Technologies and AWS Services Used

| Component | Purpose |
|-----------|---------|
| **AWS EC2** | Hosted the test web server |
| **AWS Systems Manager (SSM)** | Executed remote commands without SSH access |
| **Amazon Linux 2023** | Operating system for the EC2 instance |
| **Apache HTTP Server (httpd)** | Application service under test |
| **AWS IAM** | Provided EC2 instance permissions for SSM operations |

---

## 📋 Implementation Steps

1. **EC2 Instance Setup**
   - Created a dedicated EC2 instance for testing
   - Configured AWS Systems Manager (SSM) Agent for remote access
   - Set up appropriate IAM role for SSM operations

2. **Apache HTTP Server Configuration**
   - Installed Apache HTTP Server (httpd)
   - Configured service to start automatically on system boot
   - Verified initial installation and functionality

3. **Initial Health Check**
   - Verified Apache service status using `systemctl`
   - Confirmed HTTP server responding with successful requests using `curl`
   - Documented baseline metrics

4. **Service Failure Simulation**
   - Executed `sudo systemctl stop httpd` to simulate failure
   - Confirmed service became inactive and unresponsive
   - Observed HTTP connection failures

5. **Service Recovery**
   - Executed `sudo systemctl start httpd` to restore service
   - Verified service status returned to active state
   - Confirmed HTTP requests successful with `200 OK` responses

6. **Incident Documentation**
   - Recorded failure timestamp: **05:34:32 UTC**
   - Recorded recovery timestamp: **05:36:05 UTC**
   - Documented all findings in incident report

---

## ✅ Test Results

| Test Case | Expected Result | Actual Result | Status |
|-----------|-----------------|----------------|--------|
| Initial Apache service check | Service: Active | Active (running) | ✅ Passed |
| Stop Apache service | Service: Inactive | Inactive (stopped) | ✅ Passed |
| HTTP request during failure | Connection refused | Connection refused | ✅ Passed |
| Restart Apache service | Service: Active | Active (running) | ✅ Passed |
| HTTP response after recovery | HTTP 200 OK | 200 OK | ✅ Passed |

### Recovery Timeline

```
Failure Recorded:   05:34:32 UTC
Recovery Verified:  05:36:05 UTC
Recovery Time:      1 minute 33 seconds
```

### Final HTTP Response Status
```
Status Code: 200 OK
Apache Service: Active (running)
Server Availability: Fully Operational
```

---

## 📁 Deliverables

1. **incident-notes.md** - Detailed incident report documenting the failure and recovery process
2. **Apache Web Server Screenshots**
   - Initial Healthy State
   - Chaos Test - Apache Service Failure
   - Chaos Test - Apache Recovery Verified
3. **This README** - Project documentation and implementation guide

---

## 🎓 Key Learnings

- **Chaos Engineering Principles**: Understanding controlled failure simulation for resilience testing
- **AWS Systems Manager**: Executing remote commands and managing EC2 instances without SSH
- **Linux Service Management**: Using `systemctl` to monitor, control, and manage system services
- **Service Health Monitoring**: Verifying application availability through HTTP requests and service status checks
- **Incident Response**: Documenting failures, response times, and recovery procedures
- **Recovery Verification**: Ensuring successful service restoration and validating operational state

---

## ⚙️ Commands Reference

### Check Service Status
```bash
sudo systemctl status httpd
```

### Start Apache Service
```bash
sudo systemctl start httpd
```

### Stop Apache Service
```bash
sudo systemctl stop httpd
```

### Restart Apache Service
```bash
sudo systemctl restart httpd
```

### Test HTTP Connectivity
```bash
curl http://localhost
# or
curl http://<EC2-Public-IP>
```

### View Apache Logs
```bash
sudo tail -f /var/log/httpd/access_log
sudo tail -f /var/log/httpd/error_log
```

---

## 🚨 Important Cleanup Instructions

**⚠️ Remember to terminate the temporary EC2 instance after saving your deliverables to avoid additional AWS charges.**

Steps to terminate:
1. Navigate to AWS EC2 Console
2. Select the test instance
3. Click "Instance State" → "Terminate Instance"
4. Confirm termination

---

## 📊 Project Metrics

| Metric | Value |
|--------|-------|
| Total Test Duration | ~2 minutes |
| Failure-to-Recovery Time | 1 minute 33 seconds |
| Service Uptime (Post-Recovery) | 100% |
| HTTP Success Rate (Post-Recovery) | 100% |

---

## 🔗 Related AWS Documentation

- [AWS Systems Manager Documentation](https://docs.aws.amazon.com/systems-manager/)
- [Apache HTTP Server Documentation](https://httpd.apache.org/docs/)
- [AWS EC2 User Guide](https://docs.aws.amazon.com/ec2/)
- [Systemd Documentation](https://systemd.io/)

---

## 📝 Notes

This project serves as a foundation for more advanced chaos engineering practices, such as:
- Automated failure injection
- Load testing during failures
- Multi-service failure scenarios
- Recovery time objective (RTO) measurement
- Recovery point objective (RPO) analysis

---

## ✨ Conclusion

**Project Status:** ✅ **Successfully Completed**

The chaos engineering test successfully demonstrated:
- Controlled service failure simulation
- Impact observation on application availability
- Successful manual recovery procedures
- Verification of operational restoration

All test cases passed, and the service was fully recovered to operational status. This exercise validates the ability to manage infrastructure resilience and perform effective incident recovery in AWS environments.

---

**Project Date:** November 23, 2026  
**Environment:** AWS (Amazon Linux 2023 EC2)  
**Test Status:** Passed ✅
