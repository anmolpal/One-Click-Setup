Readme For Bash Automation Standalone

Optional : Download sublime text and open this in sublime. In the bottom right corner select Bash and it just becomes easy
           for you to read this file.

Step 1. Type the command " cd /usr/local " and you are in the local directory of your linux. 

Step 2. Paste the Bash Automation Standalone.sh in your local directory. Right click where the file is stored and click on option
        " open in a Windows terminal". I you do not have windows terminal installed go to the Windows store and download it from there.
        Use command "scp /Bash Automation Multinode.sh <username>@IP:/usr/local" (  SCP (secure copy) is a command-line utility 
        that allows you to securely copy files and directories between two locations) to paste the file in /usr/local.
        (e.g. anmol@123.10.17.145:/usr/local) 


Step 3. Now type "sudo bash Bash Automation Multinode.sh". This will create a kockpit-tools directory in which 
        all of the procceses are done.

Step 4. At first, a prompt will ask you to add master and slave IP in your hosts file.
        Enter yes and input the number of master IP you want to add. Lets say I have 2 master cluster so what
        i will do is enter "2" in the prompt. Next enter the master IP you have .

        In the next prompt, Enter the number of slave clusters you have and their IP. 

        NOTE :: Step no. 4 will be repeated in "Installing Hadoop" and "Installing Spark" sections which will
        come up when you reach step no.8 and step no.9
        Do the same process in these two sections.       

Step 5. When you run the Bash Automation Standalone.sh at first it will check for Linux system updates. At every Prompt keep 
        pressing y and this will update all your linux packages to the latest.

Step 6. In the next step it will look for "kockpit-tools" directory in /usr/local and if not available then it will
        automatically create a kockpit-tools directory.

Step 7. After that it will look for Java in your system. If Java is not installed, it will get installed automatically
        and a Prompt will ask you to download Java. Just press y whenever it asks to download.         

Step 8. Same goes for Python as for Java.

Step 9. In the next step, Hadoop will be installed and configured in your system. At first, it will ask for your master
        cluster IP (master IP is the IP of your main cluster where all of the data is stored and that data will be replicated
        to your slave clusters. We create a master and a slave beacuse if our master get crashed or some technical fault happened
        to it our data will be safe in our slave clusters) .If you want to look for where that IP is stored 
        go to /usr/local/kockpit-tools/hadoop-3.2.2/etc/hadoop
        and there a file name master is created and the master cluster IP is stored in it.

        After you stored your master cluster IP in your master another prompt will appear asking for your slave cluster IP.
        So this is a Standalone setup so we do not have slave clusters in it. Input the same IP in slave which you
        have used in master. 

        Now another prompt will ask "Enter the number of servers you want to replicate data". Because we are in the
        Standalone mode enter "1" in that prompt.

Step 10. Now, in this step Spark is installed and configured in your system . The first prompt will ask for
        "SPARK_WORKER_CORES". Enter the desired number of cores you want to allocate to spark master (e.g 6 or 12)

        Another prompt will ask for "SPARK_WORKER_MEMORY". In this you have to allocate memory to your spark master
        (e.g 60g or 80g). It can be according to your requirements.    

Step 11. The "configure SSH section" and  "Adding Paths to .bashrc" will be done in a new 
         terminal. So in the prompt enter no and skip those steps.      

Step 12.After skipping above two steps, airflow will automatically downloaded and configured in your kockpit-tools directory.
        In your first terminal window Airflow will be started automatically and that terminal will be locked.
        Open your browser and in the URL bar type IP(master)@8181 and the airflow webui will open up.
        8181 is the default port to access Airflow ui. (e.g 192.10.15.132:8181)
        The default username is "admin" and the password is also "admin".

Step 13.(In a new terminal) It is recommneded to "Configure SSH" and "Adding Paths to .bashrc" part will be done in a new terminal.
        Simply open a new terminal and go to /usr/local/ in your linux and type this 
        command "bash Bash Automation Standalone.sh".
        
        A prompt will appear asking you to enter yes or no to configure SSH. Just enter yes.
        Now it will ask you for where you want to store that SSH keys. By default the SSH keys are automatically stored in
        your home directory which is "/home/username/.ssh". Just press Enter and skip that part.

        While configuring SSH we need to wait for passphrase to come up. Just press enter 2 times and leave them empty.
        ((Do not enter anything in the passphrase))
        Now the SSH key is generated and added to your home directory.

        Now a prompt will appear asking you this "Enter the number of slave IP's you want to copy from master cluster".
        In this enter the no of slave servers you want to copy your SSH key. In my case it is "3"

        After completing the above step another prompt will ask you this "Enter the slave cluster username and IP you want to add in your master cluster"
        So what you have to do is enter your slave cluster "username@IP" [e.g(anmol@192.11.45.147)]

Step 14.(Same terminal where SSH Configured is done) In the "Adding Paths to .bashrc" section, enter yes and your paths will be get 
        added ~/.bashrc file. After that it will ask you to start airflow. Since it is already running in the previous terminal.
        simply press no and airflow will not start up in that terminal. Also do the same for the "hadoop and spark daemons" section,
        enter no and skip that section. The script will terminate and now you can type commands in it.

        Now, type the command "source ~/.bahsrc" in your terminal and it save all the changes made in your ~/.bashrc

Step 15.Use command "scp /Bash Automation Multinode Slave.sh <username>@IP:/usr/local" and paste 
        Bash Automation Multinode Slave.sh in /usr/local in your slave cluster.

        Perform step no.2 to step no.10 in slave clusters.

Step 16.Again run "bash Bash Automation Standalone.sh" in the same terminal and skip all the steps (do not configure ssh and bashrc again, just enter no and skip those steps)
        Prompt will appear asking you to "start the airflow webserver" enter no in it and come directly 
        to the "hadoop and spark daemons" section. 
        
        
        
        In the prompt enter yes and hadoop and spark deamons will start.

        Now it will ask you to format namenode. Enter y and the namenode will get formated.

Step 17.For Hadoop WebUI, open your browser and type "IP@9870" (e.g. 192.10.15.132:9870)
        For Spark WebUI,  open your browser and type "IP@8080" (e.g. 192.10.15.132:8080)

That's it.