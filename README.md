# ansible_ec2_monitor
Ansible Role to install CloudWatchMonitoringScripts and Monitor Memory and Disk Metrics for Amazon EC2 Linux Instances

Role Variables
--------------

Following variables need to be defined:

- cloud_watch_monitoring_path - Path where scripts will be downloaded and unarchieved
- cron_specs - {name: "Name of the task", minute: "*/5", hour: "*", job: "{{cloud_watch_monitoring_path}}/aws-scripts-mon/mon-put-instance-data.pl --disk-space-util --disk-path=/mnt/data --from-cron --aws-access-key-id=AWS_KEY --aws-secret-key=AWS_SECRET_KEY"}

Note: There are no default values for the above mentioned variables.

Dependencies
------------

This package has no dependencies on modules not included with Ansible by default.

Install
-------

    $ ansible-galaxy install amritsingh.ec2_monitor

Usage
-----

Example Usage in `site.yml`

    $ cat site.yml
    ---
    - hosts: all
      remote_user: centos
      become: yes
      become_method: sudo
      roles:
          - role: "amritsingh.ec2_monitor"

            cloud_watch_monitoring_path: "/opt"
            cron_specs:
                - name: "Send Memory And Disk Usage Statistics"
                  minute: "*/5"
                  hour: "*"
                  job: >
                      {{cloud_watch_monitoring_path}}/aws-scripts-mon/mon-put-instance-data.pl
                      --disk-space-util
                      --disk-path=/
                      --disk-path=/data
                      --disk-space-used
                      --disk-space-avail
                      --mem-util
                      --mem-used
                      --mem-avail
                      --from-cron
                      --aws-access-key-id=your_aws_access_key_id
                      --aws-secret-key=your_aws_secret_key

License
-------

Apache

Author Information
------------------

Created by Amrit Singh
https://www.twitter.com/_amrit_
