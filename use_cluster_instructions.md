# Using cluster through Jupyter notebook:

1. Create a `small` instance, with the base image `Ubuntu 22.04 -2023.01.07`. Feel free to use the `Group 12` key Joel uploaded earlier.
2. SSH config file, remember to edit the public IP and path to the private SSH key.
    ```
    Host devm
        HostName 130.238.x.y
        User ubuntu
        Port 22
        IdentityFile /somepath
        LocalForward 8888 localhost:8888
        LocalForward 4040 localhost:4040
        LocalForward 4041 localhost:4041
        LocalForward 4042 localhost:4042
        LocalForward 4043 localhost:4043
        LocalForward 4044 localhost:4044
        LocalForward 9870 192.168.2.231:9870
        LocalForward 8080 192.168.2.231:8080
    ```

    On the VM:
    1. `sudo apt-get update`
    2. `sudo apt-get install python3-pip net-tools openjdk-11-jdk-headless git -y`
    3. Edit `/etc/hosts` to include the following, where you should edit the first line:
        ```
        192.168.x.y hostname
            
        192.168.2.231 sp-master
        192.168.2.169 sp-worker1
        192.168.2.159 sp-worker2
        192.168.2.158 sp-worker3
        192.168.2.214 sp-worker4
        ```

4. Copy the `192.168.x.y hostname` to all other VMs in the cluster (master & workers)
5. `python3 -m pip install pyspark=3.3.2 --user notebook` (important to have the correct pyspark version here)
6. Run the notebook `jupyter notebook --ip=* --no-browser`
