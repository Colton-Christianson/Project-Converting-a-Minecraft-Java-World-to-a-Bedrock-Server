# Project: Converting a Minecraft Java World to a Bedrock Server

## Technologies Used
- [Chunker App](https://chunker.app) (Java-to-Bedrock world conversion)
- Ubuntu Server
- Intel NUC6i5SYB Mini PC (Bedrock server host)
- Minecraft Java Edition
- Minecraft Bedrock Edition
- USBImager
- PuTTY / PSCP
- SSH
- Common Linux utilities: `apt`, `chmod`, `ping`, `nslookup`, `nano`, `mv`, `rm`, `screen`

---

## Step 1: World Conversion and Testing

To begin, I used the Chunker App to convert my Minecraft Java Edition world (`Agartha`) to Bedrock format. The source world was located at: AppData\Roaming.minecraft\saves\Agartha

I uploaded the world to the Chunker App, selected the latest Bedrock edition, and converted it. After downloading the Bedrock-compatible world, I installed Minecraft Bedrock Edition on my PC. Despite owning the mobile version, I had to repurchase Bedrock Edition for Windows via the new Minecraft launcher.

After installation, I imported the converted world and confirmed a successful port by exploring key areas, including the Nether.

---

## Step 2: Creating a Bootable Ubuntu Server USB

1. Downloaded the latest Ubuntu Server ISO from the [official Ubuntu website](https://ubuntu.com/download/server).
2. Used USBImager to write the ISO to a PNY USB flash drive.
3. The process completed successfully, resulting in a bootable USB.

---

## Step 3: Installing Ubuntu Server on Intel NUC

### Challenges:
- **Display**: My monitor lacked an HDMI port, so I connected the NUC to a television with HDMI support.
- **Networking**: During installation, the NUC was not connected to my Ethernet switch. I completed the install, then moved the NUC to the office and connected it to the network.

I accessed BIOS, prioritized USB boot, and installed Ubuntu Server with default options. Once complete, I connected via SSH for remote configuration.

---

## Step 4: Bedrock Server Installation and Troubleshooting

### Issues Encountered:
- The official Bedrock Server link provided was broken.
- The initial Ubuntu Server install did not include internet utilities. I resolved this by installing them manually:

```bash
sudo apt update
```
```bash
sudo apt install ping dnsutils
```
### Workaround:
- Installed PuTTY and PSCP on my Windows machine to transfer files via SSH.
- Used Command Prompt (instead of PowerShell) for better PSCP compatibility.
- Unzipped the server files into a folder and made the binary executable:

```bash
chmod +x bedrock_server
```
```bash
./bedrock_server
```
Successful connections were established from both desktop and mobile devices.

---

## Step 5: Importing the Converted World to the Server

Initially, I attempted to place the converted world in the worlds directory and updated server.properties accordingly. Despite these efforts, the server generated a new world each time.
Successful Method:

1. Let the server generate its own default world folder.
2. Deleted all contents from the generated folder:

```bash
rm -r*
```

3.Unzipped the converted world into that same folder.

This method worked as expected, and the server loaded the intended world.

---

## Post-Installation Config

- Used `screen` to run the server persistently in the background:

```bash
screen -S bedrock
./bedrock_server
```

Then detached using `Ctrl + A, followed by `D`.
- Noticed missing entities. Re-added villagers with:

```bash
give @player villager_spawn_egg 2
```

---

