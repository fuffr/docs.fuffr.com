Here is an overview of classes and methods provided by the Fuffr API.

## Class overview

The following classes contain functionality needed by most applications:

Class **FFRTouchManager** ([FuffrLib/FFRTouchManager.h](https://github.com/fuffr/fuffr-ios/blob/master/FuffrLib/FuffrLib/Touch/FFRTouchManager.h)) contains methods for connecting to Fuffr and for observing touch events. This is a singleton, the system creates and maintains the single instance of this class.

Class **FFRTouch** ([FuffrLib/FFRTouch.h](https://github.com/fuffr/fuffr-ios/blob/master/FuffrLib/FuffrLib/Touch/FFRTouch.h)) represents touches, with information like the touch coordinate and which side that generated the event.

Enum **FFRCaseSide** ([FuffrLib/FFRTouch.h](https://github.com/fuffr/fuffr-ios/blob/master/FuffrLib/FuffrLib/Touch/FFRTouch.h)) has constants that represent each side: **FFRSideTop**, **FFRSideBottom**, **FFRSideLeft**, **FFRSideRight**.

## Connecting to the sensor case

The first step in an app is to connect to Fuffr. The app uses BLE (Bluetooth Low Energy) to communicate with Fuffr.

This is how to get a reference to the **FFRTouchManager** and connect:

	FFRTouchManager* manager = [FFRTouchManager sharedManager];

    [manager
        connectToFuffrNotifying: self
        onSuccess: @selector(fuffrConnected)
        onError: nil];

## Registering touch observers

To observe touch events, the application registers methods with the **FFRTouchManager**. Here is an example that registers touch methods for the right side:

    [manager
        addTouchObserver: self
        touchBegan: @selector(touchRightBegan:)
        touchMoved: @selector(touchRightMoved:)
        touchEnded: @selector(touchRightEnded:)
        side: FFRSideRight];

## Receiving touch events

The methods registered to receive touch events takes one parameter, an **NSSet** that contains one or more **FFRTouch** objects. This is an example that logs the normalized coordinates of each touch instance:

    - (void) touchRightBegan: (NSSet*)touches
    {
		for (FFRTouch* touch in touches)
		{
			NSLog(@"Touch norm.x: %.02f norm.y: %.02f",
		        touch.normalizedLocation.x,
		        touch.normalizedLocation.y);
		}
    }
