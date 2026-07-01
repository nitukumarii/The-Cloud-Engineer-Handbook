**How do you debug a failed playbook?**



"When a playbook fails, I first read the error message to identify which task failed. Then I increase the verbosity using the -v, -vv, or -vvv option to get more detailed logs. I verify connectivity to the target hosts, check the inventory and variables, validate the YAML syntax, and rerun only the failed task if needed. If required, I use the debug module to print variable values and identify the root cause before fixing the issue."


# Increase verbosity


ansible-playbook site.yml -vvv


# Validate playbook syntax


ansible-playbook site.yml --syntax-check


# Check inventory


ansible-inventory --list

# Test connectivity

**Use the debug mode**

<img width="187" height="110" alt="image" src="https://github.com/user-attachments/assets/ffee6a75-02b5-4a2b-a779-e995447c5725" />

ansible all -m ping

**Interview Flow**

<img width="347" height="202" alt="image" src="https://github.com/user-attachments/assets/fbff9860-c36f-4507-a518-6c50a830b07d" />

