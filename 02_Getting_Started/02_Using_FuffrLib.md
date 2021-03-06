**You only need to read the following if you wish to use Fuffr with your existing apps. The examples that come with Fuffr are already set up properly.**

**FuffrLib** is an Xcode library you can add to your own iOS applications to Fuffr enable them.

Note that the example apps already are set up to use FuffrLib. You can just run them out-of-the-box.

To include FuffrLib into your own apps (existing or new ones you create from scratch), follow these steps:

1. Open your application in Xcode.

Make sure that no other application that includes FuffrLib is open in Xcode.

2. From the Finder, drag and drop the file **FuffrLib.xcodeproj** into the Xcode Project Navigator.

3. Select your project (the topmost entry) in the Project Navigator and select tab **Build Settings**.

4. Under **Search Paths/Header Search Paths**, enter the following in the Debug and Release fields (make sure to include also the quote marks):

    "$(TARGET\_BUILD\_DIR)/usr/local/lib/include" "$(OBJROOT)/UninstalledProducts/include" "$(BUILT\_PRODUCTS\_DIR)"

5. Under **Linking/Other Linker Flags**, enter the following in the Debug and Release fields:

    -ObjC

6. Next select tab **Build Phases**.

7. Under **Target Dependencies**, click **+** (plus) and add **FuffrLib**.

8. Under **Link Binary With Libraries**, click **+** (plus) and add **libFuffrLib.a**.

For more information about using libraries, see the [iOS Developer Library Documentation](https://developer.apple.com/library/ios/technotes/iOSStaticLibraries/Articles/configuration.html#//apple_ref/doc/uid/TP40012554-CH3-SW1).
