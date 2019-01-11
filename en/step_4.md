## Create a Twitter application

After your developer account has been approved, you will need to register your application with Twitter to get keys; these allow you to access the Twitter account from Python using the Twitter API (Application Programming Interface).

- Go to [developer.twitter.com](https://developer.twitter.com), select **Apps** from the menu and click the **Create and App** button.

    ![screenshot of the apps page with the apps link in the menu and the create app button highlighted](images/create_app1.png)

- Complete the application details form. You must enter an app name, description, website (this can be *https://www.raspberrypi.org/* if you don't have one) and some information about *how the app will be used*. You can leave the other fields blank and click **Create**.

    ![screenshot of the Create an App page](images/create_app2.png)

- Review the Developer Terms and click **Create**.

    ![screen shot of developer terms popup](images/create_app3.png)

- Click the **Keys and Access Tokens** tab to view your keys and access tokens.

- Click the **Create** button under *Access token & access token secret*.

    ![screenshot of apps keys and tokens page with tab and create button selected](images/create_app4.png)

- You should now be able to see your **Consumer API key**, **Consumer API secret key**, **Access token**, and **Access token secret**. You'll need these four keys to connect to your Twitter account from your Python code. Don't share these keys with anyone, as they can be used without the account's password. 

If you share your code online, make sure not to include these keys. 

If you ever accidentally share or publish these keys, you should regenerate the keys at [developer.twitter.com](https://developer.twitter.com).

![Twitter keys](images/create_app5.png)

