# CityMapper
I've checked your app for an hour and here are my notes:

Appsight.io goes back to April 2018. Unfortunately iMazing didn’t work on my iOS 13 beta phone to fetch ipa file and make some basic reverse engineering

## Questions
### FMDB
You’re using [FMDB](https://github.com/ccgus/fmdb)
Does that mean you’re handling multi-threading and sql queries? Realm would be better with lazy properties and handling migrations.
### Language
I assume all of your model layer is written by Objective-C. Do you use Swift at all or have some plans to use for example on the UI layer?
### Deep linking
I also see that you have deep link in your web site with app-site-association file. 
Did you encrypt it? Because What I get is a p7m file. However I can, of course, change its type to txt and see its content.
### Dev, Staging, Release builds
Do you have separate bundle id for each? Seems like that way on deep link identifiers.

## Bugs
### Not Allowing Location
Pick a City -> “Next City?” Button does not work 
You can add an alert mentioning “we need your access” with Settings button to easily navigate user.

### Pick a City
I can not see the bottom of the list when keyboard is open. You can use keyboard size as an inset to table view.

### Login
1. You will require “Sign in with Apple“ due to having 3rd party authorization such as Facebook and Google

2. You can add auto completion for email on top of keyboard by setting input type of the text field.

### Settings -> AR 
1. Back icon button is misplaced on iPhone X
2. App freezes for 1 second when you open it without camera access.

### City -> Get Me Somewhere -> Date picker
1. Check button interferes with bottom safe area on iPhone X
2. X button seems misplaced
3. Switching locations causing a “Thinking…” cell to appear and disappear like a glitch

### City -> Maps
Selecting Map Alert Sheet -> Does not allow to tap outside for dismissing due to Cancel action is not typed `.cancel` (it should have been bold text)

### City -> Bus and some other parts
Scrolling becomes unresponsive during initializing info after opening it %50 of the time. Definitely caused by main thread block. Also happens on the list during scrolling animation.

### City -> Select any element on the top section
Scroll to bottom until map is disappeared -> Select back icon -> City UI stays on some kind of weird state with "Location access is turned off error"
You have to select a location on map and then select back again.

### City (Istanbul) -> Tram 
Scrolling through info while background is white conflicts with also white status bar.

### City -> More
Empty selections maybe you can make it more of a transparent or grayish color instead of pure white.

## Improvements
### Apple Watch
Are you thinking about using Apple Watch for example telling user it's time to get off of the bus? It would be nice without forcing user to check his phone. A notification with haptic feedback would be really useful.

### Praise
Overall I liked the transition animations and snapping behaviors. 
Colors are also nice with highlighting.
Awesome job.

## Quick Look
### Onboarding Items
I would try to center vertically the onboarding items (Get Started, Enable Location, Enable Notifications etc.) as an iPhone X user.

### After Selecting the City
1. Table cell with `Get Me Home` `SET`: Button border color seems to be the same during highlighting. You can visualize it with white color.
2. Also highlighting the bottom cell makes `Use GO to collect and learn` label gray when the arrow color becomes white. Seems a bit inconsistent.
3. I loved the activating the map by scrolling. However you may want to consider delaying the home swipe gesture from the bottom by using `preferredScreenEdgesDeferringSystemGestures`. 
[Example](https://www.hackingwithswift.com/example-code/uikit/how-to-control-which-screen-edges-trigger-system-gestures-using-preferredscreenedgesdeferringsystemgestures)
