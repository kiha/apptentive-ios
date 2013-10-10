2013-10-09 wooster, pkamb v1.2.1
-------------------------
Fixes:

* IOS-233 "Write a Review" is grayed out when using StoreKit
* #59 'Write a Review' button disabled when app store is shown
* IOS-187 Entering text in one free form field overrides another free form field's data
* IOS-234 Add `distribution_version` to API

This release fixes an issue where iOS 7 disabled the "Write a Review" button on an app page when viewed within StoreKit. For this release, we will be switching back to the URL method of opening the page in the App Store app.

We strongly recommend updating to this version.

2013-10-08 wooster v1.2.0
-------------------------
Fixes:

* IOS-199 Contact info Name field should have word capitalization set
* IOS-200 Suggestion for "singleline" survey question type
* IOS-226 Translations of new strings
* More aggressive about updating person information.

This release also adds a mechanism to require email addresses via server setting.

2013-09-24 wooster v1.1.1
-------------------------
This is a compatibility release for iOS 7.

Fixes:

* IOS-160 Red glow under FeedbackDemo keyboard
* IOS-162 White "Message Center" title bar text can't be seen on iOS 7 white title bars.
* IOS-166 Status bar overlap issues in Message Center "Send a Photo" view
* IOS-167 Tapping Survey text entry cell results in haphazard scrolling
* IOS-171 Text entry for messages should be redone for iOS 7
* IOS-181 App hangs in iOS 7 after "No email Address?" input field alert.
* IOS-183 Unable to attach screenshot on iPad
* IOS-184 After selecting image and pressing done no action sheet is presented
* IOS-190 Survey Description Obscured when Adding Free form Text
* IOS-193 Contact info panel in MC is scrolled down too far
* IOS-194 Message Center doesn't handle rapid keyboard appearing/disappearing
* IOS-195 Handle case where message center is disabled and no valid email address

Other changes:

* Deprecated `useMessageCenter` property in favor of server-based configuration.
* Added debug messages to the rating flow for debugging ratings flow problems.
* Renamed English.lproj to en.lproj to fix Application Loader warning on app submission.
* Made `showTagline` setting work for Apptentive logo on person details screen.

2013-08-29 wooster v1.1.0
-------------------------
This release focuses on support for Enterprise Surveys.

These are mostly changes on the web side of things, but there are also some client changes:

* Moved survey responses into Core Data.
* IOS-119 Implement short v. long survey text response type
* IOS-116 Implement new survey submission endpoint

Other changes for IOS 7 forward compatibility:

* IOS-181 App hangs in iOS 7 after "No email Address?" input field alert.

Other fixes:

* apptentive-ios#45 Renames `ATMessage` to `ATAbstractMessage` because of naming conflict with `AirTraffic.framework`
* We accidentally used the Traditional Chinese localization for both Traditional and Simplified Chinese. This has been fixed.
* Added `useMessageCenter` property on `ATConnect` for those who don't want to use Message Center.

2013-08-18 wooster v1.0.1
-------------------------
Deprecating the `-addCustomData:withKey:` and `-removeCustomDataWithKey:` methods in `ATConnect`.

In their place, use these new methods, which add custom data about devices and people:

```
/*! Adds an additional data field to any feedback sent. object should be an NSDate, NSNumber, or NSString. */
- (void)addCustomPersonData:(NSObject<NSCoding> *)object withKey:(NSString *)key;
- (void)addCustomDeviceData:(NSObject<NSCoding> *)object withKey:(NSString *)key;

/*! Removes an additional data field from the feedback sent. */
- (void)removeCustomPersonDataWithKey:(NSString *)key;
- (void)removeCustomDeviceDataWithKey:(NSString *)key;
```

Also deprecating the `appName` property on `ATAppRatingFlow`. Now, the display name of the application used in our framework can be set server-side.

Per IOS-144 and IOS-145, we now have much better localizations across many more languages.

We have started on iOS 7 compatibility with IOS-157, IOS-159, IOS-164, IOS-168, and IOS-169. We covered some of the major parts, but there's more to come!

Fixes:

* IOS-144 Get incremental updates of localizable strings for Message Center
* IOS-145 Get missing strings from surveys localized
* IOS-149 Don't allow nested key/value pairs for custom data.
* IOS-157 Unread message count not centered in FeedbackDemo
* IOS-159 Spacing between top of email form and the status bar
* IOS-156 Message Center on Original iPad locks to portrait mode
* IOS-164 Message Center background color: white vs. grey
* IOS-168 Attaching photo causes crash on iOS 7
* IOS-169 UITextView metrics changed in iOS 7
* IOS-173 Make client play nicely with location updates and file protection
    * This was a crasher caused when background apps were started before the phone was unlocked.
* IOS-174 Initial email address and name not hooked up to person object
* IOS-175 Add warning if resource bundle isn't found in app
    * If the app isn't properly integrated, and you run it in the Simulator, this will warn you with an alert.
* IOS-176 Select/Copy/Paste menu is broken
* IOS-179 Localization overflow in Message Center feedback form title
* apptentive-ios#44 Doesn't work well in portrait mode on iPad
* apptentive-ios#26 More localizations

2013-06-28 wooster v1.0.0
-------------------------
There are a lot of major API changes. They are documented in docs/APIChanges.md

* Fixes IOS-127 Make some APIs private for Message Center release
* Fixes IOS-129 Simplify SDK API
* Fixes IOS-130 Rename add info API call
* Fixes IOS-128 Remove feedback API for Message Center
* Fixes IOS-103 Make ratings flow easier
* Fixes IOS-136 Create personal info editing screen
* Many, many other changes.

Note that for apps created before June 28, 2013, please contact us to have your account
upgraded to the new Message Center UI on our website. If you have any questions at all,
please let us know!

2013-06-07 wooster v0.4.9
-------------------------
We've finally added support for surveys with tags.

- To check for surveys, call `ATSurveys +(void)checkForAvailableSurveys` as usual.
- Listen for the `ATSurveyNewSurveyAvailableNotification`.
- Check to see if surveys with a given set of tags are available with `ATSurveys +(BOOL)hasSurveyAvailableWithTags:(NSSet *)tags`.
- Display a survey with tags with: `ATSurveys +(void)presentSurveyControllerWithTags:(NSSet *)tags fromViewController:(UIViewController *)viewController`.

Other fixes:

* Fixes IOS-105 Add Russian Localization
    * Thanks to Захаров Дмитрий for the translation!
* Fixes IOS-120 Get localizations for iOS Client strings
* Fixes IOS-63 Implement new client API for surveys (survey tags)
* Fixes IOS-106 Limit connections to 2 at once
    * This prevents a potential problem in situations where the number of connections is limited. See [the problem AFNetworking+TestFlight hit](https://github.com/AFNetworking/AFNetworking/issues/307).
* Fixes IOS-92 Demo app should show a message when the API key is not set
    * This will hopefully be a nice reminder, rather than an irritation.
* Fixes IOS-85 Setting days before re-prompt to 0 doesn't work as expected
    * If this value is 0, we will now only prompt once per update.
* Fixes IOS-84 Re-prompt only once per version
    * We will only prompt twice per update total (prompt and re-prompt).
* Fixes IOS-62 Add support for repeat surveys
* Fixes IOS-99 Add Callback after a user agrees to rate the app
    * You can now listen for `ATAppRatingFlowUserAgreedToRateAppNotification` to know when a user agrees to rate the app.
* apptentive/apptentive-ios#32 Showing the rating dialog from a modal
* IOS-108 Fix for launches not being detected after IOS-76 changes
* IOS-107 Fix warnings in PrefixedJSONKit
* Fixes IOS-124 Surveys with tags shouldn't show up in bare surveys calls
* Fixes IOS-126 Long survey answers are truncated
* Also brings in pull requests #38 and #39.

2013-05-31 wooster v0.4.8a
--------------------------
This is a localization minor bump. There are still a few edge cases in the UI.

Thanks to Robert Lo Bue and Applingua (with help from SpaceInch) for the new localizations!

2013-02-01 wooster v0.4.8
-------------------------
This is a bug fix release.

* Fixes IOS-80 Use StoreKit to show product page when reviewing app
    * Your users on iOS 6 and above will no longer be bounced out of the app to rate your app.
    * To use this, you'll need to link against StoreKit and build with the iOS 6 SDK.
* Fixes IOS-86 Always dismiss keyboard on feedback dialog going away
* Fixes IOS-76 Update launch logic for iOS 4 API (better last use of app metrics for iOS 4+)
* Fixes IOS-83 Distribution build script phase is buggy and runs even when not necessary
* Fixes IOS-72 Find out more button doesn't work in iOS 6
* Fixes IOS-28 Show success message on survey completion when configured
* Fixes IOS-15 Privacy information on info screen
* Fixes [Issue #30](https://github.com/apptentive/apptentive-ios/issues/30) JSONKit warnings in Xcode 4.6
* Fixes IOS-96 Text cut off in screenshot view in landscape
* Fixes IOS-94 Right side of feedback UI doesn't work on iPhone app running on iPad (in landscape)
* Fixes IOS-97 Sending file attachments is writing files to disk a lot
* Fixes IOS-88 Send CP suffix on client version for cocoa pod versions

2012-09-27 wooster v0.4.7
-------------------------
Major change:
* We're dropping armv6 support. This means no more iPhone 3G or iPod Touch 2 support. This is in line with what we're seeing from app developers and other vendors of 3rd party libraries. If you *really* need armv6 support, let us know.

Other changes:

* Fixes IOS-71 Add callback after survey completion
  See the `ATSurveys.h` header for details.
* Added `showTagline` property on `ATConnect`. This allows you to hide the "Powered by Apptentive" logo text.
* Fixes IOS-78 Always send dates in english
  
  This bug was causing some dates to be sent localized to the server. Oops.
* Fixes IOS-79 Allow dev to prompt user to re-rate after new version installed
  
  When the "Reset rating prompt counters when app version changes" settings is enabled, if a user has already rated the app, that will be reset when they upgrade the app. The upshot of this is, users will be prompted to rate the app again after upgrade. You may want to do this if you want users to re-rate the app on a version change, as the iOS App Store is heavily geared towards ratings and reviews for the current version. This change makes our behavior match what developers expect when checking that box on the Apptentive site.
* URL Loading changes:
  * Better cache policy handling, per http://blackpixel.com/blog/1659/caching-and-nsurlconnection/
  * Better URL redirection handling.
* Fixes IOS-39 No option to cancel a photo/screenshot attachment?
  * To cancel a screenshot or photo attachment, just drag it away from the paperclip.


2012-09-11 wooster v0.4.6
-------------------------
One major change in the API:
* The `shouldTakeScreenshot` property of `ATConnect` is now `NO` by default.

Some changes for iOS 6 compatibility:
* Fixes for `viewDidUnload` deprecation (IOS-66 Fixes for deprecated API in iOS 6)
* Retrieves review URL for app store from our server (IOS-64)
* Fixes issue when taking a photo with the iPad camera.

So, due to iOS 6 changing the review URL for opening the App Store and submitting a review, we're now computing this on the server.

Other fixes:
* IOS-60 Respect "cache-expiration" setting returned with configuration
* #23 Modal window closes after feedback (Also logged as IOS-68 Modal Dialog Issue)
* IOS-70 Getting surveys returns 404 on no surveys
* IOS-67 Populate the feedback source field with "enjoyment_dialog" when launched from the ratings prompt
* Changes to `shouldTakeScreenshot` property with existing images attached to feedback work more like one would expect.

Of these, the configuration expiration lets us be less aggressive in retrieving new configurations from the server on startup. #23 fixes a problem in which presenting the feedback dialog from within a modal view controller caused view hierarchy issues with the modal view controller. IOS-70 was, in cases where the app had no surveys, sometimes preventing configuration settings being retrieved from the server. IOS-67 lets us track which pieces of feedback were generated by people saying they don't like the app in the ratings flow.

2012-08-29 wooster v0.4.6
-------------------------
Changes for OS X compatibility:
* Added backing ivars for properties.
* Removed methods for displaying different feedback window types on OS X.

2012-08-29 wooster v0.4.5
-------------------------
Fixes in this version:

* Fixes IOS-65, `[[UIApplication sharedApplication] keyWindow]` being nil after feedback window is dismissed.
* Fixes leak of feedback and custom placeholder text by feedback controller.
* Current feedback is cleared before feedback window is shown by ratings and after that window is dismissed.

2012-08-08 wooster v0.4.4
-------------------------
Major changes:

We switched from JSONKit to our PrefixedJSONKit library, which prefixes all the JSONKit symbols. In this case, our prefix is `AT`. So, we no longer conflict with JSONKit. If you were using JSONKit already and removed it in favor of ours, you'll want to add the original JSONKit back to your project rather than using the PrefixedJSONKit project.

Minor changes:
- Fix for IOS-59, which tweaks how `ATBackend` stops and restarts the task queue.

2012-07-24 wooster v0.4.3
-------------------------
* Fix for IOS-41, wherein the metrics were being sent incorrectly and metric for 
  text responses was being sent after the metric for survey submission.

2012-07-23 wooster v0.4.2
-------------------------
* Fix for [#20](https://github.com/apptentive/apptentive-ios/issues/20), wherein the image picker on iPad would cause the app to crash.

2012-07-22 wooster v0.4.2
-------------------------

* IOS-52: Requests sent before API key is set won't succeed until next app start

	Thanks to [@kgn](https://github.com/kgn) for finding this and [proposing a fix](https://github.com/apptentive/apptentive-ios/pull/19). The fix we've chosen is a
	bit more involved. We are now making each of our various URL requests be handled
	by `ATTask` objects, which can tell the task queue whether or not they're able
	to be executed at the current time. For the case of API requests, that will be
	`NO` until such time as the API key is set.

2012-07-09 wooster v0.4.2
-------------------------
Minor changes:
* Adding Spanish localization courtesy of [Babble-on Inc](http://www.ibabbleon.com/).
* Fixes from [@kgn](https://github.com/kgn) for crash on original iPad and disabled styling on Send button ([pull request 18](https://github.com/apptentive/apptentive-ios/pull/18)).
* IOS-48: Use count is incremented twice at startup, again at location prompt See [a8dedf6abb5b08342aa564ca2a26fcbae80c9d6f](https://github.com/apptentive/apptentive-ios/commit/a8dedf6abb5b08342aa564ca2a26fcbae80c9d6f)


2012-06-25 wooster v0.4.1
-------------------------
Major changes:

The surveys module has been integrated into `ApptentiveConnect` proper, as the survey features are now live for all users on the site. If you have previously added the Surveys module to your app, you will need to update the configuration by removing it from your app and including the `ATSurveys.h` header file.

Minor changes:
* Consistent use of tabs for indents.
* New icons with new Apptentive logo.

2012-06-01 wooster v0.4.0
-------------------------
Major changes:

The metrics module has been integrated into `ApptentiveConnect` proper. Now that you can enable and disable metrics from the website, it didn't make sense to keep them separate.

Bug fixes:
* IOS-40: On debug builds, the configuration is updated much more often to aid debugging. See [df7aa47dce369e6caad8c18ff72b8f9cb0485050](https://github.com/apptentive/apptentive-ios/commit/df7aa47dce369e6caad8c18ff72b8f9cb0485050)
* IOS-41: Added metrics for surveys and for feedback submission. See [e4ce211834737c08b8a5fe9591dffc14b884304f](https://github.com/apptentive/apptentive-ios/commit/e4ce211834737c08b8a5fe9591dffc14b884304f)
* IOS-38: Fixed bug where the paperclip blocked feedback text when there was no email field and no thumbnail. See [f0d7c6e52ee8053653d5ae346ddebb626f9b048e](https://github.com/apptentive/apptentive-ios/commit/f0d7c6e52ee8053653d5ae346ddebb626f9b048e)
* IOS-31: Now sending time to completion of surveys with the response. See [40b1e1e221a0fe60826da2b5ff31877485c72451](https://github.com/apptentive/apptentive-ios/commit/40b1e1e221a0fe60826da2b5ff31877485c72451)
* IOS-42: Should use the localized app name in the ratings flow, if available. See [dc2f59ef5cd347ecc5aa332323d9894092f635e7](https://github.com/apptentive/apptentive-ios/commit/dc2f59ef5cd347ecc5aa332323d9894092f635e7)
* IOS-43: Fixes a bug where sometimes the ratings dialog was not shown at startup due to network reachability. See [717b010ee01bbfd87ee3cca957e7c5bf76d0f648](https://github.com/apptentive/apptentive-ios/commit/717b010ee01bbfd87ee3cca957e7c5bf76d0f648) for more info.
* IOS-36: Fixes bug where the alert view asking for email addresses looks funny in landscape mode. This fix only works on iOS 5+. See [b1aa55dac9b4dc6ae9b10440901129572d271b21](https://github.com/apptentive/apptentive-ios/commit/b1aa55dac9b4dc6ae9b10440901129572d271b21)
* IOS-44: Where screenshots appear too small on Retina display devices. See [7a0d877b523a7f58ba94789bda6ceeebaaff1bd0](https://github.com/apptentive/apptentive-ios/commit/7a0d877b523a7f58ba94789bda6ceeebaaff1bd0)
* IOS-45: In which the application frame wasn't properly taken into account and whitespace appeared in the screenshot under non-default orientations. See [e8a7358f329797812e9d944412bd6708b0d238d4](https://github.com/apptentive/apptentive-ios/commit/e8a7358f329797812e9d944412bd6708b0d238d4)

2012-03-26 wooster v0.3.3
-------------------------

Fixes problem wherein app wouldn't use the correct ratings configuration from the server.

2012-03-25 wooster
------------------
Major changes:

* Start of version 0.3.
* Ratings flow configuration is now done server-side. Old parameters in SDK no longer exist.
* There are now server-side on/off switches for both ratings and metrics.
* Added initial version of surveys.
* Ratings parameter counters (days of use, significant events) can be reset on version upgrade.
* Including armv6 (non-thumb) architecture in all libraries.
* "Distribution" target in FeedbackDemo builds a static library distribution.
* Application exit events wired up in Metrics module.
* Adding `initialName` property to ATConnect for pre-populating the user's name.

##### Metrics
The metrics module can be used by simply linking against the `libApptentiveMetrics.a` static library. That's it. You can turn metrics on or off server side in your app settings.

##### Surveys
This is a very rough initial version of surveys. To use, link against `libApptentiveSurveys.a`.

Specific bug fixes and features:

* IOS-3: App Exit events don't seem to be sent?
* IOS-6: $ARCHS_STANDARD_32_BIT is now armv7 only, needs to be changed to armv6 and armv7
* IOS-11: Surveys Module on iOS
* IOS-21: Support for Server Side Ratings Settings
* IOS-22: Option to clear ratings parameter values (days of use, events, etc.) on version upgrade
* IOS-34: Add support for prepopulating the user's name

2012-01-13 wooster
------------------
* Start of version 0.2.
* Added support for adding and removing extra data to feedback.
* Added initial version of metrics module.
* Added support for optionally showing or hiding the email address field on feedback.
* Added support for setting an initial email address on the feedback form.

To add data to feedback, use these methods on `ATConnect`:

``` objective-c
- (void)addAdditionalInfoToFeedback:(NSObject<NSCoding> *)object withKey:(NSString *)key;
- (void)removeAdditionalInfoFromFeedbackWithKey:(NSString *)key;
```

The data objects should, at this time, either be of type `NSString` or `NSDate`. They will be added to the `record[data]` hash, with the key as the key, as in `record[data][key]`.

If you add the metrics module to your project, it will load on run. It's experimental at this point, so I wouldn't recommend using it quite yet.

You can use these properties to control email field behavior on the feedback form:

``` objective-c
@property (nonatomic, assign) BOOL showEmailField;
@property (nonatomic, retain) NSString *initialEmailAddress;
```

`showEmailField` controls whether or not the email address field is shown on the feedback form. `initialEmailAddress` can be used to set the initial email address that populates the field. Note: if the user submits feedback with a different email address, `initialEmailAddress` will not be used.
