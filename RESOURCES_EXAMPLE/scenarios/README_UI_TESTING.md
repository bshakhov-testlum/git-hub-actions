# WEB

> **Testlum supports web page testing and mobile testing**

## List of all web commands:
```
click
scroll
dragAndDrop
input
javascript
repeat
dropDown
include
hovers
navigate
wait
image
assert
clear
switchToFrame
scrollTo
tab
hotKey
repeat
doubleClick	
```

### Usage Example
```xml
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="http://www.knubisoft.com/testlum/testing/model/scenario"
          xsi:schemaLocation="http://www.knubisoft.com/testlum/testing/model/scenario scenario.xsd">

    <overview>
        <description>Self test for command: click</description>
        <name>Click test</name>
    </overview>

    <settings>
        <tags>web,free</tags>
    </settings>

    <web comment="Start WEB scripts">

        <wait comment="Wait 1 second" time="1"/>

        <click comment="Click on 'Sign In' button"
               locatorStrategy="xpath" locator=".//button[@type=&quot;submit&quot;]"/>

        <wait comment="Wait 1 seconds" time="1"/>

        <assert comment="Create assert for command's test">
            <attribute comment="Assert for click" name="outerHTML" locator="dashboard.title">
                <content><![CDATA[<h3 class="text-3xl font-medium text-gray-700">Dashboard</h3>]]></content>
            </attribute>
        </assert>

        <wait comment="Wait for timeout scenario" time="1"/>
    </web>

</scenario>
```

> **A full description of WEB commands can be found** [here](https://testlum.developerhub.io/version-2/web-commands)