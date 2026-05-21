# 🚀 Linux Interview Questions + Answers (Structured)

---

## 🟦 1. Basic Linux Commands & Concepts (1–10)

1. What is the difference between ps, top, and htop?  
ps → snapshot of processes  
top → real-time process monitoring  
htop → interactive UI with better visualization  

2. How do you display the IP address?  
`ip a` or `ifconfig`  

3. Explain ls command with options  
`ls -l` → detailed view  
`ls -a` → hidden files  
`ls -lh` → human readable  

4. df vs du  
df → disk usage of filesystem  
du → disk usage of directory/files  

5. Check disk usage of directory  
`du -sh /dir`  

6. What is grep?  
Search text in files  

7. Search string in multiple files  
`grep -r "error" /path`  

8. chmod vs chown vs chgrp  
chmod → permissions  
chown → owner  
chgrp → group  

9. /etc/passwd role  
Stores user account info  

10. /etc/fstab role  
Defines filesystems mounted at boot  

---

## 🟦 2. Process Management (11–15)

11. What is a zombie process?  
Finished process still in process table  

12. List all processes  
`ps -ef`  

13. kill vs killall  
kill → PID  
killall → process name  

14. fg vs bg vs jobs  
fg → foreground  
bg → background  
jobs → list jobs  

15. Stop or suspend process  
`kill`, `kill -9`, `Ctrl+Z`, `bg`  

---

## 🟦 3. System Resources & Performance (16–20)

16. Monitor system resources  
`top`, `htop`, `vmstat`, `iostat`  

17. Check memory usage  
`free -m`  

18. Analyze performance  
vmstat → CPU/memory  
iostat → disk  
top → processes  

19. Check swap usage  
`free -m` or `swapon -s`  

20. Diagnose high CPU  
`top`, `ps aux --sort=-%cpu`  

---

## 🟦 4. Logs & Troubleshooting (21–30)

21. Purpose of /var/log  
Stores system logs  

22. Check logs  
`journalctl`, `cat`, `less`  

23. View kernel logs  
`dmesg`  

24. Filter logs  
`grep "error" /var/log/syslog`  

25. What is core dump?  
Memory snapshot of crashed app  

26. dmesg usage  
Check hardware/kernel logs  

27. Troubleshoot failed service  
Check logs + `systemctl status`  

28. Log rotation  
`logrotate`  

29. Analyze crash dump  
`gdb`, `kdump`  

30. Interpret crash dump  
Analyze stack trace  

---

## 🟦 5. Kernel & System (31–40)

31. What is Linux kernel?  
Core of OS managing hardware  

32. Check kernel version  
`uname -r`  

33. Upgrade kernel  
`yum update kernel`  

34. Boot process  
BIOS → Bootloader → Kernel → Init  

35. initrd  
Temporary root filesystem  

36. sysctl  
Manage kernel parameters  

37. Boot failure troubleshooting  
Check logs, rescue mode  

38. Kernel panic  
System crash due to kernel error  

39. Kernel modules  
`lsmod`, `modprobe`  

40. udev  
Device manager  

---

## 🟦 6. Networking (41–50)

41. Troubleshoot network  
ping, traceroute, curl  

42. Network tools  
`ping`, `ss`, `netstat`  

43. Check internet connectivity  
`ping google.com`  

44. Configure network  
`ip`, `nmcli`  

45. DNS issues  
Check `/etc/resolv.conf`  

46. iptables  
Firewall rules  

47. iptables vs firewalld  
firewalld = modern  

48. Active connections  
`ss -tulnp`  

49. NAT & port forwarding  
Translate private/public IP  

50. netstat usage  
Check connections  

---

## 🟦 7. Filesystem & Disk (51–60)

51. ext4 vs xfs  
ext4 → stable  
xfs → better performance  

52. Extend LVM  
`lvextend`, `resize2fs`  

53. Check disk errors  
`fsck`  

54. Swap partition  
Virtual memory  

55. Inode usage  
`df -i`  

56. Recover filesystem  
`fsck`  

57. Unmount disk  
`umount`  

58. Filesystem integrity  
`fsck`  

59. Hard link vs soft link  
Hard → same inode  
Soft → pointer  

60. Full disk troubleshooting  
`df`, `du`  

---

## 🟦 8. Security (61–70)

61. Secure Linux server  
SSH hardening, firewall  

62. SELinux  
Security layer  

63. sudoers file  
User privilege config  

64. SSH configuration  
`/etc/ssh/sshd_config`  

65. SSH keys  
Password-less login  

66. Secure file permissions  
chmod, chown  

67. AppArmor vs SELinux  
Different security models  

68. Security audit  
Logs, auditd  

69. System hardening  
Disable unused services  

70. auditd  
Audit logs  

---

## 🟦 9. Cloud & Containers (71–80)

71. Manage cloud server  
SSH + configs  

72. Setup VM  
Install OS  

73. Docker basics  
Container runtime  

74. Troubleshoot container  
logs, inspect  

75. Kubernetes + Linux  
Runs on Linux kernel  

76. AWS CLI setup  
`aws configure`  

77. Monitor cloud instance  
CloudWatch  

78. Terraform usage  
Infra provisioning  

79. Ansible usage  
Automation  

80. Cloud-native apps  
Microservices  

---

## 🟦 10. Backup & Recovery (81–85)

81. Backup tools  
tar, rsync  

82. Restore backup  
untar / rsync  

83. RAID  
Redundant storage  

84. Disaster recovery  
Backup + restore  

85. Backup best practices  
Automation + testing  

---

## 🟦 11. Troubleshooting (86–92)

86. Slow website  
Check CPU, DB, logs  

87. Performance bottleneck  
CPU, memory, disk  

88. Service not starting  
logs + systemctl  

89. Core dump analysis  
gdb  

90. Debug app crash  
strace, logs  

91. Debug kernel issues  
dmesg  

92. General troubleshooting  
logs → metrics → fix  

---

## 🟦 12. Automation & Scripting (93–100)

93. Automate tasks  
cron, scripts  

94. Script for disk usage  
df + alert  

95. Cron jobs  
Schedule tasks  

96. Schedule cron  
`crontab -e`  

97. Health check script  
Check service + restart  

98. Ansible advantage  
Automation  

99. Log analysis script  
grep + awk  

100. Efficient scripting  
loops + conditions  

---

# 🎯 One-Line Summary

Linux = Commands + Processes + Networking + Storage + Security + Troubleshooting + Automation
