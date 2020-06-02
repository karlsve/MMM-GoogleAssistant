# Google Assistant Setup

## Get Auth and credentials to make profile.
1. Create a project in the [Actions Console](https://console.actions.google.com/)

**Follow this step**
  - New Project
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/1.png)
  - Agree and Continue
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/1b.png)
  - Create project
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/1c.png)

2. After creation, Enable `Google Assistant API` for your project in the [Cloud Platform Console](https://console.cloud.google.com/)

**Follow this step**
  - Agree and Continue<br>
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/2.png)
  - Select your project and note your `Project ID` name<br>
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/2a.png)
  - In the left menu select `APIs & Services` and `Library`<br>
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/2b.png)
  - API Library search<br>
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/2c.png)
  - Google Asssitant API search<br>
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/2d.png)
  - Enable Google Assistant API<br>
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/2e.png)
  - Wait for activation<br>
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/2f.png)
  
3. Return to Actions Console and Follow this instructions to register a device model

  - You can use this URL https://console.actions.google.com/u/[0]/project/[yourprojectId]/deviceregistration/) (change [] to your Project ID)<br>
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/3.png)
  - Register Model<br>
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/3b.png)
  - Download credentials<br>
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/3c.png)
  - Optional (Maybe for a future version Of GoogleAssistant)<br>
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/3d.png)

  - If needed, you can find again your credentials from [Cloud Platform Console](https://console.cloud.google.com/) (Your Project > APIs & Services > Credentials)<br>
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/4b.png)
4. `OAuth Consent Screen` setup
  - Go to [Cloud Platform Console](https://console.cloud.google.com/), then navigate to `APIs & Services > OAuth Consent Screen`. At first, you'll be asked which user type would use your project. Just select `External`.<br>
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/4c.png)
  - Select you email adress<br>
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/4d.png)
  - Save it<br>
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/4e.png)
  
4. you have download your credentials file (`client_secret_XXX.json` file) for OAuth and Carefully store it in `MMM-GoogleAssistant` directory and rename it to `credentials.json`
```sh
cd ~/MagicMirror/modules/MMM-GoogleAssistant
mv client_secret_XXX.json credentials.json
```
 
5. In your SBC, you can run auth-tool for auth. (not via SSH)
```sh
cd ~/MagicMirror/modules/MMM-GoogleAssistant
node auth_and_test.js
```
   - If you meet some errors related with node version, execute `npm rebuild` and try again.

   - At first execution, this script will try opening a browser and getting permission of a specific user for using this Assistant. (So you'd better to execute this script in your RPI shell, not via SSH)<br>
     ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/5a.png)

   - After confirmation, Some code (`4/ABCD1234XXXXX....`) will appear in the browser.<br>
     ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/5c.png)
   
   - Copy that code and paste in your console's request (`Paste your code:`)<br>
     ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/6.png)

   - On success, Prompt `Type your request` will be displayed. Type anything for testing assistant. (e.g: `Hello`)<br>
     ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/6a.png)

   - Now you can find `token.json` in your `MMM-AssistantGoogle` directory.<br>
     ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/6c.png)

## Get `deviceModelId` and `deviceInstanceId` [Optional]
> If you are not an experienced developer or don't need `gactions` implements, pass this section.

If you want not only pure Assistant embeding but also customized gactions for device, you might need to get `deviceModelId` and `deviceInstanceId`. To help understanding, **deviceModel** is something like `Volkswagen Golf` or `MagicMirror` and **deviceInstance** is something like `mom's car` or `mirror in living room`.

### For `deviceModelId`
You can get `deviceModelId` as a result of previous [register a device model](https://developers.google.com/assistant/sdk/guides/service/python/embed/register-device) step. In `Device registration` menu in `Actions Console`, you can find it.

### For `deviceInstanceId`
You need additional `google-assistant-sdk` library. See [
Manually Register a Device with the REST API](https://developers.google.com/assistant/sdk/reference/device-registration/register-device-manual#get-access-token) page.
