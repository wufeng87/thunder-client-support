<p align="center">
  <img src="images/thunder-icon.png" width="120" height="120" />
</p>

# Thunder Client
[![installs](https://vsmarketplacebadge.apphb.com/installs/rangav.vscode-thunder-client.svg)](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client) [![version](https://vsmarketplacebadge.apphb.com/version-short/rangav.vscode-thunder-client.svg)](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client)

Thunder Client is a lightweight Rest API Client Extension for Visual Studio Code, hand-crafted by [Ranga Vadhineni](https://twitter.com/ranga_vadhineni) with simple and clean design. The source code is not open source. You can report any Bugs Or Feature requests here.

* Voted as **#10 Product of the day** on [Product Hunt](https://www.producthunt.com/posts/thunder-client)
* Website - [www.thunderclient.com](https://www.thunderclient.com)
* Follow Us for updates - [Twitter](https://twitter.com/thunder_client), [LinkedIn](https://www.linkedin.com/company/thunderclient/)

#### Story behind Thunder Client
* Read Launch Blog Post on [Medium](https://rangav.medium.com/thunder-client-alternative-to-postman-68ee0c9486d6)

## Menu
* [How to Use](#usage)
* [Tech](#tech)
* [Features](#features)
* [Team Features / Git Sync](#team)
* [Testing](#testing)
* [Environments](#environments)
* [Set Environment Variable](#setenv)
* [Auth](#auth)
* [Path Variables](#path)
* [System Variables](#variables)
* [Code Snippet](#codegen)
* [Proxy](#proxy)
* [Http/2](#http2)
* [Import/Export](#import)
* [Keyboard Shortcuts](#keyboard)
* [VS Code Settings](#settings)
* [Contribution](#contribution)
* [Privacy](#privacy)


<a name="usage"></a>
## How to Use
* Install the Extension, Click Thunder Client icon on the Action Bar.
* From Sidebar click `New Request` button to test API
* Video: [youtube.com/watch?v=NKZ0ahNbmak](https://youtu.be/NKZ0ahNbmak?t=3)

![](images/thunder-client.gif)

<a name="tech"></a>
## Tech
* Thunder Client is built with **Javascript, Typescript, Flexbox, Ace Editor, Got, Nedb**.

<a name="features"></a>
## Features
* Send http/https API request using any of the methods GET, POST, PUT, DELETE, PATCH, HEAD and OPTIONS.
* The Response data supports **syntax hightlighting using ACE Editor** which can handle large responses easily, you can also view response in **Full Screen**
* **History, Collections and Environment** Tabs in the Action Bar View for quick access.
* **[Authentication](#auth):** Basic Auth, Bearer Token and OAuth 2.0 are supported.
* **Post Body:** For Post Content-Type header will be automatically set.
* **Graphql:** Send Graphql Query & Variables has syntax highlighting support.
* **Environment Variables:** Syntax highlighting support for environment variables just use `{{variable}}` syntax in most fields
* **[Scriptless Testing](#testing):** Test APIs with GUI based functionality, no scripting knowledge needed.
* **Themes:** The extension also supports VS Code themes.

<a name="team"></a>
## Team Features
The team features are useful to share requests with team by saving data in git project.

**WARNING**: The **Environment** file which stores the secrets also saved in the same git folder, see **Note: 1** below.

Integration with the Git project is supported by below vscode settings, choose **any one** as required.

1. **Load From Project**: select this option when you like to spilt requests data per project, it will create `thunder-tests` folder in root of workspace. This option loads the data when you open the project in vscode automatically.
   * (Optional) The default location of `thunder-tests` folder is root of workspace. Use setting `Workspace Relative Path` to specify different relative path. see below examples
   * Make sure the `Workspace Relative Path` setting is **Workspace** setting not **User** setting.
   * Example 1: To save in Child folder of workspace then relative path is `FolderName` or `Child/FolderName`
   * Example 2: To save in Parent folder of workspace then relative path is `../`
2. **Custom Location**: select this option when you like save all the requests data in one fixed location, enter the full folder path to save the data.
   * Supports relative path to Home directory. use **$HOME** prefix e.g `$HOME/Documents/ProjectName`
   
   
* Note 1: The environments will be stored in `thunderEnvironment.db` file, which will be part of **thunder-tests** folder. If you like to exclude any secrets from `thunderEnvironment.db` file then use `Local Environment` to store values locally on your computer
* Note 2: **Files changes** are not detected by the extension yet, if you pulled changes from git, click **Reload** icon in sidebar.
* Note 3: Please **restart vscode** after updating settings.

<a name="testing"></a>
## Scriptless Testing
![](https://github.com/rangav/thunder-client-support/blob/master/images/thunder-client-tests.png?raw=true)

* We need to write a lot of boilerplate code in Postman and other clients to do basic testing using scripting like status code equal 200. So I implemented GUI based tests, where you select couple of dropdowns to do most standard tests very easily without any scripting knowledge.
* Tests can be done for strings, number, count and type checking
* Setting Env variable also possible in Tests section
* Re-arrange tests order using drag and drop

<a name="environments"></a>
## Environments
![env2](https://user-images.githubusercontent.com/8637550/154529631-7b6a4cb0-5538-471d-ab88-4035bacba878.png)

The following environments can be used in Thunder Client from least precedence to high precedence are listed below.
1. **Local Environment**: Use Local Environment to save secrets and transient tokens locally on your computer, which you dont want to save in the git project. This environment is a `global type` and the variables are available to all collections. (See above image option 3)

2. **Global Environment**: Use Global Environment to save variables and share with all the collections. The values will stored in main `thunderEnvironment.db` file.  (See above image option 2)  

3. **env file**: You can use `.env files` in Thunder Client. To Use .env file follow below steps
   - Create an Environment (using option 1 in img)
   - Open the Environment view, then you will see the option `Link to .env file`
   - Select the .env file and save it, Now you can use the variables in the Requests using `{{variable}}`
   - The env file variables format should be in 
    ```
    key=value
    name=thunder
    number=25543
    ```
 4. **Active Environment**: To use an environment variables, you need to make it active using the options menu `...` then select `Set Active`.
 5. **Attach Env to Collection**: (Optional) You can attach a environment to collection from Collection Settings view. Use this option when you like to link multiple collections to multiple environments. The values in this Environment will take precedence over Active Environment. If you change environment frequently, this option is not recommended. Please see example below
    ```
    CollectionA -> EnvA
    CollectionB -> EnvB
    CollectionC -> EnvC
    ``` 
 
 #### Import Env
 You can import Thunder Client, Postman and .env files using the Import Menu Option ( see above image option 4), more details [here](#import) 

<a name="setenv"></a>
## Set Environment Variable
Setting environment variables is supported in the Tests tab. Follow the steps below:
 * Create an environment first from the Env tab if it's not already created.
 * In the Tests tab, select the `Set Env Variable` dropdown option. (The action will automatically become `setTo`.)
 * Enter the appropriate source of variable value in the left input box:
   * **Header:** Enter `header.headerName` where `headerName` is the response header name.
   * **Cookie:** Enter `cookie.cookieName` where `cookieName` is the response cookie name.
   * **JSON Response:** Enter `json.propertyName` where `propertyName` is the JSON key in the response body.
   * **Text Response:** Enter the `text` keyword. This sets the entire response body to the variable.
 * In the value input, enter a variable name in the `{{variableName}}` format.
   * When it matches a variable name in Env, it will turn **green**. If the variable doesn't exist, it will be created.
 * Now execute the request. You will see the variable value set in the Env tab.
   * If you don't see the change in the Env tab, close and re-open the tab to refresh it.
 <a name="scope"></a>
 #### Set Env with Scope
   The default location will be Active Environment when you use `{{variable}}`. You can use scope to control which environment variable to set the value explicitly
 * To set variable in **local** environment use `{{variable, local}}`
 * To set variable in **global** environment use `{{variable, global}}`
 * (optional) To set variable in **active** environment use `{{variable, active}}`, Use this format only when you have attached Environment to Collection, otherwise `{{variable}}` format should be used
 
<a name="auth"></a>
## Auth
* OAuth 2.0 when grant type is **Authorization Code** the **callback url** needs to be entered into your oauth server trusted redirect url list.
* OAuth authentication credentials are sent **via header or body**, please select appropriate one based on your server requirement.

* ### Manual SSL Certificates
  * Provide ssl certificate paths for auth, using relative path to workspace or absolute paths. 
  * Use the **Certificates** vscode setting, see example below
  ```json
  "thunder-client.certificates": [
          {
              "host": "thunderclient.io",
              "certPath": "ssl/cert.pem",
              "keyPath": "ssl/keyfile.key",
              "pfxPath": "ssl/pfx.p12",
              "passphrase": "test"
          },
          {
              "host": "localhost:8081",
              "pfxPath": "/Users/test/Documents/ssl/pfx.p12",
              "passphrase": "test"
          },
          {
              "host": "testing.com",
              "certPath": "ssl/cert.pem",
              "keyPath": "ssl/keyfile.key"
          },
      ]
  ```
    
<a name="path"></a>
## Path Variables
Path variables are supported using the format `{variable}` in the url field
* e.g 1: `https://www.thunderclient.com/details/customer/{customerId}`
* e.g 2: `https://www.thunderclient.com/details/{customerId}{name}/`

<a name="variables"></a>
## System Variables
The system variables are useful to generate random/dynamic data for use in request query params or body. The format is `{{#variableName}}`
* {{#guid}} - generates random uuid
* {{#string}} - generates random string
* {{#number}} - generates random number between 1 to 1000000
  * Custom Range: use `{{#number, min, max}}`, e.g: `{{#number, 100, 999}}`
* {{#email}} - generates random email
* {{#date}} - generates date timestamp
  * Custom date format: use `{{#date, 'YYYY-MM-DD hh:mm:ss:fff'}}`, the format should be in single quote.
* {{#dateISO}} - generates date ISO format
* {{#bool}} - generates true or false
* {{#enum, val1, val2, val3,...}} generates one of the enum values (comma separated) provided
  * e.g `{{#enum, red, green, blue}}`
  * e.g `{{#enum, 1, 2, 3}}`

<a name="codegen"></a>
## Code Snippet
The code snippet generation is available for following languages. Open request view and click icon `{}` to see Code Tab.
* C# - HttpClient
* cURL
* Dart Http
* Javascipt Fetch & Axios
* PowerShell
* Python requests & http.client

The feature is open for contribution - https://github.com/rangav/thunder-codegen 

<a name="proxy"></a>
## Proxy
* Proxy is supported using vscode proxy setting. format `http://username:password@host:port` 
* **exclude Proxy Host List**: Use this setting to exclude hosts from proxy, supports comma separated values e.g: `abc.com,xyz.com`

<a name="http2"></a>
## Http/2
* To send request using Http/2 protocol, please select `HTTP/2` option in vscode settings for **Http Version**

<a name="import"></a>
## Import/Export
* You can import or export Thunder Client collections and environment data.
* Currently you can import collection or Environment file from **Postman** 2.1.0 format. ( other file formats support soon.. ).
* Submit PR for other file formats on https://github.com/rangav/thunder-imports
* **Import Curl** is now supported from Activity tab. Keyboard shortcut `Cmd/Ctrl + u`
* Import of **.env files** also supported, select `Import` from Env tab and choose .env file

#### How to Import Collection
  1. Select the `Collection` tab from the sidebar
  2. Click `Menu` icon near searchbar, and Select `Import`
  3. Now select json file from Postman or Thunder Client.
  
#### How to Convert to Postman Fortmat
  - First Export Thunder Client collection to json file, Then convert to Postman format using below options
  - From Command Palette - `Convert To Postman Format` option available
  - From Sidebar menu at the Top `(...)` select `Convert To Postman Format`

<a name="keyboard"></a>
## Keyboard Shortcuts
* `Ctl+Shift+P`: From Command Palette
  * Thunder Client - New Request 
  * Thunder Client - Run Last Request
  * Thunder Client - Change Environment
  * Thunder Client - Convert To Postman Format
* `Cmd/Ctrl + Enter`: To execute the request.
* `Enter` on request url field to send request.
* `Cmd/Ctrl + s` Save Request without run.
* `Cmd/Ctrl + click` on request in Sidebar will open in new tab
* `Cmd/Ctrl + s` Environment view save data.
* `Cmd/Ctrl + e` Change Active Environment.
* `Alt+Shft + f` Format Post Body data.
* `Cmd/Ctrl + u` Import Curl
* `Alt + z` Toggle Word wrap on response

<a name="settings"></a>
## VS Code Settings

To see all the Thunder Client vscode settings
1. Open vscode settings View, then search for `Thunder Client`
2. From Sidebar View -> Click `...` menu at the top, then click `Extension Settings`

<a name="contribution"></a>
## Contribution
* Documentation: if you like to improve documentation, please submit PR.
* The following modules are open for contribution, let me know if you like to contribute
  * Code Snippet Generation
  * Import of OpenAPI json/yaml files
  * Import of Insomnia Collections

<a name="privacy"></a>
## Privacy
* Basic anonymised analytics data is collected using [vscode-extension-telemetry](https://github.com/Microsoft/vscode-extension-telemetry), No Personal or request data is collected. You can opt out using VS Code Settings [details here](https://code.visualstudio.com/docs/getstarted/telemetry)
* There is no backend or cloud sync, all the data is stored locally on your computer.


