# androidBackgroundApp

Usage

The plugin creates the object cordova.plugins.backgroundMode and is accessible after the deviceready event has been fired.

document.addEventListener('deviceready', function () {
    // cordova.plugins.backgroundMode is now available
}, false);
Enable the background mode

The plugin is not enabled by default. Once it has been enabled the mode becomes active if the app moves to background.

cordova.plugins.backgroundMode.enable();
// or
cordova.plugins.backgroundMode.setEnabled(true);
To disable the background mode:

cordova.plugins.backgroundMode.disable();
// or
cordova.plugins.backgroundMode.setEnabled(false);
Check if running in background

Once the plugin has been enabled and the app has entered the background, the background mode becomes active.

cordova.plugins.backgroundMode.isActive(); // => boolean
A non-active mode means that the app is in foreground.

Listen for events

The plugin fires an event each time its status has been changed. These events are enable, disable, activate, deactivate and failure.

cordova.plugins.backgroundMode.on('EVENT', function);
To remove an event listeners:

cordova.plugins.backgroundMode.un('EVENT', function);
Android specifics

Transit between application states

Android allows to programmatically move from foreground to background or vice versa.

cordova.plugins.backgroundMode.moveToBackground();
// or
cordova.plugins.backgroundMode.moveToForeground();
Back button

Override the back button on Android to go to background instead of closing the app.

cordova.plugins.backgroundMode.overrideBackButton();
Recent task list

Exclude the app from the recent task list works on Android 5.0+.

cordova.plugins.backgroundMode.excludeFromTaskList();
Detect screen status

The method works async instead of isAcive() or isEnabled().

cordova.plugins.backgroundMode.isScreenOff(function(bool) {
    ...
});
Unlock and wake-up

A wake-up turns on the screen while unlocking moves the app to foreground even the device is locked.

// Turn screen on
cordova.plugins.backgroundMode.wakeUp();
// Turn screen on and show app even locked
cordova.plugins.backgroundMode.unlock();
Notification

To indicate that the app is executing tasks in background and being paused would disrupt the user, the plug-in has to create a notification while in background - like a download progress bar.

Override defaults

The title, text and icon for that notification can be customized as below. Also, by default the app will come to foreground when tapping on the notification. That can be changed by setting resume to false. On Android 5.0+, the color option will set the background color of the notification circle. Also on Android 5.0+, setting hidden to false will make the notification visible on lockscreen.

cordova.plugins.backgroundMode.setDefaults({
    title: String,
    text: String,
    icon: 'icon' // this will look for icon.png in platforms/android/res/drawable|mipmap
    color: String // hex format like 'F14F4D'
    resume: Boolean,
    hidden: Boolean,
    bigText: Boolean
})
To modify the currently displayed notification

cordova.plugins.backgroundMode.configure({ ... });
Note: All properties are optional - only override the things you need to.

Run in background without notification

In silent mode the plugin will not display a notification - which is not the default. Be aware that Android recommends adding a notification otherwise the OS may pause the app.

cordova.plugins.backgroundMode.configure({ silent: true });
