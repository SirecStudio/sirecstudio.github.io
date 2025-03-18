# Configuration Helps

### **Configuration Options**

Below are the customizable options available in the `config.lua` file:

#### **1. General Settings:**

* **Dev Mode:** `Dev = true` – Enables debug mode for testing. Set to `false` for production. If enabled, administrators can test the join scene using `/testscene`.
* **New Character Intro:** `UseVideoNewCharacter = true` – If `true`, new players will be welcomed with an **intro scene** and AI voice.
* **Identity Requirement:** `SSIdentityCard = true` – If `true`, all new players **must** create an identity card before joining the server.
* **Wakeup Scene:** `UseRejoinScene = true` – Enables the **wake-up scene** for returning players, ensuring a smooth transition into the world.

#### **2. AI Voice Configuration:**

* **Gender Selection:** `Gender = "M"` – Determines the AI voice gender (`M` for male, `F` for female).
* **Voice Type:** `Voice = 4` – Selects the AI voice variant (up to 5 different voices available).
* **Customizable Welcome Message:**
  * **Text1:** `"Hello "` – The opening text before the player's name.
  * **Text2:** `", welcome to Sirec Studio server..."` – The rest of the welcome message after the player’s name.
  * The server owner can fully customize this message.

#### **3. City Spawn Locations:**

When joining the server, players can spawn in one of the following cities. Each location can have a unique **video intro** file or link:

* **Valentine:** `vector4(-167.455, 631.407, 114.032, 0.0)`
* **Blackwater:** `vector4(-798.759, -1205.143, 44.140, 0.0)`
* **Rhodes:** `vector4(1227.376, -1304.366, 76.904, 0.0)`
* **Saint Denis:** `vector4(2683.544, -1444.589, 46.254, 0.0)`
* **Strawberry:** `vector4(-1776.22, -435.98, 155.00, 0.0)`
* **Annesburg:** `vector4(2945.909, 1281.752, 44.623, 0.0)`
* **Armadillo:** `vector4(-3739.4717, -2607.5571, -14.1842, 0.0)`
* **Tumbleweed:** `vector4(-5514.7397, -2918.6450, -2.6882, 0.0)`

Each city can be configured to have a **default or custom intro video** (`video = "default.mp4"`).
