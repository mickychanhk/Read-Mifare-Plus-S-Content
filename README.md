# ReadMifarePlusSContent
I found out that it is very difficult to find how to read mifare plus s card memory content online, so I would like to create a java example for that

First of all, please download the NXP TagInfo App.
https://play.google.com/store/apps/details?id=com.nxp.taginfolite&hl=en

After that, open the app and try to tap your mifare plus s card, you will be able to see all the memory content if the mifare card is using default factory key to do authnication.
For my situation, the unique identifier content is stored in sector 2:
![Memory content](https://github.com/mickychanhk/ReadMifarePlusSContent/blob/master/image/memory%20address.png)

if your card has different key, please enter the key in app under "User Keys" in app menu : 
![User Keys](https://github.com/mickychanhk/ReadMifarePlusSContent/blob/master/image/mifare%20key%20insert%20in%20app.jpg?raw=true)
