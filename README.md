# isMobile

isMobile is a simple yet powerful function that I wrote in PHP that will detect if a user is on a mobile browser and/or a mobile device. With this function, you can easily create a conditional statement that allows you to redirect mobile users to your mobile site and/or show mobile only css, code, etc. On top of being extremely accurate, this function is only 220 bytes, which is impressive considering other scripts with less accuracy are anywhere from 5x to 40x the size.

### Basic usage

`// Create the function, so you can use it
function isMobile() {
    return preg_match("/(android|avantgo|blackberry|bolt|boost|cricket|docomo|fone|hiptop|mini|mobi|palm|phone|pie|tablet|up\.browser|up\.link|webos|wos)/i", $_SERVER["HTTP_USER_AGENT"]);
}
// Use the function
if(isMobile())
    // Do something for only mobile users
else
    // Do something for only desktop users
`
### How does it do it?

This PHP function searches the user-agent string $_SERVER['HTTP_USER_AGENT'], using PHP’s preg_match() for fragments that signify a mobile browser is being used, than returns a boolean value (true/false) for use in your code. Although this script is tiny, it’s accuracy makes it a valuable asset when you want to cater to mobile users.

### How do I use this script?

I’ve been asked a lot, since creating the script, “How do I use this if I want to [insert scenario]“. To answer the most common questions, I’ve written some basic solutions below. If you dont see a solution for your scenario, please feel free to leave me a comment on this page or email me at justin@justindocanto.com and I’ll help you the best I can.

`// Create the function, so you can use it
function isMobile() {
    return preg_match("/(android|avantgo|blackberry|bolt|boost|cricket|docomo|fone|hiptop|mini|mobi|palm|phone|pie|tablet|up\.browser|up\.link|webos|wos)/i", $_SERVER["HTTP_USER_AGENT"]);
}
// Use the function
if(isMobile())
    // Do something for only mobile users
else
    // Do something for only desktop users
`

### How do I detect a mobile user, so I can redirect them to my mobile website?

Place this code at the top of your site’s index.php file. It will graciously redirect mobile users to your your mobile site at http://m.yoursite.com/.

`// Create the function, so you can use it
function isMobile() {
    return preg_match("/(android|avantgo|blackberry|bolt|boost|cricket|docomo|fone|hiptop|mini|mobi|palm|phone|pie|tablet|up\.browser|up\.link|webos|wos)/i", $_SERVER["HTTP_USER_AGENT"]);
}
// If the user is on a mobile device, redirect them
if(isMobile())
    header("Location: http://m.yoursite.com/");
`
### How do I detect a mobile user in WordPress, so I can redirect them to my mobile website?

The code directly above will not work if you put it in your theme’s index.php file because PHP’s header() function cannot work if any headers have already been set, which they are by the time WordPress gets to your theme’s index.php file. Technically you could edit your WordPress’s core index.php file as a ‘hack’ but that is not recommended since updating WordPress could/will overwrite your code and there’s a much better way to do it.

The best way to setup this function within WordPress is by putting the following code in your theme’s function.php file. First it creates the function and then it tells WordPress, using WordPress’s add_action() function, to call it as one of the first pieces of code it runs so you dont run into any sort of conflicts with your headers already being defined.

`// Create the function, so you can use it
function isMobile() {
    return preg_match("/(android|avantgo|blackberry|bolt|boost|cricket|docomo|fone|hiptop|mini|mobi|palm|phone|pie|tablet|up\.browser|up\.link|webos|wos)/i", $_SERVER["HTTP_USER_AGENT"]);
}
// Tell WordPress to use this function as soon as it starts
function isMobileForWordPress() {
    // If the user is on a mobile device, redirect them
    if(isMobile())
        header("Location: http://m.yoursite.com/");
}
add_action('init', 'isMobileForWordPress', 1);
`
### How do I detect a mobile browser, but allow them to choose the desktop version?

This is another frequently asked question that I’d like to address. Let’s say you had an index.php file that serves your documents or a header.php file that’s called at the top of every page. By placing the following code on the top of one of those pages, you could have a link anywhere on your mobile site that says ‘Desktop Version’ that made the isMobile() function skip the redirect for the rest of that user’s session.

The following code assumes your ‘Show Desktop’ link looks like this: http://www.yoursite.com/index.php?desktop=true

`// Start the $_SESSION so we can set $_SESSION variables
start_session();
// If the user clicked the 'Desktop Only' link, set a $_SESSION variable
if(isset($_GET['desktop']) && $_GET['desktop'] == "true")
    $_SESSION['desktop'] = "true";
// If this is a mobile user and the $_GET and/or $_SESSION 'desktop' variables aren't set to true, redirect this user
if(isMobile() && $_GET['desktop'] != "true" && !$_SESSION['desktop'] != "true")
    header("Location: http://m.yoursite.com/");
`

Please note: do not include the start_session() function if you already have a session setup to be started on your site, as this will cause errors on your site.

### Test Results

To view test results again user-agent strings for approx 30 popular devices (iphones, blackberrys, android devices, sidekicks, palm devices, mac osx desktops, windows desktops, linux desktops, etc) please visit http://www.justindocanto.com/scripts/detect-a-user-on-a-mobile-browser-or-device

### Questions, Requests & Support
##### Justin DoCanto
* justin@justindocanto.com
* justindocanto.com
* @justindocanto

### Known Issue: HTML Caching Conflicts

If you are caching html on your website, this can create inaccuracies when using this script. By nature of html caching, the first time a page is viewed it is cached as HTML and delivered to all future parties the same way. HTML caching typically prevents the dynamic portions of a page from loading so dynamic scripts such as this one are never even called and cannot do their job. Please disable caching of html for any pages that use this script for it to work properly.

Updated May 1st, 2012: For the sake of brevity and legibaility, I changed the name of this function from detectMobileDevice() to isMobile().

Updated June 11th, 2012: I received a few messages recently about the double quotes not copying correctly into a text editor, so I wrapped the examples in tags that should allow everybody to copy and paste the examples without running into any PHP errors.