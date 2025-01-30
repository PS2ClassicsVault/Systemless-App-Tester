## APP SETUP:

To setup your app to test here is how you can test it:

1). you will need to place your app within one of two folders the available folders are:


- app

- priv-app

These are where your app will systemlessly install to, but do not worry systemless apps will be removed once the module has been removed,they do not actually install via the /system partition permanently.


When you add your app for example in your adding a app to /system/app you will need to create a sub folder of the app(s) name like for example say you have a app called Name.apk 

youu would create a sub-folder Named whatever you like, but for us we will name the sub-folder to "Name" this will show up like this "/system/app/Name"


Now in that sub-folder place the apk in it, as shown below with the Name.apk we made up:

- /system/app/Name/Name.apk

Now that you successfully did that, we need to mention that some apps requires other dependancies such as their libary files.

for example say our Name.apk has a "lib" folder in the app itself you will need to extract that lib folder and place it in "/system/app/Name"

Now you may think that is all you have to do, but your not quite done yet. In most cases in that lib folder you may see  severa arch folders such as follows:

- arm64-v8a, armeabi-v7a, x86, x86_x64


for the app to function properly.you will need to focus on the arm64-v8a and the armeabi-v7a folder and rename them as follows:

- arm64
- arm

Once your do this you're done with this step, Tis step also applies if you're using the priv-app folder.


----------------------------------------------------


## PERMISSIONS SETUP:

Permissions allows android to read these permissions when the app requests them to function. This is the most tedious step because it requires you to setup each permission the app has available one by one manually this will take time to do and we highly suggest not to rush it because a single mistake could ruin your day, if you need to see what permissions your app uses we recommend this application on the Google Play Store: [Apk Analyzer by Martin Styk](https://play.google.com/store/apps/details?id=sk.styk.martin.apkanalyzer)

This can display all the permissions the app uses and you can copy and oaste them in the xml file located in "/system/etc/permissions"

We have provided an xml file for you in the directory we mentioned above this is where tou will setup permissions for your app.

in the directory you will see a file named "name.of.package.xml"

you will need to rename the file to whatever your apps package name is for example our Name.apk it sill look like this with a made up package name like this: 

- org.name.cyberdev.xml 

This will tell the OS what app this permission goes to.

Now open up that file in a text editor and you can now edit/add/remove permissions according to what the apps used permissions are. It will be displayed like this w/out the quotation marks:

"<?xml version="1.0" encoding="utf-8"?>
<permissions>
    <app-permissions package="name.of.package">
        <permission name="android.permission.UNKNOWN"/>
        <permission name="android.permission.UNKNOWN"/>
        <permission name="android.permission.UNKOWN"/>
        <permission name="android.permission.UNKNOWN"/>
    </app-permissions>
</permissions>"


you can see how it's setup and it's very easy to setup as long as you take your time of course.

Now to begin lets view the first line we need to edit:

This is where you will place the package name.
                                 |
                           ↓---------------↓
<app-permissions package="name.of.package">
  ↑_________________↑
           |
This will tell android were the app is located if your app is located in the priv-app folder you will need to edit it like shown below:

<privapp-permissions package="name.of.package">


Now lets go to the permissions section:
Each permission has its own bracket, you cannot add multiple permissions in a single bracket.

        <permission name="android.permission.UNKNOWN"/>

say your app requires to post notifications and has a permission to specify rhat the app requires notifications access you would thus adjust the permissions mentioned in the app we recommended to use earlier and implement it as shown below:

        <permission name="android.permission.POST_NOTIFICATIONS"/>


Now your app has multiple of permissions to add here is how you would do it:


       <permission name="android.permission.POST_NOTIFICATIONS"/>
       <permission name="android.permission.UNKNOWN"/>

Now you show see how the permission goes to the next line and is aligned with the previous <permission position?

each beginning of each permission needs to be aligned to the previous one, it does matter how its formatted, each line but be the exact position no matter what otherwise android cannot properly read the permission.

its mostly a rinse and repeat process and trust me it can take good amount of time to do it depending how many permissions an app requests.

for the beginning and end of the permissions list you will see these lines:

<?xml version="1.0" encoding="utf-8"?>
<permissions>
    </app-permissions>
</permissions>"

if your app is placed in the /system/app folder then you do not ned to do anything with these lines.

however if your app is placed in the /system/priv-app folder then some changes need to be made use the following example on how you would set it up



"<?xml version="1.0" encoding="utf-8"?>
<permissions>
    <privapp-permissions package="name.of.package">
        <permission name="android.permission.UNKNOWN"/>
        <permission name="android.permission.UNKNOWN"/>
        <permission name="android.permission.UNKOWN"/>
        <permission name="android.permission.UNKNOWN"/>
    </privapp-permissions>
</permissions>"


Once you have all your permissions setup, just zip up this module from the root of it and install and reboot your device.

But keep in mind this module wasn't built to build your own magisk module using this as a base, please make your own flasher this is for testing purposes only!
