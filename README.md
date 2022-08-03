# TurtleBot3DebugTips

## Control Turtlebot3 from remote PC

To control the turtlebot3 from a remote PC, you need to set up the environment variables `ROS_MASTER_URI` and `ROS_HOSTNAME` on both turtlebot and your remote PC. The first step is to get both your turtlebot3 and PC in the same WiFi network. The check the IP addresses for both your turtlebot3 and PC using

```console
ifconfig
```

The on both machines add this to either `~/.bashrc` or `~/.zshrc`

```bash
export ROS_MASTER_URI=http://{PC_IP_ADDRESS}:11311
```

and set the `ROS_HOSTNAME` to the ip address of their own machine, i.e.

```bash
export ROS_HOSTNAME={PC_IP_ADDRESS}
```

on the PC, and

```bash
export ROS_HOSTNAME={TURTLEBOT3_IP_ADDRESS}
```

on your turtlebot. To check the connection, first, `ping` each other. If that works, then try running 

```console
netcat -l 1234
```

on your PC, and 

```console
netcat {PC_IP_ADDRESS} 1234
```

on the turtlebot and check if you can receive the messages typed on the turtlebot on your PC. If this works, try it reversely. If one of these do not work, the issue might lie with the firewall on your PC. To disable your firewall on a Ubuntu machine run

```console
sudo ufw disable
```

After this try and see if `netcat` enables communication. It worked for me after this.
