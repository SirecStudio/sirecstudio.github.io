# How to Configure the SS-CORE

Follow these steps to properly configure the _SS-CORE_ script on your RedM server:

#### Step 1: Set Your Server IP on the Website

1. Go to your account page on our website: [https://www.sirecstudio.com/account/my-account](https://www.sirecstudio.com/account/my-account).
2. Make sure to enter your server’s IP address in the designated field. This is crucial for linking your server with the license. You need enter only the IP without the port.

#### Step 2: Configure the License in SS-Core

1. Open the file `SS-Core/license.lua`.
2. In this file, locate the `YourSSLicense` variable.
3. Copy the license key from your account page (where you set the IP) and paste it as the value of `YourSSLicense`.

#### Step 3: Set Your Steam Access for CORE Panel Access

1. In `SS-Core`, open the file that controls access permissions (usually found in `config.lua` or similar).
2. Locate the `SteamAccess` variable.
3. Enter your Steam ID here to allow access to the CORE panel, enabling you to manage your scripts directly in-game.

#### Step 4: Enable SS-Core in server.cfg

1. After setting up the previous configurations, add `ensure SS-Core` in your `server.cfg` file. And all the others SS scripts must be below SS-Core.

***

#### Important Notes

* In fxmanifest.lua you can choice the framework !

By following these steps, your _SS-CORE_ script should be correctly configured and ready to manage all other scripts smoothly on your server.
