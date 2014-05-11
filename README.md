This is the data repository for [Choosy](https://github.com/substantial/choosy). To stay informed about changes to the data structure (if any) and major updates, please follow [@choosyios](http://www.twitter.com/choosyios).

If you'd like to help us and register an app's URL scheme with Choosy, please fork, modify/add files, and submit a pull request. If needed, we'll work with you to properly categorize the app, define actions and parameters, etc.

> NOTE: as of May 10 later afternoon, the data in files here gets merged with the [data about built-in apps](https://github.com/substantial/choosy/blob/master/Choosy/Resources/systemAppTypes.json). For example, if 'post' action is define for Twitter app type inside of that file, it will not be defined again in the twitter.json file here. This reduces file and download sizes. Since data gets merged, not repaced, the actions/parameters defined in the built-in file are still accessible to 3rd-party aps defined in files here, they just don't need to be re-defined here as well. You _can_ re-define same action or parameter if the built-in file is outdated; server data, once downloaded, will then be used over local data (server data always win over local data during merge). Choosy 0.6.0 and later supports this updated data storage structure.

### File structure

Each JSON file's name is the name of the app type. So if the app type is "twitter", the file name should be twitter.json. Each file always starts with `[{` and ends in `}]`, even though currently they all contain one app type each. All keys should be in [snake case](http://en.wikipedia.org/wiki/Snake_case)). Keys are Choosy-specific, but if there's a predominant or most-documented URL scheme for an known app that belongs to the category of apps we're describing, it's preferred to use their parameter names, unless another name is clearly better.

The format for the files is as follows:

```
[{
  name:   app type/category name in human-readable form, capitalized (ex: "Music Mixers")
  key:    unique string key (ex: "music_mixers")
  parameters:   (array of all parameters for this app type, across all apps)
      name:         human-readable, capitalized (ex: Profile Username")
      description:  human-readable, a sentence (ex: "Username of the profile to be shown")
      key:          unique in the scope of this app type (ex: "profile_screenname")
  actions:      (array of all supported actions for this app type)
      name:  human-readable, capitalized (ex: "Show Profile")
      key:   unique in the scope of this app type (ex: "show_profile")
  apps:     (array of all apps that this app type represents)
      name:    name to display below the icon (ex: "Tweetbot")
      key:     unique across all app types, so search if already used (ex: "tweetbot")
      app_url_scheme:  the front part of the url scheme, including the colon (ex: "tweetbot:")
      actions:  (array of actions that this app supports)
          key:  one of the keys from the 'actions' defined above for this app type (ex: "show_profile")
          url_format:  app-specific url scheme format for this action, with parameters in double curly braces (ex: "tweetbot:///user_profile/{{profile_screenname}}?callback_url={{callback_url}}")
}]
```

The magic sauce is in the `url_format` field. There, Choosy just replaces the parameter names in double curly braces with the actual values. 

So tweetbot:///user_profile/{{profile_screenname}}?callback_url={{callback_url}}

-> tweetbot:///user_profile/Substantial?callback_url=choosy%3A

### App icons

Please note that as of this writing, each app requires a corresponding app icon in the app-icons folder. We hope to start pulling icons from iTunes App Store instead, but if one isn't available there (or you're testing and your app is not in the App Store yet), then we'll use the icons from here. Please Submit square icons without rounded corners, just like you would for the App Store. You only need to submit icons for the platforms the app is available on (best to submit for all platforms to be safe, just so you don't have to remember to do it in the future). The icon sizes are as follows:

* \<appKey\>.png - 60x60 px
* \<appKey\>@2x.png - 120x120 px
* \<appKey\>~ipad.png - 76x76 px
* \<appKey\>@2x~ipad.png - 152x152 px

If you want to just submit JSON additions without an icon, that's fine. We'll find the icon(s) ourselves and merge your pull request afterwards. Any help is better than no help :)



**Thank you!**
