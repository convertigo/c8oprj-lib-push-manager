# c8oprj-lib-push-manager
This is the Firebase Cloud Messing Push notifcations library for Convertigo platform.

# Usage
This library brings the server part and the client part for Firebase Push Notifications support for Convertigo mobile builder apps. 

## Setting up the Firebase Service

1. Connect to the firebase console : [https://console.firebase.google.com/](https://console.firebase.google.com/)
2. Sign in with your google account and add a project by click on the "+" (add project)
3. Give a project name, hit "Continue", Disable or enable google Analytics and hit "Continue"
4. Wait for the resources to be provisioned, Hit "Continue", you will be on the firebase overview page
5. Click on the Gear icon next to "Projet Overview" -> "Project settings" to configure your Firebase  project
6. Add your iOS and Android app by clicking on the iOS or Android icons. When you add your apps be sure to configure a valid bundle id (iOS) or Android package name (Android) and use the same ids for both platforms, for example __"com.mycompany.myapp"__. The id configured here will be used later on to configure the __MobileApplication__ object in Convertigo project.
7. Download the config files, this will be the __google-services.json__ (Android) or the __GoogleService-info.plist__ (iOS). These files will have to be included in your app and described in the next section.
8. You can ignore next steps for Convertigo Mobile Builder applications.

## Getting your server key

Firebase services automatically generated a Server key. You will need it to Configure the Convertigo Push manager Library. To get your server key :

1. In the project settings, click on the "Cloud Messaging" tab.
2. Copy the "Server Key" as you you will have to configure it in a Convertigo global Symbol.

## Configure your iOS APNS notifications (Only if you want to do iOS notifications)

FCM supports APNS notification for iOS. You will have to configure your APNS Auth key. This is done in the "Cloud Messenging' tab under the "iOS app configuration" section (The section will be shown only if you added an iOS app to your FCM project). To get you APNS Auth key, you need and Apple developper account and connect to :  

[https://developer.apple.com/account/resources/authkeys/add](https://developer.apple.com/account/resources/authkeys/add)

Add a APNS key, give it a name and be sure to know your team id (shown in upper right corner of the apple developper portal)

Once the key is generated, download the .P8 file, and upload it in the FCM "iOS app configuration" section with its name and the TEAM ID.

## Client Part configuration

The library provides a __FCMPushNotifications__ Convertigo Shared action you must add in your client application. To do so :

1. In your Mobile Builder application add a [Project Reference](https://www.convertigo.com/documentation/latest/reference-manual/convertigo-objects/common/references/schema-references/project-reference/) (Right click on the Convertigo project root and new->Reference->Project reference). Choose any template as it will be edited in the next step.
2. On the project reference property click on the __"Project name and remote URL"__ property '...' to edit the property
3. Paste in the "Project Remote URL" field this reference :

		lib_PushManager=https://github.com/convertigo/c8oprj-lib-push-manager.git
 
	  
	The library will be downloaded from github and installed in your Convertigo workspace.
4. Now invoke the shared action in your client app to register and start receiving push notifications.

## Client part usage

the __FCMPushNotifications__ shared action has a __Topics__ shared variable you can use register FCM notifications on a list of topics. By default, the topic list is empty but you can use there an array of FCM topics you want to be notified on.

You can receive FCM events by using a [Subscribe Handler](https://www.convertigo.com/documentation/latest/reference-manual/convertigo-objects/mobile-application/components/control-components/subscribe-handler/) on the "FCM" vent topic property. You will receive FCM events with this data structure :

		{
			type: "data" or "token" (If token the data field is the token),
			data: {
				wasTapped:false if received in backgound, true otherwise,
		        property1: value1,
		        property2: value2,
				...
		        propertyn: valuen,
				body: "The push notification payload"
			}
		}					   
       
## Server part Configuration

## Server part usage
