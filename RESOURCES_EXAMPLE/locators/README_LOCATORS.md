# Locators
> Before describing the WEB related commands, it is necessary to know how to create a locator and connect it to a scenario

## Available types of locators:

* id
* class
* xpath
* cssSelector
* text

## Locator for commands can be written in two types:
1. **locatorId** - locators are created in special folders with names that can be used in different scenarios without duplicating the entire locator
2. **Directly in the field for the locator** - the locator is entered in the field in its entirety each time

### locatorId
This approach is described in detail in the file  [README_PAGES.md](README_PAGES.md)

### Directly In The Field For The Locator
**To write locators directly in the field for the locator you need:**

* Use the locatorStrategy atribute in each command that you need
```xml
<click comment = "Click on 'email' button" locator="" locatorStrategy=""/>
```

* Select the required locator type (`locatorId` - is default value, which there is no need to write)
```xml
<click comment = "Click on 'email' button" locator="" locatorStrategy="xpath"/> - the type of locator that will be in the locator field
```

* Write locator in the `locator` field
```xml
<click comment = "Click on 'email' button" locator="//input[@type='email']" locatorStrategy="xpath"/>
```