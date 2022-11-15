
# INTRODUCTION

IOS 14 Corellium SSL Pinning Bypass

![front](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/ssl-bog%202.jpg)

-----------------------------------------------

 Recently, some of the projects at nVisium have involved executing iOS penetration tests against a production application. 
During this process, some of the applications only supported iOS 14.1 and higher, which is soon to become an industry standard. 
In these instances, our team members have had to find a different way to bypass SSL. After doing extensive research, we found 
that by using Corellium iOS 14 VM to proxy through Burp suite, you can bypass SSL pinning. 


## HERE IS THE STEP-BY-STEP GUIDE:


Within this example, a  iPhone X VM running iOS 14.1 and is jailbroken: 

![one](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE1.png)

1. INSTALL THEOS:  

 A cross-platform build system for creating iOS and other programs, later will be use to bypass SSL pinning.
 Open Cydia (update or upgrade if needed), 


Within Cydia:

  I. Add  new repo

  II. Click "Sources”

  III. Then click "Edit”

  IV. Then click “Add” 

  V. Input URL:

  http://repo.bingner.com/ 
 
  VI. Click “Add Source” to confirm

![two](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE2.png)



VII. Now, search and install the Theos Dependencies 


![three](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE3.png)



2. SETUP THEOS ENVIRONMENT VARIABLE: 

 I.Open a terminal on the device and execute the following commands:

 ```bash
 echo "export THEOS=~/theos" >> ~/.profile
 ```

![four](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE4.png)

 ```bash
 $git clone --recursive https://github.com/theos/theos.git $THEOS
 ```

![five](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE5.png)

 ```bash
 curl -LO https://github.com/theos/sdks/archive/master.zip & TMP=$(mktemp -d) & unzip master.zip -d $TMP & mv $TMP/sdks-master/*.sdk $THEOS/sdks & rm -r   master.zip $TMP
 ```
![six](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE6.png)


3. INSTALL SWIFT-TOOLCHAIN:

  I. Reopen Cydia

  II. Search and install “swift-toolchain” from the BigBoss Repo (Default in Cydia)

![seven](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE7.png)



4. INSTALL SSLBYPASS TOOL:

  I. Go back to the device’s terminal and install the SSLBypass tool: 


```bash
git clone https://github.com/evilpenguin/SSLBypass
```

![eight](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE8.png)


```bash
cd SSLBypass/packages
```

![nine](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE9.png)

```bash
dpkg -i com.evilpenguin.sslbypass_1.0-5+debug_iphoneos-arm.deb
```
![ten](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE10.png)



  II. Restart SpringBoard so the new tool goes into effect. NOTE: Device’s screen should flashing. 

  III. Then killall SpringBoard


![eleven](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE11.png)



6. Install Burp Suite’s Certificate:

  I. Connect to the Corellium VPN, set Burp Suite to listen on your VPN's IP.

![12](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE12.png)

  II. Then set a manual proxy within the WI-FI settings of the iPhone to proxy through Burp Suite.

![13](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE13.png)



  III. Open Safari, go to http://burp ,Click the "CA Certificate" button and click “Allow”. 

![14](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE14.png)

  IV. Go to iPhone Settings and Select “General”, Select “Profile” 

![15](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE15.png)



  V. Select the PortSwigger CA profile and click "Install" 3 times.

![16](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE16.png)



  VI. Then  “Profile Installed” screen should be appearing with the profile showing a green verified symbol. 


![17](https://github.com/ElizaKeffeler/blog/blob/main/IOS%20Bypassing%20/img/IMAGE17.png)



  VII. That’s it! Now Your device will proxy all HTTPS communications through Burp Suite with no problems! Happy testing!



For similar blogs click ![HERE](https://nvisium.com/news/)

Sources:   

1. Contributed By: Jon Gaines, nVisium Sr. Cybersecurity Consultant

2. https://theos.dev/docs/installation-ios

 
