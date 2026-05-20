# Private 5G Network Testbed - User Guide

This guide outlines the steps required to boot, connect to, and use the existing Private 5G Network testbed. The network consists of an Open5GS core, an srsRAN gNodeB (using a USRP B210), and COTS (Commercial Off-The-Shelf) User Equipment.

## Step 1: System Boot & Core Network Check
The Open5GS core network is configured to run automatically in the background.

1. Turn on the PC.
2. From the BIOS/Dual-Boot menu, select **Ubuntu**.
3. Once logged in, open a terminal and verify that the core services are running:
   ```bash
   systemctl status open5gs-*


*(Ensure the services show as active/running).*

## Step 2: Hardware Setup (USRP B210)

1. Screw the antenna(s) securely onto the USRP B210.
2. Connect the USRP to the PC using a **USB 3.0** port.

## Step 3: Start the Base Station (gNodeB)

With the core running and the USRP connected, you can start the radio transmission.

1. From anywhere in the terminal, run the following command (replace the path with the actual location of your configuration YAML file):
```bash
sudo gnb -c "/path/to/your/config.yml"

```


2. **Note on Tracing:** If you want to view the live trace metrics in the console, press `t` and hit `Enter` after the gNodeB has initialized.

## Step 4: Smartphone (UE) & SIM Configuration

1. Insert a programmed Sysmocom SIM card into a modern 5G COTS UE (smartphone).
2. Follow the official [srsRAN COTS UE Tutorial](https://docs.srsran.com/projects/project/en/latest/tutorials/source/cotsUE/source/index.html) to configure the phone's hidden menus and force it to connect to the SA test network.
3. *Note: If you need to program a brand new SIM card, refer to the same guide above for the configuration parameters.*

## Step 5: Verify Connectivity

* Check your smartphone for the 5G cellular connectivity icon.
* Monitor the `srsRAN` trace in your terminal. If the connection is successful, you will see the UE attach and metric data (like CQI, RSRP, BLER) updating in the console.

## Step 6: Enable Internet Access

By default, the UE is connected to the core network but does not have outbound internet routing.

To grant the connected phone(s) access to the external internet, run the following command from anywhere in the terminal:

```bash
sudo givethemaccess
