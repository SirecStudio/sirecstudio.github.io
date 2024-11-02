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

1. After setting up the previous configurations, add `ensure SS-Core` in your `server.cfg` file.
2. **Important**: Do not ensure other SS scripts directly in `server.cfg`. Only `SS-Core` should be ensured this way, as it will manage other scripts automatically.

#### Step 5: Using the CORE Panel

1. To manually start or stop scripts while you’re on the server, type `/sscore` in the server’s command line. This opens the SS-CORE panel, where you can control all linked scripts.

#### Step 6: Autostart Scripts (Optional)

1. If you prefer to autostart scripts downloaded from our website, open `config.lua` in `SS-Core`.
2. Set `Autostart = true` to have the SS-CORE automatically launch compatible scripts at server start.

***

#### Important Notes

* **Only SS-Core**: Ensure only `SS-Core` in your `server.cfg`. All other SS scripts are managed through this central script.
* **CORE Panel**: Remember that access to the CORE panel is managed via the Steam ID you set in `SteamAccess`.

By following these steps, your _SS-CORE_ script should be correctly configured and ready to manage all other scripts smoothly on your server.
