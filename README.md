# geacon_plus
The CobaltStrike stageless http(s) beacon implemented by golang has more extensions based on the geacon project

Thanks to the good brother [@H4de5](https://github.com/H4de5-7) for the windows part of the code support  
Secondary development ideas [CobaltStrike beacon second guide] (https://blog.z3ratu1.cn/CobaltStrike%20beacon%E4%BA%8C%E5%BC%80%E6%8C%87%E5%8D%97. html)

## Disclaimer
Please use this project after fully reading and agreeing to the following content  

**This project is only used for learning the CobaltStrike protocol and testing the implementation of related technical methods.
Do not use for any illegal purposes, and it is strictly forbidden to use this project to attack computer information systems. The resulting consequences are borne by the user**  

The sister project [geacon_pro](https://github.com/H4de5-7/geacon_pro) has been converted to private and is no longer open to the public due to its high aggressiveness and risk of abuse  
This project does not update the anti-kill related functions added later in the pro version, it is only used as a design for learning CS beacon


## Realize the function
Supports cross-platform use, and can execute simple commands on linux and macOS (there is no macOS, so it can be executed theoretically)  
It has passed the tests of local windows7/10, winserver 2012 and ubuntu22.04  

It seems that everyone prefers the higher version. . . Therefore, version 4.1+ is compatible, and you can use Support41Plus in config/config.go to specify whether to use version 4.0 or version 4.1+

## Instructions
This project is improved based on [darkr4y/geacon](https://github.com/darkr4y/geacon), the specific usage method can refer to the original project  
c2profile supports partial encoding and filling. The c2profile in the project comes from the classic jquery.profile, which is given here  
You can add -ldflags "-H windowsgui -s -w" when compiling to reduce the program size and cancel the black box. You can also use the [go-strip](https://github.com/boy-hack/go-strip) project Delete data such as symbol table


###c2profile
Implemented partial support for c2profile
Supports encoding and prepend append of server and client data, encoding algorithm supports base64, base64url, netbios, netbiosu, mask

### File management
Realized mv, cp, mkdir, rm, upload, download, fileBrowse  
Return data in a standard format and support CS graphical interface interaction

### Process management
Implemented listProcess and kill, also supports graphical interaction

### Command Execution
Implement shell, run and execute, use local shell to execute commands, and use CreateProcess to create processes under windows

### Process Injection
Only supports windows platform
Support reflective dll injection, realize simple process injection and puppet process injection, support screenshot, portscan, netview and other CobaltStrike RDI tasks
Since injection into remote threads has a certain chance of being caught, add a patch dll exitProcess to exitThread and change spawn+inject to inject itself, which can be selected in config

### token related
Tried to implement functions such as runas, make token, and steal token
The steal token can be used, but runas reports a confusing error. I don’t know what the situation is.
The make token is very strange, the password is wrong when inputting anything with LOGON32_LOGON_BATCH, and the returned token cannot be used for inputting anything with LOGON32_LOGON_NEW_CREDENTIALS

### Post penetration function
Support memory loading PowerShell module, support using reflection DLL injection or go language memory execution C#

## Complete
Because the error line number is always reported when debugging the server, the vast majority of the code is realized through static analysis and search data, which cannot guarantee the complete restoration of the CS protocol  
At the same time, the author's windows level is low, so he doesn't know anything about token stealing and hash transmission, and he doesn't seriously analyze operations such as intranet cascading (it can't be done). Welcome all gods to communicate and discuss and submit PR


# ORIGINAL Geacon Configuration:

**Using Go to implement CobaltStrike's Beacon**

----

*This project is for learning protocol analysis and reverse engineering only, if someone's rights have been violated, please contact me to remove the project, and the last DO NOT USE IT ILLEGALLY*



## How to play

1. Setup the teamserver and start a http lisenter, the teamserver will generate the file `.cobaltstrike.beacon_keys`.
2. Compile the BeaconTool with Jetbrains Idea, use command `java -jar BeaconTool.jar ` to convert java keystore to PEM format.
3. Replace the RSA key pair in the file `cmd/config/config.go` (the RSA private key is not required, I wrote it in the code just for the record)
4. Compile the geacon whatever platform you want to run: for example, use the command `export GOOS="darwin" && export GOARCH="amd64" && go build cmd/main.go` to compile an executable binary running on MacOS.
5. Or fow win: export GOOS="windows" && export GOARCH="amd64" && go build main.go
6. Having fun ! PR and issue is welcome ;)
7. Geacon has just been tested on CobaltStrike 3.14 and only support default c2profile, so many hardcode in the project and I will not try to implement more C2profile support at this moment.
8. Thanks for **[@xxxxxyyyy](https://github.com/xxxxxyyyy)**'s PR, And now Geacon supports **CobaltStrike 4.0**, please checkout the branch `4.0` to compile.
9. Geacon's branch `master` supports **CobaltStrike 4.1**, currently available functions include: executing commands, uploading, downloading, file browser, switching the current working directory, and exiting the current process.
10. Geacon only focuses on protocol analysis, but if you want to experience more features, you can use another project of our partners, check out **[CrossC2](https://github.com/gloxec/CrossC2)** now!
