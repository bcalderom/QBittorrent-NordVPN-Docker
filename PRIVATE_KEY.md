
### How To Get Your  `PRIVATE_KEY`

[](https://github.com/bubuntux/nordlynx/pkgs/container/nordlynx#how-to-get-your-private_key)

To get your  `PRIVATE_KEY`  you will need to get an access token from the NordVPN website and then use the  [https://github.com/bubuntux/nordvpn](https://github.com/bubuntux/nordvpn)  container.

1.  Log in to  [https://nordvpn.com/](https://nordvpn.com/)
    
2.  On the left side, click on  **NordVPN**
    
3.  In the middle, under  **Manual setup**, click on  **Set up NordVPN manually**  and go through the verification process
    
4.  On the new page, in the middle, in the  **Access token**  box, click on  **Generate new token**
    
5.  In the  **Generate new token?**  pop-up box, select  **Set to expire in 30 days**  and click  **Generate token**
    
6.  In the  **Copy access token**  pop-up box, click the  **Copy**  linnk to copy your token
    
7.  From your computer where Docker is installed, run the below command and replace  `{{{TOKEN}}}`  with what you copied from step 6 above:
    
    ```
    docker run --rm --cap-add=NET_ADMIN -e TOKEN={{{TOKEN}}} ghcr.io/bubuntux/nordvpn:get_private_key
    
    ```
    
8.  Docker will do it's thing and spit out your  `PRIVATE_KEY`:
    
    ```
    user@hostname:~/docker> docker run --rm --cap-add=NET_ADMIN -e TOKEN=[redacted] ghcr.io/bubuntux/nordvpn:get_private_key
    Unable to find image 'ghcr.io/bubuntux/nordvpn:get_private_key' locally
    get_private_key: Pulling from bubuntux/nordvpn
    06d39c85623a: Pull complete 
    3e1c241a05c8: Pull complete 
    0077b26e8dce: Pull complete 
    Digest: sha256:0d91aabb4511d400b01e930654950729a4e859d3c250f61664662b0ed7027c56
    Status: Downloaded newer image for ghcr.io/bubuntux/nordvpn:get_private_key
    Waiting for daemon to start up...
    A new version of NordVPN is available! Please update the application.
    Welcome to NordVPN! You can now connect to VPN by using 'nordvpn connect'.
    A new version of NordVPN is available! Please update the application.
    Technology is already set to 'NORDLYNX'.
    A new version of NordVPN is available! Please update the application.
    Connecting to United States #5831 (us5831.nordvpn.com)
    You are connected to United States #5831 (us5831.nordvpn.com)!
    ############################################################
    IP: 10.5.0.2/32
    Private Key: [!!! THIS IS YOUR PRIVATE_KEY YOU NEED !!!]
    ＼(＾O＾)／############################################################
    user@hostname:~/docker> 
    
    ```
    
9.  Copy everything after  `Privatey Key:` (note the space after  `:`) to the end of the line -- this is your  `PRIVATE_KEY`


Source:
https://github.com/bubuntux/nordlynx/pkgs/container/nordlynx#how-to-get-your-private_key 