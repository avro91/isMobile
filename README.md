# detectMobileDevice

detectMobileDevice() is powerful little PHP function that I wrote that detects if a user is on a mobile device, so you can easily do something specifically for a mobile user. The function searches the user-agent string $_SERVER['HTTP_USER_AGENT'] for terms that signify a mobile device is being used or not and returns a boolean value (true/false) for use in your code. Although this script is tiny, it’s accuracy makes it valuable when you take into consideration there are very few alternative solutions elsewhere online.

### Basic usage
`if(detectMobileDevice()) { // If mobile device detected, do something... } else { // Otherwise, do something else... }`

Note: To create as lightweight & efficient of a script as possible, I resisted searching for unnecessary terms. For example, I do not search for “iPhone” as searching for “mobi” within ‘mobile’ already detects an iPhone, as well as many other mobile devices.

### Test Results

To view test results again user-agent strings for approx 30 popular devices (iphones, blackberrys, android devices, sidekicks, palm devices, mac osx desktops, windows desktops, linux desktops, etc) please visit http://www.justindocanto.com/scripts/detect-a-mobile-device-in-php-using-detectmobiledevice

#### Suggested Uses

* Detect when to redirect users to a mobile version of your site
* Include mobile-only code (eg. special stylesheet or javascript)
* Detect when to display mobile-friendly content (eg. different image sizes or an abbreviated form)

### Questions, Requests & Support
##### Justin DoCanto
* justin@justindocanto.com
* justindocanto.com
* @justindocanto

### Known Issue: HTML Caching Conflicts

If you are caching html on your website, this can create inaccuracies when using this script. By nature of html caching, the first time a page is viewed it is cached as HTML and delivered to all future parties the same way. HTML caching typically prevents the dynamic portions of a page from loading so dynamic scripts such as this one are never even called and cannot do their job. Please disable caching of html for any pages that use this script for it to work properly.