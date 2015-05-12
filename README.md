# Windows-Apps-Adobe-Analytics
Windows App using Adobe Analytics tracking

All of the examples provided here are using C#

You can find the official documentation [here](https://marketing.adobe.com/resources/help/en_US/mobile/winu/)

All up to date Adobe Analytics mobile SDKs can be found [here](https://github.com/Adobe-Marketing-Cloud/mobile-services/releases)

#Requirements

##Create an app in Adobe Mobile services

You need to create an app in Adobe Mobile Services : https://mobilemarketing.adobe.com/ . This will allow you to download the
latest mobile SDKs 4.x and the correct config file

###Replace the config file
You need to replace the ADBMobileConfig.json by the one downloaded from Adobe Mobile services:

0. Right-click you your project and select Add > Existing Item. 
0. Browse to ADBMobileConfig.json and click Add. 

###Change Build action for config file
Once you replace the config file by the one download from Adobe Mobile services, make sure to do the following:

0.Right-click ADBMobileConfig.json in your solution and select Properties. 
0.Change Build Action to Content. 

##Download an install the Windows Visual Studio for Marketing Cloud Solutions 4.x SDK

###Install from GitHub

Follow the steps provided in this [documentation](https://marketing.adobe.com/resources/help/en_US/mobile/winu/win_vse_4x.html)

##Change the debugger type

You need to change the debugger type to Native only or Mixed

#Code

For each project the following code was added to use Adobe analytics tracking in the file App.xaml.cs

```c#
using ADBMobile;
```
```c#
 public App()
        {
            this.InitializeComponent();
            this.Resuming += this.OnResuming;
            this.Suspending += this.OnSuspending;   
        }
```
```c#
 public App()
        {
            this.InitializeComponent();
            this.Resuming += this.OnResuming;
            this.Suspending += this.OnSuspending;   
        }
```
```c#
 protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            Debug.WriteLine("In OnLaunched");
            /*Adobe Analytics code start*/
            ADBMobile.Config.SetDebugLogging(true);
            //Start the lifecycle tracking
            ADBMobile.Config.CollectLifecycleData();
            //Send a normal pageView (State)
            ADBMobile.Analytics.TrackState("Test Adobe mobile windows app desktop", null);
            /*Adobe Analytics code end*/
            [...]
```
```c#
private void OnSuspending(object sender, SuspendingEventArgs e)
        {
            Debug.WriteLine("In OnSuspending");
            /*Adobe Analytics code start*/
            ADBMobile.Config.PauseCollectingLifecycleData();
            /*Adobe Analytics code end*/
            [...]
```
```c#
 private void OnResuming(object sender, object e)
        {
            Debug.WriteLine("In OnResuming");
            /*Adobe Analytics code start*/
            ADBMobile.Config.CollectLifecycleData();
            ADBMobile.Analytics.TrackState("Test Adobe mobile windows app desktop", null);
            /*Adobe Analytics code end*/
        }
```


