Scenario 3: Finding Service Logs

A developer asks: "Where are the logs for the 'docker' service?"
The service is managed by systemd.
What commands would you use?

Answer: Since Docker is managed by systemd, I would use journalctl -u docker to view logs, -n to limit output, and -f to follow logs in real time.

# Check service status
systemctl status docker

# Last 50 logs
journalctl -u docker -n 50

# Live logs
journalctl -u docker -f

# Logs from last 1 hour
journalctl -u docker --since "1 hour ago"

# Only errors
journalctl -u docker -p err
