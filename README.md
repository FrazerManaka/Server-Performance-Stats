https://roadmap.sh/projects/server-stats
This project is part of roadmap.sh DevOps projects.
# Server-Performance-Stats
#!/bin/bash

echo "=== Server Performance Statistics ==="
echo

# CPU Usage
echo "CPU Usage:"
top -bn1 | grep "Cpu(s)" | awk '{print $2}' | awk -F. '{print $1"%"}'

# Memory Usage
echo -e "\nMemory Usage:"
free -m | awk 'NR==2{printf "Used: %sMB (%.2f%%)\nFree: %sMB (%.2f%%)\n", $3, $3/$2*100, $4, $4/$2*100}'

# Disk Usage
echo -e "\nDisk Usage:"
df -h / | awk 'NR==2{printf "Used: %s (%s)\nFree: %s (%s)\n", $3, $5, $4, 100-$5"%"}'

# Top CPU Processes
echo -e "\nTop 5 Processes by CPU Usage:"
ps aux | sort -nr -k 3 | head -5 | awk '{printf "%-10s %5s%% %s\n", $1, $3, $11}'

# Top Memory Processes
echo -e "\nTop 5 Processes by Memory Usage:"
ps aux | sort -nr -k 4 | head -5 | awk '{printf "%-10s %5s%% %s\n", $1, $4, $11}'
