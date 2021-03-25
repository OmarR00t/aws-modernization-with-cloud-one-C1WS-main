---
title: "Trend Micro Hybrid Cloud Security Command Line Interface"
chapter: false
weight: 90
---

### Introduction

Trend Micro Hybrid Cloud Security Command Line Interface is a consistent interface that provides suport for automating your tasks using the Deep Security API. This tool is particularly useful to leverage the Deep Security API without the need for a deep dive into Python or APIs. All replies from the server are in JSON. Therefore jq is a good companion program to pipe the output to. For most distributions, you can install jq with yum install jq or apt-get install jq.  

### Steps to install THUS tool
1-Python 3.6.x or greater installed.  
2-For termninal of your choices:To install globally (use this for Windows): ```sudo pip3 install tm-thus```,If you're using a virtual environment, set that up first then enter: ```pip3 install tm-thus``` and To install for your user:```pip3 install --user tm-thus```

if you would like to install for specific operating system Visit [OS specific installation ](https://github.com/trendmicro/thus/blob/master/doc/os_install.md)

### Enable command completion

1-If you installed with ```--user:``` run: :```source ~/.local/bin/thus_completer_bash.sh:```  
2-If you installed thus globally run: :```source /usr/bin/thus_completer_bash.sh:```  
3-To enable this on every login, add the command to your :```  ~/.bashrc:```   file.

### Integration
Before using this tool, you need to provide the credentials and hostname of your service.

there are two types of configuration:

1-Guided configuration:  
You can configure this by using the command  ```thus --config ```  Which will ask a sequence of questions, then write out the configuration files for you.

2-Manual configuration: 
if you do not choose the guided configuration, you will need to create dir and configuration files credentials and config.    

     1-Create a credentials file:~/.thus/credentials
     
     2-Enter the following in the file [default] DSMapikey =
     to create DSMAPI key,to create one in the Deep Security Manager by going to Administration > User Management > API Keys > New. Fill in the necessary fields and copy the API key to your clipboard, then paste it next to DSMapikey.
     this is a sample of input:
     ----------------------
     [default]
     DSMapikey = E5D08256-1998-21F4-D38B-685ABF6B7CDB:523C4B26-7BD5-D537-9495-1AB2373305DA:OKdUZZIM1ZBVXS
     
     3-Save and close the credentials file.
     4-Create a configuration file: ~/.thus/config
     5-Enter the following in the file:
       [default] DSMhost = DSMverifyssl = False
       For DSMhost, enter your host URL with the correct port and /api attached at the end. If your Deep Security Manager has a self-signed cert, user DSMverifySSL=False. If you're using DSaaS or have a valid cert on your Deep Security Manager, use DSMVerifySSL=True For example:
        --------------------------
        [default]
        DSMhost = https://mydsm.example.com:4119/api
        DSMverifyssl = False
     6-Save and close configuration.
   
### Get Started 
if you want to use TrendMicro hybrid cloud security CLI,Enter ```thus deepsecurity``` ,and press the tab key twice.A list of available options should appear. Once you choose an option, you can continue to use tab completion until you've selected the API object you desire.To get started try entering these APIs examples  ```thus deepsecurity computers listcomputers``` for a list of computers.
if you would like to Automate and Integrate using the Deep Security API &SDK,visit
 [Deep security automationn center](https://automation.deepsecurity.trendmicro.com/article/20_0/)
 
