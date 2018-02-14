## Create a Twitter application

You need to register your application with Twitter to get keys; these allow you to access the Twitter account from Python using the Twitter API (Application Programming Interface).

- Go to [apps.twitter.com](https://apps.twitter.com) and click the **Create New App** button.

    ![Create new app](images/create-new-app.png)

- Complete the application details form. You must enter an application name, description, and website (this can be `https://www.raspberrypi.org/` if you don't have one). Leave the 'Callback URL' field blank and proceed.

    ![App details](images/app-details.png)

- Accept the Developer Agreement.

    ![developer agreement](images/dev_agreement.png)

- Click the **Create your Twitter Application** button.

You may receive the error _"You must add your mobile phone to your Twitter profile before creating an application"_, if so follow the instructions to add a mobile phone to your twitter profile.

The application details page will then appear, showing you all the information about your app.

- Check the **access level** in Application Settings is set to **Read and write**.

    ![Read and write](images/application-settings.png)

- Click the **Keys and Access Tokens** tab to view your keys and access tokens.

    ![keys and access tokens](images/keys-and-access-tokens.png)

- Click the **Create my access token** button.

    ![create access token](images/create-access-token.png)

- Once you've clicked the **Create an Access Token** button, refresh the page and you'll see a new section beneath the **Application Settings** with your access token details.

- You should now be able to see your **Consumer key**, **Consumer secret**, **Access token**, and **Access token secret**. You'll need these four keys to connect to your Twitter account from your Python code. Don't share these keys with anyone, as they can be used without the account's password. 

If you share your code online, make sure not to include these keys. 

If you ever accidentally share or publish these keys, you should regenerate the keys at [apps.twitter.com](https://apps.twitter.com).

![Twitter keys](images/twitter-keys.png)

