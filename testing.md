# Testing

A comprehensive guide to running and understanding tests on the bike/buck, and interacting with ROS and the Raspberry Pi / Tx1.

##  Running a test on the bike
### Set up hardware
All the sensors on the bike are connected to the Arduino. The Arduino communicates this data from its programming port to the USB port on the Raspberry Pi labeled "Arduino". The Raspberry Pi should be powered through its microUSB port. 

To turn on the bike, plug in the battery in the bike's hardware box. You can check the battery's voltage using a multimeter (set to 60 V). The battery is 29 V fully charged. It at function at lower voltages but you may notice the bike unexpectedly shutting down while testing. Make sure the Arduino and Raspberry Pi are both powered on. 

You may need to front motor on while testing. There are two switched on the right side of the hardware box. The right one turns on the front motor, and the left one turns on the rear motor. Make sure the motors are turned off while uploading code.

### Connect to the Pi
There are two ways to do this. When testing in the lab use Locomotion Wifi. When testing outside, use Ad-hoc wifi to connect to the Raspberry Pi without internet.

#### LocomotionLab (in lab)
1. Connect to LocomotionLab on your computer.
2. Open a terminal/command line and ssh into the pi 
```bash
    ssh pi@10.0.1.50
```
3. Enter the password for the Pi which is "raspberry"

#### Ad-hoc (outside)
1. Steps 1-3 from LocomotionLab
2. While ssh'ed into the Pi, run the following command
```bash
        sudo cp /etc/network/interfaces-adhoc /etc/network/interfaces
```
This changes the network configurations on the Pi by copying the adhoc configurations (interfaces-adhoc) to the file that is actually run (/etc/network/interfaces). 
3. Disconnect the Pi to turn it off and wait a minute. Reconnect the Pi and connect to RPIWireless on your computer. It may appear in "Devices" instead of Wifi in the network list.
4. ssh into the pi using the Adhoc IP address (same password)
```bash
    ssh pi@192.168.1.1
```
5. Now your computer is directly connected to the Pi with no dependence on Wifi or internet. Your computer will not to be connected to the internet/eduroam.
6. Make sure to reset the network configurations after you are done so the next person can test in lab.
```bash
    sudo cp /etc/network/interfaces-wifi /etc/network/interfaces
```

### Running a test
1. Tests are started and ended by running launch files (start.sh, end.sh). To start a test, run start.sh.
```bash
    . start.sh &    
```
The test starts with a launch file. If you do not specify a different launch file, it will use run.launch by default.

"&" runs the file in the background. This allows you to have access to the terminal during a test. If you forget to include "&", you can interrupt the command with ctrl-z, and then the "bg" command. 

If you want to terminate a test completely and not save data, make sure the test is running in the background and run "job". This lists the current processes. Get the process id (PID) of the test and then run "kill %pid". 
```bash
    kill %1   
```

2. (Optional) View data in real time.
You can view rostopics and see the data that the Pi is receiving. 
```bash
    rostopic list
```
This will show all the topics that are available and started by start.sh. You can echo the topics to see the data. 
```bash
    rostopic echo bike_state
```
bike_state can be replaced by GPS or any other available rostopic. This can be a valuable check to see if you are receiving the right data.

3. Once you are done, you will need to run end.sh to terminate the nodes and save the data to CSVs. This can be run in the foreground.
```bash
    . end.sh
```

4. View the CSVs.
```bash
    roscd bike/bagfiles/
```
You can list all the files (ls) in the bagfiles directory and see the names for the current test's files. Once you are done with all tests, run the following tests to store the data files in the "old" folder to keep the bagfiles directory clean.
```bash
    mv * old
```
You can check if a particular file contains data and is not empty by reading off the first three lines in the terminal.
```bash
    head -n 3 filename.csv 
```

5. Retrieve the file from the Pi
Open another terminal and cd into the directory on your computer. Note the filenames on the Pi.
```bash
    scp pi@10.0.1.50:/home/pi/ros_ws/src/bike/bagfiles/filename .
```
Enter the Raspberry Pi password and the file will download. Make sure to include the ".".

## Raspberry Pi File Structure

## Launch Files
During a test, you can specify one of many launch files.
```bash
    . start.sh file.launch &    
```
1. all_but_serial.launch
2. nav.launch
3. nav_gps.launch
4. nothing.launch
5. playData.launch
6. recordData.launch
7. run.launch
This is the default launch file which starts the serial, map, and nav nodes.
8. run_nav.launch
9. run_with_kalman.launch
10. serial_only.launch
Runs only serial communication with the Arduino. It does not run navigation or kalman nodes. This is ideal for sensor testing.
11. vis.launch

The launch files have their own git repository. You can look into these files to see which ROS nodes they run.

## ROS Nodes




