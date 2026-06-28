**Monitoring Script**


#!/bin/bash

threshold=90

cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}' | cut -d. -f1)

if [ "$cpu_usage" -gt "$threshold" ]; then
    echo "High CPU usage detected: $cpu_usage%"
    # Add alert/notification logic here
fi





**-b**

In top, batch mode does not mean "multiple batches". It means -b tells top:

"Don't open the interactive screen. Print your output as plain text."

It does not decide how many times to print.


**-bn1**


<img width="435" height="677" alt="image" src="https://github.com/user-attachments/assets/ccc8cb98-e33b-4631-8062-425d8c2360bc" />


**awk**

awk reads input line by line, splits each line into fields (columns), and lets you print or process those fields.





<img width="792" height="426" alt="image" src="https://github.com/user-attachments/assets/9245fb00-a484-46c1-890e-3ec5087c1a6f" />
