# ui.xml
`ui.xml` - is a file, where you can set configurations for the WEB, Native and Mobile Browser tests


## WEB
> Inside this command you are able to configure all settings that needed to conduct WEB test scenario

* `baseURL` - is a command for placing base URL of system under test

* `browserSettings` - is a command where you can set up details for conducting your web test scenario, such as <takeScreenshots> , <elementAutowait> and <browsers>

  * `takeScreenshots` - is used to choose whether to make screenshots for each UI test step or not

  * `elementAutowait` - is a command to configure auto wait for ui elements.

  * `browsers` - is a command where you are able to choose different browsers for your UI test

    * `chrome` `edge` `safari` `opera` `firefox` - allows to configure different types of **Google Chrome**, **Opera**, **Safari**, **Microsoft Edge** and **Firefox** browser, such as `localBrowser`, `remoteBrowser` and `browserInDocker`. Identically. 
    * Contains attributes: 
      1. `alias` - you can give an Alias to any browser 
      2. `maximizedBrowserWindow` - when selected true, test scenarios will be executed on maximixed browser window 
      3. `headlessMode` - when selected true, browser window will be shown during test execution 
      4. `browserWindowSize` - when attribute `maximizedBrowserWindow="false"` is active, you can choose any window size for your UI test

         * `browserType` is a command within which you can choose needed browser type, such as: `localBrowser`, `remoteBrowser`, `browserStack` and `browserInDocker`

           * `localBrowser` - is a command, that allows to use locally installed web browser for conducting WEB test scenarios. 
             * Contains attributes: 
               1. `driverVersion` - is used to identify driver version of web browser, that you want to use while test execution.
           * `remoteBrowser` - is a command to configure remote browser settings that allows execute WEB test scenarios on remote web server. 
             * Contains attributes: 
               1. `browserVersion` - here you can enter version of the browser that you want to use. 
               2. `remoteBrowserURL` - attribute to place URL Selenium Grid for remote browser.
           * `browserInDocker` - is a command to configure browser in dockersettings. 
             * Contains attributes: 
               1. `browserVersion` - here you can enter version of the browser. that you want to use. 
               2. `dockerNetwork` - is used to enter docker network. 
               3. `enableVNC` - when selected true, record of test execution will be saved on your computer and when selected false, record of test execution will not be saved on your computer, but you can see results of tests in logs and reports.
           * `browserStack` is a command to configure browserStack settings. 
             * Contains attributes: 
               1. `browserVersion` - is to identify browser version. 
               2. `os` - is to identify OS. 
               3. `osVersion` - is to identify OS version
           
         * `chromeOptionsArguments` - allows to set and use any chrome options argument for test execution. The same command is able to use with other browsers, that Testlum supports.

           * `argument` - here you can enter needed chrome options argument.
         * `capabilitites` - allows to set and use any capabilities for test execution. The same command is able to use with other browsers, that Testlum supports.

           * `capability` 
           * Contains attributes: 
             1. `name` - is used to enter capability name. 
             2. `value` - value for the specific capability

  
> **If no `driverVerison` is entered, Testlum will use the latest version of web browser, that is installed locally**

### Usage Example
```xml
<web enabled="...">
        <baseUrl>...</baseUrl>
        <browserSettings>
            <takeScreenshots enabled="..."/>
            <elementAutowait seconds="..."/>
            <browsers>
                <chrome enabled="..." maximizedBrowserWindow="..." alias="..." headlessMode="..." browserWindowSize="...">
                    <browserType>
                        <localBrowser driverVersion="..."/>
                    </browserType>
                    <browserType>
                        <browserStack browserVersion="..." os="..." osVersion="..."/>
                    </browserType>
                    <browserType>
                        <browserInDocker browserVersion="..." enableVNC="..." dockerNetwork="..."/>
                    </browserType>
                    <browserType>
                        <remoteBrowser browserVersion="..." remoteBrowserURL="..."/>
                    </browserType>
                    <capabilities>
                        <capability name="..." value="..."/>
                        <capability name="..." value="..."/>
                    </capabilities>
                    <chromeOptionsArguments>
                        <argument>...</argument>
                    </chromeOptionsArguments>
                </chrome>
                <firefox enabled="..." maximizedBrowserWindow="..." alias="..." headlessMode="..." browserWindowSize="...">
                  ... 
                </firefox>
                <opera enabled="..." maximizedBrowserWindow="..." alias="..." headlessMode="..." browserWindowSize="...">
                  ...
                </opera>
                <safari enabled="..." maximizedBrowserWindow="..." alias="..." headlessMode="..." browserWindowSize="...">
                  ...
                </safari>
                <edge enabled="..." maximizedBrowserWindow="..." alias="..." headlessMode="..." browserWindowSize="...">
                  ...
                </edge>
            </browsers>
        </browserSettings>
</web>
```



## Mobile Browser
> Inside this command you are able to configure all settings that needed to conduct mobilebrowser test scenario
* `baseURL` - is a command for placing base URL of system under test

* `takeScreenshots` - is used to choose whether to make screenshots for each UI test step or not

* `elementAutowait` - is a command to configure auto wait for ui elements.

* `connection`

  * `browserStack` - this command indicates which suggests that this configuration is for using BrowserStack for testing. (only one `browserStack` or `appiumServer` can be selected)

  * `appiumServer` - this command indicates which suggests that this configuration is for using appiumServer for testing. (only one `browserStack` or `appiumServer` can be selected)

    * `serverUrl` - to configure the appium server url
    
  * `devices` - command where you can declare multiple devices and where you can easily switch between them.

    * `device` this element may contain configurations or settings related to the devices on which you want to perform mobile testing. 
    * Contains attributes: 
      1. `platformName` - option to choose Android or iOS. 
      2. `enabled` - the ability to choose whether this device will be connected or not. 
      3. `alias` - you must give an Alias to any device

      * `appiumCapabilities` - this command indicates the Appium server configuration

        * `deviceName` - represents the name of the mobile device on which the testing will be performed.
        * `platformVersion` - specifies the version of the mobile operating system.
        * `udid` - the UDID (Unique Device Identifier) is typically used for identifying the specific device when running tests. (If the simulator is running, you can find UDID by executing the command in the terminal - adb devices)

      * `browserStackCapabilities` - this command indicates the Browser Stack configuration

        * `deviceName` - represents the name of the mobile device on which the testing will be performed.
        * `platformVersion` - specifies the version of the mobile operating system.
      * `capabilities` - allows to set and use any capabilities for test execution.

        * `capability` 
        * Contains attributes: 
          1. `name` - is used to enter capability name. 
          2. `value` - value for the specific capability

### Usage Example
```xml
<mobilebrowser enabled="...">
        <takeScreenshots enabled="..."/>
        <elementAutowait seconds="..."/>
        <baseUrl>...</baseUrl>
        <connection>
            <appiumServer>
                <serverUrl>...</serverUrl>
            </appiumServer>
          
            <browserStack/>
        </connection>
        <devices>
            <device platformName="..." enabled="..." alias="...">
                <appiumCapabilities>
                    <deviceName>...</deviceName>
                    <platformVersion>...</platformVersion>
                    <udid>...</udid>
                </appiumCapabilities>
              
                <browserStackCapabilities>
                    <deviceName>...</deviceName>
                    <platformVersion>...</platformVersion>
                </browserStackCapabilities>
              
                <capabilities>
                    <capability name="..." value="..."/>
                    <capability name="..." value="..."/>
                 </capabilities>
            </device>
        </devices>
</mobilebrowser>
```


## Native
> Inside this command you are able to configure all settings that needed to conduct native test scenario

* `takeScreenshots` - is used to choose whether to make screenshots for each UI test step or not

* `elementAutowait` - is a command to configure auto wait for ui elements.

* `connection`

  * `browserStack` - this command indicates which suggests that this configuration is for using BrowserStack for testing. (only one `browserStack` or `appiumServer` can be selected)

  * `appiumServer` - this command indicates which suggests that this configuration is for using appiumServer for testing. (only one `browserStack` or `appiumServer` can be selected)

    * `serverUrl` - to configure the appium server url
    
  * `devices` - command where you can declare multiple devices and where you can easily switch between them.

    * `device` - this element may contain configurations or settings related to the devices on which you want to perform mobile testing. 
    * Contains attributes: 
      1. `platformName` - option to choose Android or iOS. 
      2. `enabled` - the ability to choose whether this device will be connected or not. 
      3. `alias` - you must give an Alias to any device

      * `appiumCapabilities` -  this command indicates the Appium server configuration

        * `deviceName` represents the name of the mobile device on which the testing will be performed.
        * `platformVersion` specifies the version of the mobile operating system.
        * `udid` the UDID (Unique Device Identifier) is typically used for identifying the specific device when running tests. (If the simulator is running, you can find UDID by executing the command in the terminal - adb devices)
        * `appPackage` specifies the package name of the Android app you want to test. This is required when testing Android apps.
        * `appActivity` defines the main activity within the Android app that you want to launch. It's also used in Android app testing.
        
      * `browserStackCapabilities`

        * `deviceName` represents the name of the mobile device on which the testing will be performed.
        * `platformVersion` specifies the version of the mobile operating system.
        * `app` refers to the mobile application (APK or IPA file) you want to test. You provide the key that you get when you download the application to the browser stack
        * `googlePlayLogin` command to automatically login into your Google Play account
          * `email` - Email from Google Play account
          * `password` - Password from Google Play account

      * `capabilities` - allows to set and use any capabilities for test execution.

        * `capability` 
        * Contains attributes: 
          1. `name` - is used to enter capability name. 
          2. `value` - value for the specific capability

> Make sure you disabled additional security checks (**like two-step verification**) in your google account that you want to use for logging in

### Usage Example:
```xml
<native enabled="...">
        <takeScreenshots enabled="..."/>
        <elementAutowait seconds="..."/>
        <connection>          
            <appiumServer>
               <serverUrl>...</serverUrl>
            </appiumServer>
          
            <browserStack/>
        </connection>
        <devices>
            <device platformName="..." enabled="..." alias="...">
                <appiumCapabilities>
                    <deviceName>...</deviceName>
                    <platformVersion>...</platformVersion>
                    <udid>...</udid>
                    <appPackage>...</appPackage>
                    <appActivity>...</appActivity>
                </appiumCapabilities>
              
                <browserStackCapabilities>
                    <deviceName>...</deviceName>
                    <platformVersion>...</platformVersion>
                    <app>...</app>
                    <googlePlayLogin>
                        <email>...</email>
                        <password>...</password>
                    </googlePlayLogin>
                </browserStackCapabilities>
              
                <capabilities>
                    <capability name="..." value="..."/>
                    <capability name="..." value="..."/>
                 </capabilities>
            </device>
        </devices>
</native>
```

## BrowserStack Login
> Inside this command you are able to set BrowserStack credentials that needed to conduct test scenario on BrowserStack

* `username` - Username from the Stack browser which can be found by path: Account & Profile/View profile
* `accessKey` -Access Key from the Stack browser which can be found by path: Account & Profile/View profile

### Usage Example:
```xml
<browserStackLogin>
        <username>...</username>
        <accessKey>...</accessKey>
</browserStackLogin>
```