---
title: Introduction to Mobile Augmented Reality Development in Unity
authors:
- Jacob W. Greene
date: 2015-01-04
layout: lesson
---

This lesson serves as an introduction to creating mobile augmented reality applications. Augmented reality (AR) can be defined as the overlaying of digital content (images, video, text, sound, etc.) onto physical objects or locations, and it is typically experienced by looking through the camera lens of an electronic device such as a smartphone, tablet, or optical head-mounted display (e.g. Microsoft Hololens). Although AR is a cutting-edge, complex technology, there are a number of user-friendly platforms that allow people with no previous coding experience to create compelling augmented reality experiences. 

## Lesson Goals

In this introductory tutorial, you will learn how to:

* setup the Unity game engine for augmented reality development
* convert images to trackable data sets
* add overlays to trigger images
* modify C# scripts in the Unity editor
* build standalone augmented reality applications to Android and iOS devices

## How can Humanists use Augmented Reality?

Novel applications of AR continue to surface  within a variety of industries: [museums](https://www.youtube.com/watch?v=gx_UQxx54lo) are integrating AR content into their displays, [companies](http://www.gizmag.com/ikea-augmented-reality-catalog-app/28703/) are promoting AR apps in lieu of print or even web-based catalogs, and [engineering firms](https://www.youtube.com/watch?v=bXqe2zSepQ4) are creating AR applications showcasing their efforts to promote sustainability. [Predicted to grow](http://www.digi-capital.com/news/2015/04/augmentedvirtual-reality-to-hit-150-billion-disrupting-mobile-by-2020/#.VbetCU1VhHw) into a $120 billion industry within the next five years, augmented reality is an exciting new medium that humanists cannot afford to ignore. Indeed, many scholars within the growing field of digital humanities are beginning to explore how AR can be utilized as a viable medium of scholarly engagement within public spaces, objects, images, and texts.

{% include figure.html filename="new-ar-dev-1.png" caption="Augmented reality can be used to overlay digital information onto existing texts such as historical markers. This modified image is based on a photograph by Nicholas Henderson." %}

Since at least 2010, [digital artists](https://manifestarblog.wordpress.com/about/) have been creating AR applications for social advocacy and cultural intervention. For example, Tamiko Thiel's AR project [Clouding Green](http://www.tamikothiel.com/AR/clouding-green.html) reveals the carbon footprint of specific technology companies. Projects such as Thiel's capitalize on AR's unique rhetorical affordance to provide compelling, site-specific interactions between physical and digital spaces.

At the [Trace Initiative](http://english.ufl.edu/trace_arcs/), a digital humanities organization in the University of Florida English Department, we seek to build upon the work of these artists by promoting the creation and circulation of humanities-focused mobile AR applications. We released our first AR application [to the Google Play store](https://play.google.com/store/apps/details?id=com.Trace.Dollars&hl=en) in spring 2016.

The augmented reality software used in this tutorial relies on image-recognition technology, meaning that it requires some kind of visual trigger (a logo, painting, etc.) to know when to display digital content. In the example application depicted in the image above, the application is programmed to only display the digital image of John C. Calhoun if the camera "recognizes" the specific historical marker with which it is associated. For this lesson, we will augment the cover of a physical book with a digital overlay that displays a picture of the author. You could use the technical skills gained throughout this tutorial to create digital overlays for a variety of texts such as historical documents or signs. For example, you might create an application that allows readers to scan the pages of a book or document and access historical context or critique related to that specific page. Humanities scholars could also use this tutorial to create site-specific AR applications to educate visitors about cultural aspects of a location that have been excluded from its historical presentation.

## A Note About AR Creation Platforms

Unity is a very powerful and complex application used to create desktop, console, and mobile games. It is not designed exclusively for augmented reality development. As a result, this lesson has many detailed, albeit necessary, steps for navigating and operating the Unity interface. Although some of the steps might not be directly related to augmented reality development, they are certainly transferrable to other tutorials on Programming Historian or elsewhere that utilize Unity. If you would prefer to gain some familiarity with the Unity Editor prior to completing this lesson, I would suggest consulting [Unity's beginner tutorial videos](https://unity3d.com/learn/tutorials/modules/beginner/editor) and the online [Unity manual](http://docs.unity3d.com/Manual/LearningtheInterface.html).

However, before you decide to dive into AR development in the Unity interface, it is important to understand that there are other (much simpler) AR creation platforms available, such as [HP Reveal](https://www.hpreveal.com/). HP Reveal is a simple, drag-and-drop AR creation studio that allows users to augment images with digital content.

{% include figure.html filename="ar-dev-1-16.png" caption="With HP Reveal, you can overlay multimedia content such as videos over the pages of a book." %}

HP Reveal is a fantastic AR creation platform that can be learned fairly quickly. I would highly recommend it for classroom usage and for smaller projects with simple multimedia overlays such as images or short videos. However, online creation platforms like HP Reveal have their limitations. When you create an overlay in HP Reveal, users can only access it through the HP Reveal application. This leaves the AR creator with no control over the design of the application interface. Moreover, HP Reveal requires users to have an internet connection when accessing the application, which makes it difficult to create site-specific AR applications in places where there is little to no internet connectivity. With Vuforia, however, you can create stand-alone AR applications that can be downloaded and stored in the mobile device's memory and thus do not require that users to have internet access. Consult the table below to help you decide which platform is best suited for your AR development needs.

|            | HP Reveal        | Unity/Vuforia    |     
|------------| ------------- |-------------|
| **Type**           | online platform    | computer program |
| **Use**           | small projects with simple overlays     | large projects with complex overlays, site-specific applications |
| **Pros**           | users can instantly access overlays, no coding required    | create standalone applications, more control over interface design, overlays load quickly |
| **Cons**           | file size limits for overlays, requires internet connection     |steeper learning curve, must upload completed application files to Google Play or Apple Store for others to access|
| **Access**           | [HP Reveal Studio](https://www.hpreveal.com/) | [Unity](https://unity3d.com/get-unity/download/archive) [Vuforia](https://developer.vuforia.com) |

## Software Requirements

For this lesson, you will need to download the following software applications and SDKs (software development kits). Several of the applications used in this tutorial (Unity and Android SDK) are very large and will take some time to download and install. You might want to complete the downloads section of this tutorial while working on something else. All of the steps in this lesson can be completed using either the free or paid versions of the software.

* Unity 2017.2 or later
* Java Development Kit
* Android SDK Tools (if testing on an Android device)
* Xcode (if testing on an iOS device)

### Unity

Since the release of Unity 2017.2, the Vuforia SDK is integrated into the Unity Editor. If you are unable to download Unity 2017.2 or later, [consult this archived lesson for earlier versions of Unity](link to previous lesson). To download Unity and Vuforia, go to the [Unity website](https://store.unity.com/download) and download the latest version of the Unity installer. In the "Choose Components" dialog box, make sure to select "Vuforia Augmented Reality Support" in addition to either "Android Build Support" and/or "iOS Build Support," depending on your target mobile device platform. Once the download completes, start Unity and follow the setup prompts. If Unity asks if you are creating a personal or professional account, choose personal account.

{% include figure.html filename="revised-ar-dev-1.png" caption="Check the option for Vuforia Augmented Reality Support." %}

### Java Development Kit

Download and install the [Java Development Kit](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) for your operating system.

{% include figure.html filename="ar-dev-1-9.png" caption="Download the .exe file for your operating system." %}

Click on the file once it has finished downloading, and follow the installation guide. 

### Android SDK Tools (only if testing on an Android device)

There are two options for downloading the Android SDK Tools:

* Download and install [Android Studio](https://developer.android.com/studio/index.html). Android Studio is the official IDE (integrated development environment) for creating Android applications. However, keep in mind that Android Studio is a very large program that will take longer to download, so only take this option if you are interested in developing other mobile applications with Android. If you take this option, follow the instructions in the download assistant.

* Alternatively, you can download just the [Android command line tools](https://developer.android.com/sdk/index.html#Other), which will give you access to the Android SDK but not the Android Studio IDE. if you take this option, scroll down on the Android Studio download page until you see a section labelled "Get just the command line tools." 

{% include figure.html filename="new-ar-dev-27.png" caption="Download the Android command line tools that are compatible with your operating system." %}

Click on the file once it has finished downloading, and follow the installation guide. Start the SDK manager after installation.  Install any packages that are automatically selected, but make sure that the "Android SDK Platform-tools" and "Android SDK Build-tools" options are both selected. Then, scroll down to the folder labelled "Extras" and select the "Android Support Repository" and "Google USB Driver." Click "Install packages."

{% include figure.html filename="ar-dev-1-14.png" caption="Install packages within the Android SDK manager." %}

If you are trying to install the Android packages but keep getting an error about "temp" folders not being created, close the manager and go to the "android-sdk" folder on your computer. Right click the "SDK Manager" application file and select "Run as administrator."

{% include figure.html filename="ar-dev-1-13.png" caption="Start the Android SDK manager." %}

### Xcode

Because Vuforia [no longer supports](https://developer.vuforia.com/forum/unity-extension-technical-discussion/unity-invalid-pbx-project) building Xcode projects with the Windows version of Unity, you cannot test your application on an iOS device if you are working on a Windows computer. In order to build iOS applications with Unity, you need 1) an apple device (iPhone, iPad, etc.) running iOS 9 or later and 2) a Mac running OS X 10.10.5 or later. If you meet these technical requirements, download [Xcode 7 or later](https://itunes.apple.com/us/app/xcode/id497799835?ls=1&mt=12) from the Apple app store. 

## Connect the Android SDK and Java Development Kit to Unity

In Unity, go to "Edit > Preferences > External Tools" and point Unity to the file locations for the Android Tools (Android SDK) and Java Development Kit (JDK) you just installed. If you do not see options for adding the Android SDK and Java SDK, then you will need to close Unity and restart the Unity Download Assistant and make sure that "Android Build Support" is selected on the "Choose Components" page. 

{% include figure.html filename="ar-dev-1-10.png" caption="Restart the Unity Download Assistant." %}

{% include figure.html filename="ar-dev-1-11.png" caption="Check the Android Build Support option. Check the iOS Build Support option if you working on a Mac." %}

Unity should automatically detect the location of the Java Development Kit once it has finished installing. If it does not, restart Unity and go to "Edit > Preferences." Select the "External Tools" and make sure that the "JDK" field is pointing to the Java Development Kit. Click the "Browse" button next to the JDK field and select the "jdk[version number]" folder in the "C:/Program Files/Java" folder. Leave the "NDK" field blank. 

In the External Tools dialogue box in Unity, click the "Browse" button next to the "SDK" field and point it to the "android-sdk" folder on your computer. If you downloaded the SDK through the Android Studio IDE, this folder will be located in "C:/Program Files/Android" folder. If you downloaded just the command line tools, it will be in this folder: "C:/Users/[your username]/AppData/Local/Android."

{% include figure.html filename="new-ar-dev-29.png" caption="Connect the Android SDK Tools and the Java Development Kit to your Unity project." %}

If you do not see the "AppData" folder, open your file explorer and select the "View" option in the top menu. Select the box labelled "Hidden items." 

{% include figure.html filename="ar-dev-28.png" caption="Check the 'Hidden items' box in your file explorer View options." %}
  
## Navigating the Unity Interface

This section covers some of the basic knowledge you will need while working with the Unity Editor. If you are already familiar with the Unity Interface, feel free to skip down to "Setting up Unity for AR Development."

Open Unity and create a new project. Select the "Window" option in the top menu and go to "Layouts". Select the "Default" layout option. Starting from the upper left and moving clockwise, you should see four panels labelled "Hierarchy," "Scene," "Inspector," and "Project."

{% include figure.html filename="ar-dev-2.png" caption="Default layout of the Unity interface." %}

First, navigate to the "Hierarchy" panel in the upper left. Your hierarchy panel should have a "Main Camera" and "Directional Light" included by default. If there is nothing in your hierarchy panel, select the "Create" drop-down menu directly above the panel and add a "Light > Directional Light." You do not need a "Main Camera" in your panel, but if it is already there, you can leave it.

Items that appear in the hierarchy panel are referred to as "game objects," and any game objects listed in the hierarchy panel are visually represented in the scene panel. Notice how the "Directional Light" appears in the scene panel as a sun and camera icon. To locate the position of a game object within your scene, select it in the hierarchy panel, place your cursor within the scene panel, and then strike the "F" key on your keyboard.

{% include figure.html filename="ar-dev-1-1.png" caption="The game objects in your hierarchy panel are represented visually in the scene panel." %}

In Unity, a game object is a container for different components that can be added and modified in the inspector panel. Select the "Directional Light" game object in your hierarchy panel. You should now see the properties of the Directional Light in the inspector panel on the far right. The inspector panel contains all of the "components" attached to a game object. The Directional Light game object has two components: "Transform" and "Light." You can add and modify components to change the appearance and functionality of your game objects. 

{% include figure.html filename="ar-dev-1-2.png" caption="Use the inspector panel to modify the components of individual game objects." %}

Navigate to the bottom of the Unity interface where you will find a panel labelled "Project." The project panel gives you easy access to the entire file structure of your Unity project. You can access all of the media, scenes, and scripts for your project through this panel. If you use Unity to create more complex applications, you will want to organize your project with different folders to hold all of your images, scenes, sounds files, etc. You should also see a "Console" tab located next to the "Project" panel. The console panel will display any errors or warnings in your project.

## Setting up Unity for AR Development

For your AR application, you will not need the Main Camera or Directional Light game objects. Select them both, right click (or Ctrl click), and select "Delete."

Navigate to the "GameObject" dropdown menu and select "Vuforia > AR Camera." If a dialog box appears requesting that you import additional assets, select "Import."

{% include figure.html filename="revosed-ar-dev-2.png" caption="Add Vuforia's custom AR Camera to your project." %}

Next, add an Image Target to your scene by selecting "Vuforia > Image" in the GameObject dropdown menu. Locate the directional widget in the top right corner of your scene panel. You can use this to adjust the view of your scene panel to the x, y, or z axis. Click the green y-axis option of your directional widget. This will make the green arrow  disappear and shift your perspective in the scene panel to a y-axis "birds-eye" view of your project. It will now be easier to manipulate the game objects in your scene view. 

{% include figure.html filename="ar-dev-1-4.png" caption="Click the green y-axis option of your directional widget." %}f

Select the ImageTarget game object in the hierarchy panel and strike the "F" key while your cursor is within the scene view window. This should bring your ImageTarget game object within the viewport of your scene panel. If you still can't see your ImageTarget in the scene view, make sure that the "2D" option is deselected in the scene view options menu.

{% include figure.html filename="revised-ar-dev-3.png" caption="Vuforia automatically includes a sample Image Target but we will change it in the next step." %}

Next, go to the [Vuforia developer portal](https://developer.vuforia.com/) and create a new account by selecting "Register" in the upper right corner. Once your account is setup, select "Develop" in the menu panel and then "License Manager." Select "Get Development Key" on the License Manager page. On the "Add a free Development License Key" page, give your application a name and agree to the terms.

{% include figure.html filename="revised-ar-dev-4.png" caption="Add development license key page." %}

This license key grants your application access to Vuforia's augmented reality SDK. However, we still need to connect the license key to your Unity project. To access your license key, return to the "License Manager" page in the Vuforia developer portal and click on the application name you just created. Copy the alphanumeric string in the gray box.

{% include figure.html filename="revised-ar-dev-5.png" caption="Copy the license key." %}

Return to Unity and select the "AR Camera" game object in the hierarchy panel. Navigate to the Inspector panel, where you might see a warning triangle in the "Vuforia Behavious (Script)" component telling you that Vuforia is not enabled. To resolve this, Go to "File > Build Settings" and click on the "Player Settings" button in the bottom of the pop up window. Navigate back to the Inspector panel and click on the "XR Settings" option located at the bottom of the accordion menu. Select "Vuforia Augmented Reality Support." 

{% include figure.html filename="revised-ar-dev-6.png" caption="Enable Vuforia support." %}

Reselect "ARCamera" GameObject in the Hierarchy panel. In the inspector panel, click on the "Open Vuforia Configuration" button in the "Vuforia Behavious (Script)" component. Copy and past your license key in the "App License Key" text field.

{% include figure.html filename="revised-ar-dev-7.png" caption="Copy and paste your app license key." %}

Once your license key has been added to the project, got to "File > Save Scene as..." and give your scene a name. By default, Unity will save your scenes to the "Assets" folder of your project. Feel free to leave your scene file here for now; however, for projects with more than one scene, you should create a dedicated folder to hold your scene files. To create a new folder, navigate to the "Project" panel in the lower left of the Unity editor. Right-click on the "Assets" folder and choose "Create > Folder." Give the folder a name (e.g. "Scenes"), then drag and drop your scene file into this folder.

{% include figure.html filename="ar-dev-9.png" caption="Create a dedicated 'scenes' folder for your Unity scene files." %}

## Convert your Image Target to a Dataset

For this section of the lesson, you will need a .jpg or .png image of the cover of the book. You can either take a picture of a book cover around your house or office or you can do an image search for the book cover online. In either case, make sure that you have access to a physical copy of the book.

When selecting a book cover to augment, make sure that it has stark color contrasts and a variety of complex shapes. Using a visually complex image makes it easier for your device's camera to track the Image Target for your application.

{% include figure.html filename="ar-dev-10.png" caption="This cover of John Steinbeck's *Of Mice and Men* will work well as an Image Target." %}

This cover of *Of Mice and Men* has sufficient visual complexity; however, it is not unique, and if it is used as an image target, then any copy of the book will work as an image target. Of course, this ubiquitous quality of the image might be desirable. For instance, digital artist Mark Skwarek augmented the British Petroleum logo to critique BP's complicity in the Gulf oil spill. Because the digital overlay is accessible wherever a BP logo can be scanned, Skwarek's project operates as a ubiquitous reminder of our dependence on fossil fuels.

{% include figure.html filename="ar-dev-11.png" caption="Photo courtesy of Mark Skwarek." %}

If you are taking a picture of your book cover, make sure that there are no extraneous features present in the image. In the case of the *Of Mice and Men* image above, this would be anything beyond the edge of the cover. If your image contains such extraneous features, either take another picture or open it in a photo editor such as [Gimp](http://www.gimp.org/) and
crop out these features. [Consult this video tutorial](https://www.youtube.com/watch?v=2rGGpOTSpbc) for help on cropping and resizing images in Gimp. Make sure that your image file is under 2.5 mb and that it is a .jpg or .png file.

{% include figure.html filename="ar-dev-12.png" caption="Crop out the area around the book." %}

Next, you will need to upload your book cover to Vuforia in order to code it with tracking information. Go to the [Vuforia developer portal](https://developer.vuforia.com/) and click on "Develop" in the top menu and then select "Target Manager." Next, click on the "Add Database" button on the Target Manager page. In the dialog box that appears, give your database a name and select the "Device" option. Click "Create."

{% include figure.html filename="ar-dev-13.png" caption="Name your Image Target Database." %}

Once your database has been created, return to the "Target Manager" page and click on your database. Click on the "Add Target" button. In the "Add Target" dialog box, choose "Single Image" as the type and upload your trigger image by clicking on the "Browse..." button.

{% include figure.html filename="ar-dev-14.png" caption="Image Target upload options" %}

To determine the width of your image, right-click the image file and choose "Properties." Select the "Details" tab in the dialog box that appears and scroll down to the "Image" section to find the width of the image in pixels. If you're using a Mac, Ctrl click and select "Get Info." The first number is the image's width.

{% include figure.html filename="ar-dev-15.png" caption="Properties dialog box" %}

Click "Add" in the "Add Target" options box on the Vuforia developer portal. Once your image has been processed, Vuforia will give it a feature tracking rating on a scale of 1 to 5 stars. Navigate to the Image Targets database in the Vuforia Developer Portal and select the image you just uploaded. Click on the "Show Features" link to reveal the image's trackable features.

{% include figure.html filename="ar-dev-16.png" caption="Vuforia's augmentability rating for the book cover." %}

The yellow markers represent the areas in the image that your application will use to determine if it is looking at the proper image target. If you notice that Vuforia is tracking unstable elements in your image (e.g. shadow, person, etc.), then you will need to re-edit or choose a different image. 

If your image is given a good augmentability rating (anything between 2-5 stars should work), select your image and click "Download Database." If you were creating an AR application with multiple Image Targets, you would want to convert all of your images through Vuforia's developer portal before downloading them as a Unity package.

{% include figure.html filename="ar-dev-1-3.png" caption="Select the 'Download Database' button in the top right." %}

In the dialogue box that pops up, select "Unity Editor." Click "Download" and save the Unity package to an appropriate location.

{% include figure.html filename="ar-dev-17.png" caption="Download your Image Target Database" %}

## Import the Image Target 
 
Now that you have converted your image into an image target, you need to associate it with your ImageTarget game object in Unity. Double click on the "Unity Package" file you downloaded in the last step. Unity will automatically import the file.

Once the database has been imported, select the ImageTarget GameObject in the project hierarchy panel. Navigate to the inspector panel and select the drop-down menu of the "Database" parameter in the "Image Target Behaviour." Select the name of the database you created earlier. The ImageTarget game object should now be associated with your book cover. 

{% include figure.html filename="ar-dev-18.png" caption="Image Target" %}

Zoom into your Image Target game object by selecting it in the hierarchy panel and striking the "F" key with your cursor hovering over the scene panel. If your scene view does not look like something similar to the image above, click on the green y-axis in the directional widget of your scene panel. 

Next, select the "ARCamera" object and return to the Vuforia Configuration option in the inspector panel. In the "Databases" section, check the "Load Database" and "Activate" parameters for your Image Target Database. The AR camera will not recognize your image target unless both of these boxes are selected, so make you check them first when troubleshooting your application.

{% include figure.html filename="revised-ar-dev-8.png" caption="Load and activate the Image Target Database." %}

## Add an Image Overlay

You will need to add an overlay to test if your AR camera is tracking the image. The overlay is the multimedia content that your application will superimpose onto your trigger image. In Unity, you can add images, videos, audio files, and animated 3D models as overlays. For this lesson, however, we will only be covering image overlays.

First, find an image that you want to use as an overlay. If your application is augmenting a book, then you might download an image of the author but feel free to use a different image. In either case, drag the image into the "Assets" folder in the project panel at the bottom of the editor. Once the image has finished importing, select it and change its Texture Type to "Sprite (2D and UI)" in the inspector panel. Click "Apply."

{% include figure.html filename="ar-dev-20.png" caption="Convert overlay image to a sprite" %}

Next, drag the sprite you just imported onto your "Image Target" game object in the project hierarchy. 

{% include figure.html filename="ar-dev-1.gif" caption="Attach your author image as a child of your ImageTarget game object." %}

The sprite is now a "child" of the Image Target game object and will only appear if the ARCamera recognizes the Image Target.

The position of your image overlay (the author image) in the scene view is the same position that it will appear when scanned with a mobile device camera. For example, if you place the author image at the top of the book then it will also appear at the top of the book cover when your user scans it. 

Next, you will need to adjust the size and position of your author image to center it on your book cover using the translate, scale, and rotate tools located in the upper left of the Unity editor interface. Use the instructions for each of these tools below until your author image is positioned on top of your book cover. Remember to use the "F" key to locate your overlay or image target within the scene view.

To move the author image, select the "translate" tool from the button-menu directly above the hierarchy panel. Then, select the author image in your hierarchy panel. You can now move your author image in the x, y, or z axis by clicking on dragging on the red, blue, or green arrows. Use the green y-axis arrow to position your author image slightly above the book cover. Your overlay should have a slightly higher y-axis value (only about .1 or .2) than your Image Target. You can check these values in the "Transform > Position" component in your inspector panel.

{% include figure.html filename="ar-dev-2.gif" caption="Use the Translate tool to move game objects in your scene view." %}

To resize the author image, select the "scale" tool and adjust the width and height proportionally by clicking and dragging on the white cube in the center of the image.

{% include figure.html filename="ar-dev-3.gif" caption="Use the scale tool to resize game objects in your scene view." %}

To rotate the author image, select the "rotate" tool and adjust the image by clicking and dragging on the red, blue, or green circle. Alternatively, you can set the "x" axis to "90" in the image's "Transform" component to the right.

{% include figure.html filename="ar-dev-4.gif" caption="Use the Rotate tool to rotate game objects in your scene view." %}

To adjust your perspective in 3D space, hold the Alt button (Option on Mac) on your keyboard and click and drag in the scene view. Then, select the translate tool and position your author image so it is in front of the book cover.

{% include figure.html filename="ar-dev-5.gif" caption="Position your author image on top of the book cover." %}

Because Unity is optimized for 3D environments, it is sometimes difficult to work with 2D game objects such as images. If you are new to Unity, do not be alarmed if you cannot find your images or if you feel disoriented while manipulating them in your scene view. If you want to learn more about using Unity's transform tools, I would suggest checking out [this short video tutorial by Info Gamer](https://www.youtube.com/watch?v=2Ariq8vc5Vc) and reading up on [Transforms in the Unity Manual](http://docs.unity3d.com/Manual/Transforms.html).

If you cannot find your author image in the scene view, try the following steps:

* Select the author image in the hierarchy panel and navigate to its "Transform" component in the inspector panel. Click on the small cog icon in the upper right corner of the "Transform" component and select "Reset."
* Use the "F" key to search for any game object. Make sure the game object you are searching for is selected in the hierarchy panel and that your cursor is within the bounds of the scene view.
* Select the hand tool (left-most option) in the transform menu and adjust your perspective in the scene view. Hold the Alt/Option button on your keyboard to adjust your perspective in 3D space. 
* Use the translate, scale, and rotate tools described above to reposition your author image on top of the book cover.

{% include figure.html filename="ar-dev-22.png" caption="Reset the position, rotation, and scale of a game object in the Transform component." %}

## Create a Simple User Interface

It is helfpul to create a simple user interface (UI) that directs the user to the correct book cover they need to scan. To do this, you will first need to import a .jpg or .png file of your target image into your Assets folder. You can do this by simply clicking and dragging the image file from its current file location into the Unity Assets folder. Once the image is imported, make sure to convert it to "Sprite (2D and UI)" in the inspector panel like you did for the author image overlay.

Next, navigate to the hierarchy panel and select "Create > UI > Image." Select the "2D" option in your scene view menu and center the image you just added by selecting it and clicking "F" on your keyboard. Click and drag the blue corners to center the image in your Canvas frame. Then, drag your book cover into the "Source Image" parameter in the inspector panel.

![](images/revised-ar-dev-10.gif)

Next, add some instructions to your UI by selecting "Create > UI > Text." In the inspector panel, write some instructions in the text field, such as "Scan this Image." Position your text box directly below your book cover and modify the font and color accordingly.

{% include figure.html filename="revised-ar-dev-11.gif" caption="Position the UI instructions directly below the book cover." %}

Before you can add functionality to the UI, you will need to combine your Canvas elements into a single game object. Do this by selecting "Create > Create Empty." This will add an empty GameObject to your project hierarchy. Rename this GameObject "Finder" and make it a child of the Canvas by dragging it into the Canvas game object. Then, drag the Image and Text game objects and make them children of your new "finder" game object.

{% include figure.html filename="revised-ar-dev-12.gif" caption="Create a finder game object to hold your Image and Text game objects." %}

For this next step of the UI design, you will need to modify Vuforia's "Default Trackable Event Handler" so that your "finder" game object disappears from the user's view once the Image Target has been found by the application. To open the C# script you will need to modify, click on the "ImageTarget" game object in the hierarchy panel and then double click on the "DefaultTrackableEventHandler" in the inspector panel. This will open the script in Unity's default IDE (Monodevelop) where you can add additional functionality to your AR application.

First, we need to create a public game object to store the "finder" game object we just created in the previous step. Navigate to the section of the script labelled "#region PRIVATE_MEMBER_VARIABLES" and write the following script:

<!--not javascript but markdown doesn't appear to have highlighting enabled for C#-->

```javascript
public GameObject finder;
```
Save your changes. This will create a public game object variable in Unity. 

% include figure.html filename="revised-ar-dev-13.gif" caption="Create a public finder variable in your Default Trackable Event Handler script." %}

Next, you need to return to Unity and associate the finder game object in your hierarchy panel with the public variable in your C# script. Do this by clicking and dragging the "finder" game object into the public variable slot now available in your ImageTarget's "Default Trackable Event Handler" component in the inspector panel.

% include figure.html filename="revised-ar-dev-14.gif" caption="Link your finder game object with your finder variable." %}

Next, press control (or command) "F" and search for "protected virtual void OnTrackingFound()." This will take you to the OnTrackingFound method, which contains a series of actions that the application will execute if the target image is currently being "tracked" by the user's camera. At the end of the "OnTrackingFound" method, add the following script:

```javascript
finder.SetActive (false);
```

This tells the application to disable the "finder" game object whenever the target image is currently being tracked. Next, scroll down to the "OnTrackingLost" method and add the following script:

```javascript
finder.SetActive (true);
```

This tells the application to enable the finder game object if the target image is lost.

% include figure.html filename="revised-ar-dev-15.gif" caption="Disable the finder game object when your target image is being tracked and enable the finder game object when it is lost." %}

## Test Your Scene

If you do not have a webcam on your computer, skip to the section "Building Your Application to a Mobile Device."

To test your application, save your scene and press the play icon in the menu above the scene view. Give Unity permission to access your webcam, and return to the scene view by clicking on the "Scene" tab to the left of the "Game" tab. Hold your book cover in front of your webcam. You should see your UI overlaid onto the camera view. Place your book cover into the camera view and the author image should appear overlaid on top of it.

{% include figure.html filename="revised-ar-dev-16.gif" caption="Place your book cover within the webcam view while in play mode." %}

If your overlay does not appear, double check the "Open Vuforia Configuration" component of your "AR Camera" game object to ensure that the "Load Data Set" and "Activate" boxes are both selected for your Image Target database.

## Building Your Application to a Mobile Device

### Android

Before you can install your own applications on your Android device, you will need to [enable USB debugging](http://developer.android.com/tools/device.html). To do this, go to "Setting" > About Device" and tap the "Build number" seven times. Return to the previous screen and you should now see a "Developer Options" tab. Click it and make sure the option for "USB debugging" is checked.

{% include figure.html filename="ar-dev-25.png" caption="Tap the 'Build Number' seven times." %}

{% include figure.html filename="ar-dev-26.png" caption="Make sure that 'USB Debugging' is enabled." %}

In Unity, go to "File > Build Settings." In the "Platform" section of the dialog box, select "Android" and click "Switch Platform." Then, select "Add Current" (or "Add Open Scenes").

{% include figure.html filename="ar-dev-30.png" caption="Build Settings dialog box" %}

Click on "Player Settings" and navigate to the inspector panel. Change the "Product Name" to the name you want to use for your app (e.g. "Programming Historian Demo"). Scroll down in the inspector panel and select the "Other Settings" tab. Change the "Bundle Identifier" settings from "com.Company.ProductName" to a name that will be unique to your application, such as "com.Demo.Steinbeck".

{% include figure.html filename="ar-dev-31.png" caption="Change the 'Bundle Identifier' of your application in the Inspector Panel" %}

You are now ready to build your application to your mobile device. Connect your device to your computer with a USB cable. Depending on your operating system, your computer might need to download additional drivers in order to interact with your mobile device. Your computer should do this automatically. If the computer is not recognizing your device, follow the first step in the troubleshooting guide below.

In the "Build Settings" window, make sure your scene is listed and click "Build and Run." Unity will create a ".apk" (Android Application Package) file for your project. By default, your .apk file will be saved to the root folder of your Unity project. This is the file type that will be uploaded to the Google Play store once your application is complete.

When the application is finished building, you should be able to view and test your application on your Android device.

{% include figure.html filename="ar-dev-32.png" caption="Testing the application on an Android device." %}

With Android, it is very easy to share and test your completed application with other Android users without uploading it to the Google Play store. To share your application, simply send the .apk file as an email attachment to anyone with an Android device. However, before other users can download and install the .apk file, they will need to allow their Android device to install .apk files from non-Google Play sources by navigating to "Settings > Security" on their Android device and checking the box labelled "Unknown sources."

### Troubleshooting Android Builds

During the build, if you get an error from Unity saying that it cannot locate your android device, try the following in order:

* Open the device manager on your computer and right click on the Android phone attached as a device. Select "Update Driver Software."
* Open the Android SDK manager and ensure that the "Google USB Driver" is installed.
* Unplug your device from the computer. Open the "Developer Options" in the system setting of your Android device. Select the option to "Revoke USB Debugging Authorization." Plug your device back into your computer.
* Save your scene and close Unity.
* Open your file explorer and go into the "android-sdk/platform-tools" folder. Hold shift and right-click. Select the option to "Open command window here." For Mac, open a Terminal and drag the "platform-tools" folder into the window.

Type the following commands and press "Enter" after each. As you enter each command, check your Android device and authorize your computer when prompted.

```
adb kill-server
adb start-server
adb devices
```

{% include figure.html filename="ar-dev-1-15.png" caption="Once your device is authorized, the command prompt should display 'List of devices attached' along with an alpha-numeric string that represents your Android device." %}

If you are getting errors that your "Android Build Tools" are out of date, open the Android SDK manager and make sure that the "Android SDK Platform-tools" and "Android SDK Build-tools" options are both installed.

If you get an error saying that "Unity cannot install the APK!" go to your player settings and set the "Install Location" to "Automatic."

### iOS

Before you can build your application to an iOS device, you will need to create an XCode project in Unity. First, go to "File > Build Settings" and switch your platform target to "iOS." Click on "Player Settings" and navigate to the inspector panel. Change the "Product Name" to the name you want to use for your app (e.g. "Programming Historian Demo"). Scroll down in the inspector panel and select the "Other Settings" tab. Change the "Bundle Identifier" settings from "com.Company.ProductName" to a name that will be unique to your application, such as "com.Demo.Steinbeck".

iOS applications also require a camera usage description to be set for all apps that require access to the camera. Click on "Player Settings..." and expand the option labelled "Other Settings." Add a description in the text field labelled "Camera Usage Description" (e.g. "This app requires access to your device camera."). Next, set the "Target Minimum iOS Version" to 9.0. Click "Build" and name the project "ProgrammingHistorianLessonXcodeBuild."

Open Xcode and select "Open another project" and navigate to the Xcode project you just built in Unity. Open your project in Xcode. If Xcode asks if you would like to update your project to the recommended settings, select "perform changes" and wait for the project to update.

Next, you will need to register your iOS device with Xcode. First, connect it to your computer with a USB cable.  You might have to wait a few minutes while Xcode prepares your device for app development. In order to build your app to an iOS device, you will need to link your apple account to Xcode. Click on "Xcode > Preferences" and choose the "Accounts" tab. Sign in using the same Apple ID associated with the iOS device you will be building the app to.

Next, switch over to the "Unity-iPhone" targets menu and click on the tab labelled "General." Make sure that "Automatically manage signing" is selected and switch your "Team" to the Apple ID account you just added. In "Deployment Info" select either iPhone or iPad depending on your target build device. 

{% include figure.html filename="revised-ar-dev-17.png" caption="Switch over to the "Unity-iPhone" targets menu." %}

Finally, select "Product > Run" in the top menu and wait for your app to build to your iOS device. Once the app has finished building, you will need to authorize your Apple ID as a trusted developer. Go to the settings on your iOS device and click "General > Device Management" and choose the option for "Trust [Your Apple ID username]." Start the application by clicking on the application icon on your app home screen.

## Extending the Tutorial

You should now have a fairly good grasp of how the Unity game engine can be used to create a simple augmented reality application. In future tutorials, we will cover more advanced topics that will provide you with the necessary technical skills to create more robust mobile AR applications with dynamic, interactive overlays.