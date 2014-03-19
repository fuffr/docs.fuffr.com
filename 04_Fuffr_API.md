Here is an overview of classes and methods provided by the Fuffr API.

## Class overview

The following classes contain functionality needed by most applications:

Class **FFRTouchManager** ([FuffrLib/FFRTouchManager.h](https://github.com/fuffr/fuffr-ios/blob/master/FuffrLib/FuffrLib/Touch/FFRTouchManager.h)) contains methods for connecting to the sensor case and for observing touch events. This is a singleton, the system creates and maintains the single instance of this class.

Class **FFRTouch** ([FuffrLib/FFRTouch.h](https://github.com/fuffr/fuffr-ios/blob/master/FuffrLib/FuffrLib/Touch/FFRTouch.h)) represents touches, with information like the touch coordinate and the side of the case that generated the event.

Enum **FFRCaseSide** ([FuffrLib/FFRTouch.h](https://github.com/fuffr/fuffr-ios/blob/master/FuffrLib/FuffrLib/Touch/FFRTouch.h)) has constants that represent the sides of the case: **FFRCaseTop**, **FFRCaseBottom**, **FFRCaseLeft**, **FFRCaseRight**.

## Connecting to the sensor case

The first step in an app is to connect to the sensor case. The app uses BLE (Bluetooth Low Energy) to communicate with the case.

This is how to get a reference to the **FFRTouchManager** and connect to the case:

	FFRTouchManager* manager = [FFRTouchManager sharedManager];

    [manager
        connectToSensorCaseNotifying: self
        onSuccess: @selector(sensorCaseConnected)
        onError: nil];

## Registering touch observers

To observe touch events, the application registers methods with the **FFRTouchManager**. Here is an example that registers touch methods for the right side of the case:

    [manager
        addTouchObserver: self
        touchBegan: @selector(touchRightBegan:)
        touchMoved: @selector(touchRightMoved:)
        touchEnded: @selector(touchRightEnded:)
        side: FFRCaseRight];

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
