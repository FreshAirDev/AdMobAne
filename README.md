Admob Native Extension for Adobe Air
=========

This  AdMob will add the support to use AdMob Mobile monetization platform with Adobe Air.
The Extension support Android Platform and iOS Platform.
Different Packages are available according to the needs'
- Android Only
- iOS Oly
- Both Platforms

##Admob SDK Details
- Android: Google Play services ver. 5.0
- iOS: Admob SDK 6.11.1 (Admob SDK 6.8.0 in iOS 4.3 compatible version)

##Device Compatibility:
Android: From version 2.3<br>
iOS: From version 4.3<br>

##Features:
- Set Render mode type (Android Only)
- Set Specific test Device ID
- Create Single or Multiple Banners for Application
- Move Banner, allow also to animate the banner
- Full Interstitial Ads Management and Pre-caching
- Full Request Customization
- Get Banner Dimensions
- Get Device Screen Dimension
- Custom Absolute Position
- Auto relative Docking position for:
```javascript
TOP_LEFT
TOP_CENTER
TOP_RIGHT
MIDDLE_LEFT
MIDDLE_CENTER
MIDDLE_RIGHT
BOTTOM_LEFT
BOTTOM_CENTER
BOTTOM_RIGHT
```
- Support Any adMob Size:
```javascript
BANNER
MEDIUM_RECTANGLE
LARGE_BANNER
FULL_BANNER
LEADERBOARD
WIDE_SKYSCRAPER
SMART_BANNER
SMART_BANNER_PORT
SMART_BANNER_LAND
```

##Install the library
Add the AdMob ANE library to your project.<br>
In Flash Builder 4.7:

  1. Go to Project Properties
  2. Select Native Extensions under Actionscript Build Path
  3. Choose Add ANE... and navigate to the AdMob.ane file
  4. Select Actionscript Build Packaging > Google Android, Apple IOS or Both
  5. Select the Native Extensions tab, and click the 'Package' check box next to the extension

Please note:<br>
When adding the ANE be sure to have the checkbox "Update Air Application Descriptor" selected.<br>
If it is not selected make certain that the application Id is available in the Air Application Descriptor as follow:
```xml
<extensions>
	<extensionID>com.freshairdev.ane.admobane</extensionID>
</extensions>
```

##Usage
Import the library
```javascript
import com.freshairdev.ane.admobane.AdMobManager;
```

Get The Manager Instance
```javascript
var adMobManager:AdMobManager = AdMobManager.manager;
```

Check Extension Support
```javascript
if(adMobManager.isSupported){
    ...
}
```

Set Manager Verbose Mode [Optional]<br>
The Verbose mode will allow to have debug output from all places, AS, Java and iOS console
```javascript
adMobManager.verbose = true;
```

Set The Render mode [Optional, default Hardware]<br>
This setting will allow to set the render mode for the banner.<br>
The available setting are None, Hardware and Software. The use of the render mode vary according to the application.
```javascript
adMobManager.renderLayerType = AdMobManager.RENDER_TYPE_HARDWARE;

```

Set Manager Operation Mode [Optional... Until Operation]<br>
This setting will allow to set the extension in either test mode or operation mode.<br>
By default the extension will work in Test Mode, when the application needs to be release it will be needed to switch the operation into Production mode
```javascript
adMobManager.operationMode = AdMobManager.TEST_MODE;

```

Set The test device ID<br>
This setting will prevent impression counts during testing for the specified ID.
```javascript
adMobManager.testDeviceID = "MY_DEVICE_ID";

```

Set Common AdMob Unit Id for Banners [Recommended]
Setting a common Admob Id will allow to avoid to specify an Id during banner creation
If the manager has an adMob unit id set all the banner will be created using that id, unless a new id s specified during banner creation.
In that case the banner will use the id included on its parameters.
```javascript
adMobManager.bannersAdMobId = "ADMOB_BANNER_ID";
```

Set Common AdMob Unit Id for interstitial [Recommended]
Same as for the banner the common AdMob Id for interstitial will be use for any interstitial created unless a new id is given during interstitial creation.
In that case the interstitial will use the id included on its parameters.
```javascript
adMobManager.interstitialAdMobId = "ADMOB_INTERSTITIAL_ID";
```

Set Gender Request Targeting [Optional]
This setting allow to create the ad request specifically for a gender.
Please note that all banner created after will included the given gender.
Request targeting option can be update before the creation of new banner for offer different target banner.
```javascript
adMobManager.gender = AdMobManager.GENDER_MALE;
```

Set Birthday Request Targeting [Optional]
This setting allow to have specific banner for a given age
If wish to set the age range then the year will be mandatory, while month and day can be optional.
If month and day are not specified the default value of 1 will be used.
Request targeting option can be update before the creation of new banner for offer different target banner.
```javascript
adMobManager.birthYear = 1996;
adMobManager.birthMonth = 1;
adMobManager.birthDay = 24;
```

Set the Tag for child directed treatment [Optional]
This setting allow to have specific banner for a children in accordance to Children's Online Privacy Protection Act (COPPA).
Request targeting option can be update before the creation of new banner for offer different target banner.
```javascript
adMobManager.isCDT = true;
```

This getter will allow to get the current quantity of banner created and available in the Manager
```javascript
var num:int = adMobManager.bannersQuantity;
```

This getter will allow to get all the banners id of banner created and available in the Manager
```javascript
var bannerIds:Array = adMobManager.bannersNames;
```

This getter will allow to get the information of which device is currently in use (Android or iOS)
```javascript
var device:String = adMobManager.device;
```
Get the Current Screen Size
```javascript
var screenSize:ScreenSize =  AdsManager.getScreenSize();
```
Get a Standard Banner Size
```javascript
var adSize:AdSize =  AdsManager.getBannerSize(AdMobSize.BANNER);
```
Get the Specific Banner Size in the Screen after the banner Creation
```javascript
var adSize:AdSize =  AdsManager.getExistingBannerSize("BottomBanner");
```

Create an AdMob Banner in an relative Position<br>
The parameter ae as follow:
- Banner Size (Banner specific size)
- Banner Position (Banner specific Position)
- Banner Id (Useful when you wish to create more than one banner.If an id is not specified a random id will be generated)
- AdMobId (Banner specific AdMobId, Useful if you are tracking the banner result assigning individual id. If an id is not specified the common id will be used.)
- AutoShow Option (This option allow to automatically show the banner one it is loaded.)
```javascript
adMobManager.createBanner(AdMobSize.BANNER,AdMobPosition.BOTTOM_CENTER,"BottomBanner", null, true);
```

Create an AdMob Banner in an absolute Position<br>
The parameter ae as follow:
- Banner Size (Banner specific size)
- Banner X Position (Banner specific X Position)
- Banner Y Position (Banner specific Y Position)
- Banner Id (Useful when you wish to create more than one banner.If an id is not specified a random id will be generated)
- AdMobId (Banner specific AdMobId, Useful if you are tracking the banner result assigning individual id. If an id is not specified the common id will be used.)
- AutoShow Option (This option allow to automatically show the banner one it is loaded.)
```javascript
adMobManager.createBannerAbsolute(AdMobSize.BANNER,100, 200, "BottomBanner", null, true);
```

Move a specific Banner after creation<br>

The function will allow to move a specific banner, recognized by its Id.<br>
This allow to also create banner animation when the banner is created<br>
The parameter are as follow:
- Banner Id (Specific banner Id for the banner to be move)
- Banner X Position (Banner specific X Position)
- Banner Y Position (Banner specific Y Position)
```javascript
adMobManager.moveBanner(bannerId,posX,posY);
```

Show a specific Banner<br>
The function will allow to show a specific banner, recognized by its Id.<br>
This is specifically useful when your app wish to manage several ads.<br>
The parameter are as follow:
- Banner Id (Specific banner Id for the banner to be show)
```javascript
adMobManager.showBanner("BottomBanner");
```

Hide a specific Banner<br>
The function will allow to hide a specific banner, recognized by its Id.<br>
This is specifically useful when your app wish to manage several ads.<br>
The parameter are as follow:
- Banner Id (Specific banner Id for the banner to be hide)
```javascript
adMobManager.hideBanner("BottomBanner");
```

Remove a specific Banner<br>
The function will allow to remove a specific banner, recognized by its Id.<br>
This is specifically useful when your app wish to manage several ads.<br>
The parameter are as follow:
- Banner Id (Specific banner Id for the banner to be moved)
```javascript
adMobManager.removeBanner("BottomBanner");
```

Show all existing hidden banners<br>
The function will show all available banners
```javascript
adMobManager.showAllBanner();
```

Hide all existing hidden banners<br>
The function will hide all available banners
```javascript
adMobManager.hideAllBanner();
```

Remove all existing hidden banners<br>
The function will remove all available banners
```javascript
adMobManager.removeAllBanner();
```

Create the AdMob Interstitial<br>
The parameter are as follow:
- Interstitial AdMobId (specific AdMobId. If an id is not specified the common id will be used.)
- AutoShow Option (This option allow to automatically show the Interstitial one it is loaded.)
```javascript
adMobManager.createInterstitial(null,true);
```

Show the AdMob Interstitial<br>
The function will show the cached AdMob Interstitial
```javascript
adMobManager.showInterstitial();
```

Check the Interstitial load state
```javascript
var state:Boolean = adMobManager.isInterstitialLoaded();
```

Remove the AdMob Interstitial<br>
The function will allow to remove the Interstitial when needed.<br>
This is specifically usefull when there is the need to remove an Interstitial without the user interaction.
```javascript
adMobManager.removeInterstitial();
```

##Listen to Events
In order to listen to event you need to attache the event listener to the extension dispatcher.<br>
The easiest way is to create an internal dispatcher instance:
```javascript
private function get dispatcher():EventDispatcher
{ return adMobManager.dispatcher; }
```

Then you can add all the listener for the event you need:
```javascript
    dispatcher.addEventListener(AdMobEvent.BANNER_LOADED, onBannerLoaded);

static private function onBannerLoaded(e:AdMobEvent):void
{
    // Do Something...
}
```

The event will also pass the banner id for the banner who did dispatch the event.<br>
The example above will show all the banner, if you wish to, for example, show only<br>
the specific banner who did dispatch the event you can do as follow:

```javascript
static private function onBannerLoaded(e:AdMobEvent):void
{
    // Show the specific banner who did dispatch the event
    adMobManager.showBanner(e.data);
}
```

The Extension available Event are as follow:
```javascript
BANNER_LOADED
BANNER_FAILED_TO_LOAD
BANNER_AD_OPENED
BANNER_AD_CLOSED
BANNER_LEFT_APPLICATION
INTERSTITIAL_LOADED
INTERSTITIAL_FAILED_TO_LOAD
INTERSTITIAL_AD_OPENED
INTERSTITIAL_AD_CLOSED
INTERSTITIAL_LEFT_APPLICATION
```

##Setup for Android
Update Your Application Descriptor<br>
You'll need to be using the AIR 3.1 SDK or higher, include the extension in your Application Descriptor XML, and update the Android Manifest Additions with additional settings.<br>
Add the following settings in "manifest" tag.
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

Add the following settings in "application" tag.
```xml
<meta-data android:name="com.google.android.gms.version" android:value="4452000"/>
<activity android:name="com.google.android.gms.ads.AdActivity" android:configChanges="keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize" />
```
