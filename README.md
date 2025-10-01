# roadmap.sh-devops-projects

## Server Stat Porject
the URL of the project: https://roadmap.sh/projects/server-stats
my script:

```shell
#!/bin/bash

# The total CPU usage is the average of the total in five seconds

totalCPU=$(top -b -n5 | grep "Cpu" | grep Average | awk '{print $2}')
echo -e "Total CPU usage is $totalCPU %\n"

# Free memory vs used

freememory=$(free | grep Mem: | awk '{print ($4 / $2) * 100.0}')
usedmemory=$(free | grep Mem: | awk '{print ($2 - $4) / $2 * 100.0}')
echo -e "Free memory is $freememory %\nUsed memory is $usedmemory %\n"

#Used Disk % vs Free disk %

useddisk=$(df -h | grep /dev/sda2 | awk '{print $3}' | sed 's/G//')
freedisk=$(df -h | grep /dev/sda2 | awk '{print $4}' | sed 's/G//')
echo -e "Used disk is $useddisk GB %\nTotal free disk is $freedisk GB %\n"

# Top 5 processes by CPU usage

top5process_cpu=$(ps aux | sort -nk +3 | tail -n5 | awk '{print $1" "$2" "$3}')
echo -e "Top 5 Process by memory usage :\n$top5process_cpu"

# Top 5 processes by memory usage

top5process_memory=$(ps aux | sort -nk +4 | tail -n5 | awk '{print $1" "$2" "$4}')
echo -e "Top 5 Process by memory usage :\n$top5process_memory"
```
