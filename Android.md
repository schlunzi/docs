
Embed VRPlayer to activity
 
1.    Add fragment to activity layout xml file
 
<fragment
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:name="com.omnivirt.vrkit.VRPlayerFragment"
	android:id="@+id/vrplayer_fragment" />
 
 
2.    Import vrkit into your code
 
import com.omnivirt.vrkit.*;
3.    Add the following snippet to activity code
 
VRPlayerFragment  player = (VRPlayerFragment)this.getFragmentManager().findFragmentById(R.id.vrplayer_fragment);
player.load(CONTENT_ID);
player.setCardboard(CARDBOARD_MODE);
 
4.    Implement interface OnVRPlayerInteractionListener and add the following functions:
 
void onFragmentCreated();
void onLoaded(Integer maximumQuality, Quality currentQuality, Mode cardboardMode);
void onStarted();
void onPaused();
void onEnded();
void onSkipped();
void onDurationChanged(Double value);
void onProgressChanged(Double value);
void onBufferChanged(Double value);
void onSeekChanged(Double value);
void onCardboardChanged(Mode value);
void onAudioChanged(Double value);
void onQualityChanged(Quality value);
void onExpanded();
void onCollapsed();
void onLatitudeChanged(Double value);
void onLongitudeChanged(Double value);
void onSwitched(String sceneName, Array history);
 
 
Open VR Ad
 
1.    Import vrkit into your code
 
import com.omnivirt.vrkit.*;
 
2.    Use the following code to load VRAd
 
VRAd  vrAd = new VRAd(ADSPACE_ID, ACTIVITY);
vrAd.load();
 
3.    Implement OnVRAdInteractionListener interface and add the following functions
 
void onAdStatusChanged(VRAd instance, AdState status);
 
4.    To start VRAd wait for status to change to “Ready” and call the following:
 
vrAd.show(CARDBOARD_MODE);
        	
 
Scan QR Code
 
1.    Add the following to app build.gradle
 
compile 'com.google.android.gms:play-services:7.8.0'
 
2.    Import vrkit into your code
 
import com.omnivirt.vrkit.*;
 
3.    Call the following function to open QR Code scanner
 
QRReaderFragment.launchCardboardQRScanner(ACTIVITY);
 
 


# VR Player and Monetization for App Developers

OmniVirt makes the leading player for 360 video experiences across mobile and desktop. 
Upload your 360 content to OmniVirt and serve it into your app. 

The OmniVirt advertising platform enables developers and publishers to monetize their apps with engaging VR content.
Simply integrate the OmniVirt SDK into your iOS, Android or Web application and get paid for presenting sponsored 360 video experiences to your users. Backfill your inventory with premium CPM experiences from OmniVirt’s network of advertisers. We support both 360° and 2D video ads inside VR apps.

Contact us for more info at [contact@omnivirt.com](mailto:contact@omnivirt.com).
Visit [www.omnivirt.com](https://www.omnivirt.com/) to upload content or create ad space.


## Add the OmniVirt SDK to your app
 
1.    Save the VRKit-release.aar file under app module's libs folder (eg: <project>/<app>/libs/VRKit-release.aar)
2.    Add the below to build.gradle of your "app" module folder (not your project root build.gradle). Note the name in compile line, it is VRKit-release @aar not VRKit-release.aar.
<pre>
dependencies {
 	compile 'com.omnivirt.vrkit: VRKit-release @aar'
} 
 
repositories {
 	flatDir {
     	dirs 'libs'
	}
}
</pre>

## Use the OmniVirt Player

### Display your own VR content
1. Sign up for an account at [OmniVirt](www.omnivirt.com)
2. Upload your VR/360-degree photo or video at [OmniVirt](https://www.omnivirt.com/).
3. OmniVirt will assign an ID to your content as part of the upload. Copy the content ID and pass it to the VRPlayer's launch method.

### Monetize your app with sponsored VR content

1. Sign up for an account at [OmniVirt](www.omnivirt.com)
2. Create one or more Ad Spaces for your app (for each Ad Space you can select different content and will get separate reporting)
3. Select what content to run in each Ad Space (e.g. OmniVirt's network ads)
4. Add one or more instances of the OmniVirt VRPlayer to your app (one for each Ad Space)

## Tutorials
### Add a Full Screen VRPlayer
 
1. Add the following to AndroidManifest.xml
<pre>
<activity android:name="com.omnivirt.vrkit.FullscreenVRPlayer"
    android:configChanges="orientation|screenSize"></activity>
</pre>

2. Import vrkit into your code
<pre>
import com.omnivirt.vrkit.*;
</pre>
3.    To open fullscreen player with adspace use the following code:
<pre>
FullscreenVRPlayer.launch(YOUR_ACTIVITY, CONTENT_ID, AUTOPLAY, CARDBOARD_MODE, ADSPACE_ID)
 </pre>
4.    To open fullscreen player with no adspace use the following code instead:
<pre>
FullscreenVRPlayer.launch(YOUR_ACTIVITY, CONTENT_ID, AUTOPLAY, CARDBOARD_MODE);
</pre>
 
5.    Implement interface OnVRPlayerInteractionListener in the caller activity and add the following functions:
<pre>
void onFragmentCreated();
void onLoaded(Integer maximumQuality, Quality currentQuality, Mode cardboardMode);
void onStarted();
void onPaused();
void onEnded();
void onSkipped();
void onDurationChanged(Double value);
void onProgressChanged(Double value);
void onBufferChanged(Double value);
void onSeekChanged(Double value);
void onCardboardChanged(Mode value);
void onAudioChanged(Double value);
void onQualityChanged(Quality value);
void onExpanded();
void onCollapsed();
void onLatitudeChanged(Double value);
void onLongitudeChanged(Double value);
void onSwitched(String sceneName, Array history);
</pre>


### Add an Ad Space programmatically
To add an Ad Space in your app, create a new instance of the VRAd object to your view controller.
   <pre>
   let myAd = VRAd.create(withAdSpaceID: 1000, andViewController: self, andListener: self) //replace 1000 with your Ad Space ID
   </pre>
To load an ad from the network for you Ad Space call the load method
   <pre>
   myAd.load()
   </pre>
You can listen to the ad state to check when the ad is ready to display
   <pre>
   func adStatusChanged(withAd ad: VRAd, andStatus status: AdState) {
     switch (status) {
       case AdState.NONE:
         break;
       case AdState.LOADING:
         ...
       case AdState.READY:
         // Set the button into ready status. So, we can launch the ad space.
         startAdButton.setTitle("Start Ad", for: UIControlState.normal);
         ...
       case AdState.SHOWING:
         ...
       case AdState.COMPLETED:
         ...
       case AdState.FAILED:
         ...
     }
   }
   </pre>
Once the ad is ready to display you can call the show method on the ad.
    <pre>
	myAd.show(withCardboardMode: Mode.OFF)
   </pre>
   
### Use Storyboard to add a VRPlayer

This tutorial shows you how to make fullscreen cardboard app within minutes.

Inside the ViewController of the sample app you will find the Player view, which subclasses VRPlayer. **If you plan to use VRPlayer in both landscape and portrait orientation, please make sure to set your controller to allows both orientation**. The gyroscope may not give you an accurate reading if the device orientation is not supported and the phone is rotated.

![alt tag](https://s3.amazonaws.com/adsoptimal-3dx-assets/manual_upload/wiki/step+1+-+Check+VRPlayer+View.png)

Try to make the VRPlayer fill the full screen by setting the vertical constraint to zero.

![alt tag](https://s3.amazonaws.com/adsoptimal-3dx-assets/manual_upload/wiki/step+2+-+Make+Player+fullscreen.png)

Replace your OmniVirt content ID and insert "player.cardboard = Mode.ON;" inside the playerLoaded() method.

![alt tag](https://s3.amazonaws.com/adsoptimal-3dx-assets/manual_upload/wiki/step+3+-+Turn+cardboard+mode+on.png)

### Result

![alt tag](https://s3.amazonaws.com/adsoptimal-3dx-assets/manual_upload/wiki/cardboard+output.png)

### Example Apps

- [Swift VR Player / Monetization](https://github.com/OmniVirt/iOS-VR-Example/tree/master/Examples/Swift/VRKitExample)
- [Objective-C VR Player / Monetization](https://github.com/OmniVirt/iOS-VR-Example/tree/master/Examples/Objective%20C/VRKitExample)
- [Cardboard QR Code Reader](https://github.com/OmniVirt/iOS-VR-Example/tree/master/Examples/Scan%20QR%20Code/VRKitExample)

# Questions?

Please email us at [contact@omnivirt.com](mailto:contact@omnivirt.com)
