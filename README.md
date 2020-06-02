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
  - Agree and Continue
  
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/2.png)
  - Select your project
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/2a.png)
  - In the left menu select `APIs & Services` and `Library`
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/2b.png)
  - API Library search
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/2c.png)
  - Google Asssitant API search
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/2d.png)
  - Enable Google Assistant API
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/2e.png)
  - Wait for activation
  ![](https://github.com/bugsounet/MMM-GoogleAssistant/blob/setup/resources/2f.png)
  
3. Return to Actions Console and Follow the instructions to [register a device model](https://developers.google.com/assistant/sdk/guides/service/python/embed/register-device)

(If you cannot find `Device registration` menu, you can use this URL https://console.actions.google.com/u/[0]/project/[yourprojectId]/deviceregistration/) (change [] to your project) or [Manual registration](https://developers.google.com/assistant/sdk/reference/device-registration/register-device-manual))

4. In register steps(step 2), you can download your `credentials.json` for OAuth. Carefully store it in `MMM-GoogleAssistant` directory.
 - Or you can find your credentials from [Cloud Platform Console](https://console.cloud.google.com/) (Your Project > APIs & Services > Credentials)
5. In your SBC, you can run auth-tool for auth. (not via SSH)
```sh
cd ~/MagicMirror/modules/MMM-GoogleAssistant
node auth_and_test.js
```
   a. If you meet some errors related with node version, execute `npm rebuild` and try again.

   b. At first execution, this script will try opening a browser and getting permission of a specific user for using this Assistant. (So you'd better to execute this script in your RPI shell, not via SSH)

   c. After confirmation, Some code (`4/ABCD1234XXXXX....`) will appear in the browser. Copy that code and paste in your console's request (`Paste your code:`)

   d. On success, Prompt `Type your request` will be displayed. Type anything for testing assistant. (e.g; `Hello`, `How is the weather today?`)

   e. Now you can find `token.json` in your `MMM-AssistantGoogle` directory.

## `OAuth Consent Screen` setup
Sometimes, you might encounter some problem related to `OAuth Consent Screen missing`.
In that case, go to [Cloud Platform Console](https://console.cloud.google.com/), then navigate to `APIs & Services > OAuth Consent Screen`. At first, you'll be asked which user type would use your project. Just select `External`. The page will be changed to `OAuth consent screen`, but leave it as unverified. On dev stage, it's enough.


## Get `deviceModelId` and `deviceInstanceId`
> If you are not an experienced developer or don't need `gactions` implements, pass this section.

If you want not only pure Assistant embeding but also customized gactions for device, you might need to get `deviceModelId` and `deviceInstanceId`. To help understanding, **deviceModel** is something like `Volkswagen Golf` or `MagicMirror` and **deviceInstance** is something like `mom's car` or `mirror in living room`.

### For `deviceModelId`
You can get `deviceModelId` as a result of previous [register a device model](https://developers.google.com/assistant/sdk/guides/service/python/embed/register-device) step. In `Device registration` menu in `Actions Console`, you can find it.

### For `deviceInstanceId`
You need additional `google-assistant-sdk` library. See [
Manually Register a Device with the REST API](https://developers.google.com/assistant/sdk/reference/device-registration/register-device-manual#get-access-token) page.

