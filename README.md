# Read Mifare Plus S Card Content in Android
I found out that it is very difficult to find how to read mifare plus s card memory content online, so I would like to create a java example for that

My repository is basically download from TapLinx which is provided android SDK and provide adjustment: 
https://www.mifare.net/en/products/tools/taplinx/

I added the changes : 
1. Upgrade the code to Android X
2. Add code for reading memory address data

(I am using Samsung Galaxy S10+, Android 10 for this project)

First of all, please download the NXP TagInfo App.
https://play.google.com/store/apps/details?id=com.nxp.taginfolite&hl=en

After that, open the app and try to tap your mifare plus s card, you will be able to see all the memory content if the mifare card is using default factory key to do authnication.
For my situation, the unique identifier content is stored in sector 2:
![Memory content](https://github.com/mickychanhk/ReadMifarePlusSContent/blob/master/image/memory%20address.png)

if your card has different key, please enter the key in app under "User Keys" in app menu : 
![User Keys](https://github.com/mickychanhk/ReadMifarePlusSContent/blob/master/image/mifare%20key%20insert%20in%20app.jpg?raw=true)

For the code,  the core section is in MainActivity.Java line 975
```Java
byte sector = (byte)2;
int memoryaddress = plusSL3.sectorNumberToBlockNumberForAESKeys(sector);
plusSL3.authenticateFirst(memoryaddress, objKEY_AES128, pcdCap2In);
result = plusSL3.multiBlockRead(IPlusSL3.ReadMode.Plain_ResponseMACed_CommandMACed, 8, 3);
```
Usually the mifare memory address start from **0x4004** which is referred to **sector 2** in our example

After finding the memory address, you are require to authenticate your card : 

```Java
plusSL3.authenticateFirst(memoryaddress, objKEY_AES128, pcdCap2In);
```

For the variable **objKEY_AES128**, which is provided by NXP library, For mifare plus s which is using AES algorithm, which require using a 16 byte as a key to authnicate the card. The factory key of the card should be 16 byte all in 0xFF

You could edit the key under SampleAppKeys.Java
```Java
 public static final byte[] KEY_AES128 = {(byte) 0xFF, (byte) 0xFF,
            (byte) 0xFF, (byte) 0xFF, (byte) 0xFF, (byte) 0xFF, (byte) 0xFF,
            (byte) 0xFF, (byte) 0xFF, (byte) 0xFF, (byte) 0xFF, (byte) 0xFF,
            (byte) 0xFF, (byte) 0xFF, (byte) 0xFF, (byte) 0xFF};
```

