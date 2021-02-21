# ansible-splunkuf-update

Using Ansible playbook to automate Splunk UF config update.

To add new log source into Splunk UF:
- Add a new line in `syslog-sources.csv` with [name of the source],[port number],[tcp or udp],[key name used for syslog files].

    Example: `fooudp,46588,udp,foo`
    
- Add a new line in `inputs.csv` with [name of the input][index name][index data type].
    
    Example: `foo,network_foo,cisco:ios`

After updated the CSV files, run `ansible-playbook update-config.yml`.

The playbook `update-config.yml` does the following:
- Import syslog-ng sources from `syslog-sources.csv`
- Use Jinja2 template to generate syslog-ng config file.
- Import Splunk Universal Forwarder inputs from `inputs.csv`
- Use Jinja2 template to generate Splunk UF syslog app inputs config file.
- Restart Splunk service

Remember to update SSH key path in `ansible.cfg`.