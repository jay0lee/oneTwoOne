# oneTwoOne
A simple extension to prevent students from using other 1:1 Chromebooks

# Early Testing Guide
__WARNING__: this extension is meant for early testing only, it's not recommended yet for general student populations.
### Populate the location attribute of Chrome devices with comma separated list of allowed user logins.

A few examples:

Limit device to one user account:
```
Location: rgeorge6549@acme.edu
```
allow the following three students to use the device
```
Location: jsmith7877@acme.edu,tgregg4343@acme.edu,fscott2498@acme.edu
```
We don't really care what else is in the field as long as the email and comma are there:
```
Location: George Washington High,pswanson0937@acme.edu
```
Wildcard * allows any user for lab devices:
```
Location: *

Location: 4th grade lab rm122,*
```
if Location is empty, the device is unmanaged, the device is managed by another G Suite instance or the extension is running on a non-Chrome OS platform (Windows/Mac/Linux) then the extension should allow regular access.

### Force the extension to students who should be locked down
If teachers don't get the extension, they'll be able to login to any device.
1. admin.google.com > 3 bar menu at top left > Devices > Chrome management > Apps & extensions
1. Choose student testing OU to the left.
1. Yellow + circle at bottom right > yellow "grid" icon with tooltip "add Chrome app or extension by ID".
1. Extension ID: ```dlpapifgpjhgiadfeiehakoedhiajole```
1. Switch dropdown to "From a custom URL"
1. URL: ```http://onetwoone-lockdown.appspot.com/update.xml```
1. Click save. Now in the list of extensions change ```dlpapifgpjhgiadfeiehakoedhiajole``` from "Allow install" to "Force install". Click save at top right.

### Things to test
- It can take a while for changes to device location attribute to reach the device. Go to chrome://policy and force a refresh to speed up testing.
- Confirm student listed in location is able to login and access websites as usual.
- Confirm student not listed in location gets a popup on login and gets redirected to block page when browsing web.
- Confirm teacher and admin accounts that don't get the extension force installed won't be locked out of any device.
- You can get details about what the extension is doing in the extension console. chrome://extensions > oneTwo > background page > console tab. You'll want to allow devtools for force installed extensions while testing but block it in production to keep students from being able to kill the extension.
- The extension is currently comparing the user's email address against the device's location attribute because both of these attributes can be read by the extension _without Internet access_. This means students can't do a timed disconnect of Internet in order to break the extension. Future versions may support mapping students to devices with other fields.
