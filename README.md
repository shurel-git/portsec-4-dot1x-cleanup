# portsec-4-dot1x-cleanup
Cleanup conflicting switchport security features on access switches

# This ansible playbook requires very little input, as its main purpose is to fully automate access layer switches having conflicting features enabled. In essence, we're removing #port-security command lines from switchports having both port-security & dot1x enabled This script was written for Cisco Catalyst 3xxx platform IOS-XE system.

The script will launch 2 separated "show" commands for both port-security & dot1x features to the targeted switch.
Command output will be saved into separated command & switch files for further parsing comparison
the dot1x interfaces output will be rewritten in order to be further compared at a later stage (Both command do show different interface names)
Lack of Jinja2 templating capabilities from ios_command module have been overcome with additional tasks
An interface backup takes place and save the output into a file (Port-security enabled ports only)
both show : port-security & dot1x are compared in order to produce a list of interfaces running the same feature
matching interfaces are then cleaned-up & config saved at the end of the script
executer required input :

Place the list of switches to be parsed into the host file

# Run the script with : 

ansible-playbook -i hosts main.yaml
