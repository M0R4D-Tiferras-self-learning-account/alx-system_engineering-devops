# Incident Report: Web Stack Debugging Project Outage

![wow](https://miro.medium.com/v2/resize:fit:1226/1*BLOPXfltUpIWJjQm1v4M_Q.jpeg)

**Issue Summary**:
- **Duration**: 2024-08-10, 14:30 - 17:00 UTC (2 hours 30 minutes)
- **Impact**: The main web application was completely unavailable to 80% of users. Users experienced 503 Service Unavailable errors when trying to access the platform.
- **Root Cause**: A misconfigured load balancer resulted in all traffic being routed to a single, overwhelmed backend server.

**Timeline**:
- **14:30**: Issue detected through monitoring alerts indicating a sudden spike in 503 errors.
- **14:35**: On-call engineer confirmed the outage and initiated investigation into backend servers.
- **14:45**: Assumed root cause was a high CPU load on the backend servers; attempts were made to restart the servers.
- **15:00**: Misleading path: Restarting servers showed temporary improvement but did not resolve the issue. Continued investigation into database performance.
- **15:30**: Escalated to the network operations team after identifying the load balancer as a potential bottleneck.
- **16:00**: Network team identified a misconfiguration in the load balancer settings that directed all traffic to a single server.
- **16:30**: Reconfigured load balancer to properly distribute traffic across all backend servers.
- **17:00**: Service fully restored, monitoring for stability.

**Root Cause and Resolution**:
- **Root Cause**: The load balancer was incorrectly configured during a recent maintenance update. Instead of balancing traffic evenly, it directed all requests to a single backend server, causing it to overload and fail.
- **Resolution**: The load balancer configuration was corrected to evenly distribute incoming traffic across all available backend servers. A thorough check was conducted to ensure no further misconfigurations were present.

**Corrective and Preventative Measures**:
- **Improvements**: Review and improve the load balancer configuration process to prevent misconfigurations. Implement better monitoring of traffic distribution across servers.
- **Tasks**:
  - Update and automate load balancer configuration scripts to avoid manual errors.
  - Implement a validation step before deploying load balancer changes.
  - Add detailed monitoring on load balancer traffic patterns and server load.
  - Conduct training for the network operations team on the new configuration process.
