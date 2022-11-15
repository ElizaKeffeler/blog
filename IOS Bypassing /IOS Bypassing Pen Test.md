


IOS 14 Corellium SSL Pinning Bypass

-----------------------------------------------

 Recently, some of the projects at nVisium have involved executing iOS penetration tests against a production application. 
 During this process, some of the applications only supported iOS 14.1 and higher, which is soon to become an industry standard. 
 In these instances, our team members have had to find a different way to bypass SSL. After doing extensive research, we found 
 that by using Corellium iOS 14 VM to proxy through Burp suite, you can bypass SSL pinning. 



HERE IS THE STEP-BY-STEP GUIDE:



Within this example, a  iPhone X VM running iOS 14.1 and is jailbroken: 






1. INSTALL THEOS:  

 A cross-platform build system for creating iOS and other programs, later will be use to bypass SSL pinning.

- Open Cydia (update or upgrade if needed), 


-Within Cydia:

Add  new repo

Click "Sources”

Then click "Edit”

Then click “Add” 

Input URL:

http://repo.bingner.com/ 

Click “Add Source” to confirm



- Now, search and install the Theos Dependencies 








2. SETUP THEOS ENVIRONMENT VARIABLE: 

-Open a terminal on the device and execute the following commands:

echo "export THEOS=~/theos" >> ~/.profile





git clone --recursive https://github.com/theos/theos.git $THEOS





curl -LO https://github.com/theos/sdks/archive/master.zip & TMP=$(mktemp -d) & unzip master.zip -d $TMP & mv $TMP/sdks-master/*.sdk $THEOS/sdks & rm -r master.zip $TMP





3. INSTALL SWIFT-TOOLCHAIN:

-Reopen Cydia

-Search and install “swift-toolchain” from the BigBoss Repo (Default in Cydia)







4. INSTALL SSLBYPASS TOOL:

-Go back to the device’s terminal and install the SSLBypass tool: 



git clone https://github.com/evilpenguin/SSLBypass





cd SSLBypass/packages







dpkg -i com.evilpenguin.sslbypass_1.0-5+debug_iphoneos-arm.deb





-Restart SpringBoard so the new tool goes into effect. NOTE: Device’s screen should flashing. 

- Then killall SpringBoard





6. Install Burp Suite’s Certificate:

-Connect to the Corellium VPN, set Burp Suite to listen on your VPN's IP.



-Then set a manual proxy within the WI-FI settings of the iPhone to proxy through Burp Suite.





-Open Safari, go to http://burp ,Click the "CA Certificate" button and click “Allow”. 



-Go to iPhone Settings and Select “General”, Select “Profile” 





-Select the PortSwigger CA profile and click "Install" 3 times.





-Then  “Profile Installed” screen should be appearing with the profile showing a green verified symbol. 





  That’s it! Now Your device will proxy all HTTPS communications through Burp Suite with no problems! Happy testing!

For similar blogs click HERE

Sources:   

1. Contributed By: Jon Gaines, nVisium Sr. Cybersecurity Consultant

2. https://theos.dev/docs/installation-ios

 