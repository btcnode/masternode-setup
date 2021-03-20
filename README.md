Masternode Setup With A Script
Setting up a single BTN masternode using an installation script.

This guide is for setting up a BTNmasternode on a Ubuntu 16.04/18.04 64-bit server (VPS) and will be controlled from the local wallet on your computer. The wallet on the VPS that runs your masternode will be referred to as the remote wallet.

Requirements:


    A personal computer - this will run the local wallet, hold your 5000 BTN collateral and can be turned on and off without affecting the masternode

    A VPS server running Ubuntu 16.04/18.04 - this computer will be on 24/7 and runs the remote wallet and masternode

    A static IP address for your VPS

Local wallet installation:

    Download, install and sync the BTN wallet on your local computer. Wallet links can be found here.

    In this local wallet, go to Tools > Debug console and type the following command: createmasternodekey 
    This command will generate your Masternode Private Key. Save this key e.g. on Notepad as we will be using it later.
    
    3. Now enter the following command into the console:

 getaccountaddress "MN1" This will create a wallet address and masternode name for your masternode. Save this as we will need it later.
 
 4. Send 5000 BTN to the address generated in the previous step. IMPORTANT: In the Amount box, type in EXACTLY 5000. This transaction tells the blockchain that the address you are sending it to is a masternode. If you type in more or less than 5000 BTN, or attempt to split the payment into two transactions, it will be invalid for a masternode. When you press the Send button the wallet will calculate the proper transaction fee. Click Yes in the dialog box that follows and proceed to the next step.

5. Using your local wallet, wait for the first confirmation and then enter the debug console (Tools > Debug Console) and type the following command: getmasternodeoutputs This will display the transaction id followed by the output index (this is the proof of transaction of sending 1,000,000 BTN). Save this to a notepad as well.

6. In the local wallet’s toolbar, click Tools > Open Masternode Configuration File to open masternode.conf and add the following line:

<MN alias> <unique IP address>:17464 <your MN private key> <transaction ID (txhash)> <output index 0 or 1 (outputidx)>
  
  Save the file and restart the wallet.

Example as per above format:
MN1 67.234.12.34:17464 93HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg 2bcd3c84c84f87eaa86e4e56834c92927a07f9e18718810b92e0d0324456a67c 0

Example of the masternode.conf file
VPS remote wallet installation

To install the remote wallet first you will log into your VPS using the SSH client. After logging in, type the following commands into your VPS terminal.

1. Download the MN installation script
2. git clone https://github.com/btcnode/masternode-setup.git

2. Run the MN installation script

bash mn.sh

3. Follow the instructions
Starting your Masternode:

When the transaction has received 15 confirmations, the masternode is eligible to start. In the Masternodes tab, right-click on the masternode and choose Start alias.
How to verify that your masternode is running:

Go back to your windows wallet to check the masternode status: startmasternode alias false MN1

A message Masternode successfully started should appear.

after goto vps and run this command ./btcnode-cli getmasternodestatus


Something similar to this should appear:{
“txhash” : “334545645643534534324238908f36ff4456454dfffff51311”,
“outputidx” : 0,
“netaddr” : “45.11.111.111:17464”,
“addr” : “CmXhHCV6PjXjxJdSXPeC8e4PrY8qTQMBFg”,
“status” : 4,
“message” : “Masternode successfully started”
}

Now you can also double-check the masternode status in the BTN explorer.

Now some time your masternode will be activate

