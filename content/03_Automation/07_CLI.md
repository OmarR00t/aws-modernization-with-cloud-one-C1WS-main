---
title: "CLI "
chapter: false
weight: 120
---

### Command line interface

The command line interface (CLI) command for workload security will be divided into two commands:  
1-```DSA_control```  
2-```DSA_Query```

### dsa_control
you can use dsa_control to configure some agent settings manually like activation,anti malware scanning.

To use this command follow these steps:
```
 In windows operating system:
 -Open CMD as administrator.
 -Change the agent installer directory. For example cd C:\Program Files\Trend Micro\Deep Security Agent\
 -Run dsa_control like this dsa_control <option>
```
 where the option will be replaced with one of these option described in [DSA_control options ](https://cloudone.trendmicro.com/docs/workload-security/command-line-interface/#How).
 ```
 In Linux operating system:
 -Open terminal.
 -Write this sudo /opt/ds_agent/dsa_control <option>
  ```
where option is replaced with one of the options described in in [DSA_control options ](https://cloudone.trendmicro.com/docs/workload-security/command-line-interface/#How).





