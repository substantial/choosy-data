This is the data repository for the open-source [Choosy framework](https://github.com/substantial/choosy). To stay informed about any breaking data structure changes and major updates, please follow [@choosyios](http://www.twitter.com/choosyios) on Twitter.

If you'd like to register an app's URL scheme with Choosy, please fork, modify, and submit a pull request. We'll work with you to property categorize the app, define actions and parameters, etc.

Please note that as of this writing, each app requires a corresponding app icon in the app-icons folder. We hope to start pulling icons from iTunes App Store instead, but if one isn't available there (or you're testing and your app is not in the App Store yet) then we'll use the icon from here. Please Submit **square** icons without rounded corners, just like you would for the app store. Choosy adds rounded corners at runtime. Choosy needs 4 icon sizes (each device only downloads the size it needs): 

<appKey>.png - 60x60 px
<appKey>@2x.png - 120x120 px
<appKey>~ipad.png - 76x76 px
<appKey>@2x~ipad.png - 152x152 px

If you want to just submit JSON additions without an icon, that's fine. We'll find the icon(s) ourselves and merge your pull request afterwards. Any help is better than no help :)

Thank you!
