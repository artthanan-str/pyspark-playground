# PySpark Standalone Installation Guideline
----
## Prerequisites
- Launch EC2 or any virtual machine with Linux-based environment
- If you use EC2. You need to keep your .pem file in your local workstation 

## Install PySpark and its dependencies
> You need to go to termminal in order to execute the below commands
1. Run `sudo apt update`
2. Install Pip3 `sudo apt install python3-pip`
3. Install python library - jupyter `pip3 install jupyter`
4. Add Python Path `export PATH=$PATH:~/.local/bin`
5. Install Java `sudo apt install default-jre` and use `java --version` to validate the installation
6. Install Scala `sudo apt install scala` and use `scala -version` to validate the installation
7. Install python library - py4j `pip3 install py4j`
8. Download spark `wget https://downloads.apache.org/spark/spark-3.0.1/spark-3.0.1-bin-hadoop2.7.tgz`
9. Extract the file `tar xvf ./spark-3.0.1-bin-hadoop2.7.tgz`
10. Set the evironment variables 
    ```
        export SPARK_HOME='home/ubuntu/spark-3.0.1-bin-hadoop2.7'
        export PATH=$SPARK_HOME:$PATH
        export PYTHONPATH=$SPARK_HOME/python:$PYTHONPATH
        export PYSPARK_DRIVER_PYTHON="jupyter
        export PYSPARK_DRIVER_PYTHON_OPTS="notebook"
        export PYSPARK_PYTHON=python3
    ```
11. Run this command `sudo chmod 777 spark-3.0.1-bin-hadoop2.7`
12. Run this command `cd spark-3.0.1-bin-hadoop2.7 && sudo chmod 777 python`
13. Run this command `cd spark-3.0.1-bin-hadoop2.7/python/ && sudo chmod 777 pyspark`

---

### If you found this error liked this `<module> ModuleNotFoundError: No module named 'pyspark'`, follow this instruction
- Run this command `pip3 install findspark`
- import `findspark` command before you import pyspark
    ```
        import findspark
        findspark.init('/home/ubuntu/spark-3.0.1-bin-hadoop2.7')

        import pyspark
    ```

### Additional: You can use our local browser to connect to Jupyter Notebook in EC2    
1. [Local] Connect the Jupyter Notebook in EC2 --> use `nano .ssh/config` and add this configuration
    ```
        Host spark_ec2
        Hostname your-ec2’s-public-ip-address here
        User ubuntu
        IdentityFile ./aws_key_pair.pem
    ```
22. [EC2] Use `screen` command to start `jupyter notebook` or `jupyter lab` in background, then copy the token
23. [Local] ssh -NfL 8088:localhost:8888 spark_ec2
24. Go to your browser and type `localhost:8088` and use token to login to Jupyter Notebook
25. Test your Jupyter Notebook by importing the pyspark