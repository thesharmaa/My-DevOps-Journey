Scenario 1: Service Not Starting

A web application service called 'myapp' failed to start after a server reboot.
What commands would you run to diagnose the issue?
Write at least 4 commands in order.

Answer:I would first check systemctl status, then inspect journal logs, verify boot configuration, and review boot-specific logs to identify why the service failed after reboot.

-----Diagnosis-----
Step 1: sudo systemctl status myapp
Why: To check whether service is active, inactive, or failed after reboot

Step 2: journalctl -u myapp -n 10
Why: To identify exact error causing failure after reboot

Step 3: sudo systemctl is-enabled myapp
Why: To verify whether service is configured to start on system boot

Step 4: journalctl -b -u myapp
Why: To analyze logs from current boot session only

-----Fixing-----
Step 5: sudo systemctl start myapp
Why: Based on investigating logs that myapp was stopped abruptly, I will start the myapp

Step 6: sudo systemctl enable myapp
Why: To run myapp automatically when server boots up automatically for future boot

-----Verification-----
Step 7: sudo systemctl status myapp
Why: To verify if myapp is running
