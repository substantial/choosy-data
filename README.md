Choosy
======

Effortlessly enable your users to choose default apps for external actions without writing any app-specific code. 

Why? When widely implemented by developers, users will be able to traverse iOS using the apps they love, which may or may not include default iOS apps. There are more benefits possible, but this is the main goal. 

A picture is worth... 
==================

Interactions: 
A tap shows an activity sheet-like view that shows installed apps for a given app type (Browser, Navigation, Email, Twitter, etc.) and lets the end user select their favorite app.
A long-press resets the default and asks the user to select a favorite app again.
If the app user designated as default is deleted, the choices are presented again.
If a new app of same type is installed (such as a new Twitter client), the choices are presented again.

Imagine: 
No Choosy: your WebView has 'Open in Safari' button, but your user loves Chrome. *wishful and slightly sad user face* 
Choosy: your button says 'Open in Browser'. When the button is tapped, Choosy displays a list of installed browsers. Once a browser is selected, the button always sends user to that browser. (You can even query Choosy to return default app for category or category name if no default, and append that to button's title. So it would be 'Open in Browser' to start with, but 'Open in Chrome' if Chrome is selected for the default.) *pleasantly surprised and excited user face*

No Choosy: your About screen has Email Us link, but your user loves Mailbox. *sound of a quiet sigh from user* 
Choosy: User is asked for their favorite email client when they tap the Email Us link. *sound of a great review being written*

How is this possible?
====================

iOS allows us to check if any app responds to a given URL scheme. We compile a list of apps and their URL schemes on the server, and then categorize the apps. When tell Choosy you want Twitter apps, it grabs the list of apps from the server and then checks if anything responds to each app's base URL scheme. If the answer is yes, we know the user has that app installed (b/c only one app can be registered with the same URL scheme on a device)! We then take the parameters you passed to Choosy and build an app-specific URL depending on which app user selected as their favorite.

Choosy abstracts all of this, though, so you can support all apps without having a single app-specific line of code. It uses caching and works in the background, so the network traffic is negligible and the main thread is not blocked.

How easy to implement?
=====================
Very. You have two options.

Easiest: 
-------
1. Register qualifying UIControls with Choosy like this:

[SBChoosyRegister registerUIElement:myButton forAction:[SBChoosyActionContext initWithAppType:@"Twitter"]];

That's it! Choosy will hook up a tap and long press gesture recognizers to that button (can be any UIControl) and do all the magic for you. 

PS: Yes! We have more initWith... methods that let you describe specific actions (like "Compose Tweet") and pass parameters (like "text").

Easier: 
------
1. Add your own gesture recognizers and call Choosy as appropriate. (We strongly recommend following the tap+long press theme, if at all possible given your UX.) 

2. In your viewDidLoad or similar, call: 

[SBChoosy registerAppTypes:@[@"Twitter", @"Browser", @"Mail", ...]]

// Prepare means: pre-load data about apps that are in those registered app categories, including any new app icons, in the background.
[SBChoosy prepare]; 

NOTE: Since it's a background operation, you can also do step #2 as the last item in appDidLoad in your App Delegate, if you'd like to make sure there's ample time to load all the data (especially helpful if your users typically don't have a good connection).


Customization:
-------------
More complex cases: 
1. Register a delegate with Choosy. The most important question a delegate can answer is, what is the parent view controller for Choosy's view controller? If the delegate does not respond to that question, but the delegate itself is a view controller, that view controller is used as the parent. But if the delegate is not present at all, Choosy uses top-most (i.e. currently visible) view controller in the Window hierarchy as the parent.