# Getting started with the Twitter API

A guide to connecting to Twitter from Python using Twython.

## Create a Twitter account

If you don't already have a Twitter account, you'll need to create one.

1. Create a Twitter account at [twitter.com](https://twitter.com).

    ![Create Twitter account](images/create-twitter.png)

You might also want to upload a photo and fill out the bio.

## Create a Twitter application

You need to register your application with Twitter to get keys; these allow you to access the Twitter account from Python using the Twitter API (Application Programming Interface).

1. Go to [apps.twitter.com](https://apps.twitter.com) and click the **Create New App** button.

    ![Create new app](images/create-new-app.png)

1. Complete the application details form. You must enter an application name, description, and website (this can be `https://www.raspberrypi.org/` if you don't have one). Leave the 'Callback URL' field blank and proceed.

    ![App details](images/app-details.png)

1. Modify your app permissions from **Read only** to **Read and write**.

    ![Read and write](images/read-and-write.png)

1. Click the 'Keys and Access Tokens' tab and create an access token.

1. Once you've clicked the **Create an Access Token** button, refresh the page and you'll see a new section beneath the **Application Settings** with your access token details.

1. You should now be able to see your **Consumer key**, **Consumer secret**, **Access token**, and **Access token secret**. You'll need these four keys to connect to your Twitter account from your Python code. Don't share these keys with anyone, as they can be used without the account's password. If you share your code online, make sure not to include these keys. If you ever accidentally share or publish these keys, you should regenerate the keys at [apps.twitter.com](https://apps.twitter.com).

![Twitter keys](images/twitter-keys.png)

## Set the system date/time

You'll need to make sure your system date/time is set correctly in order to connect to Twitter.

1. Check your Raspberry Pi's system time is correct. It's usually set from the internet, but it may be set to the wrong timezone or may not have been set correctly. If it's correct, you can skip to the next step.

1. Set the timezone in the **Raspberry Pi Configuration Tool**.

1. If the date/time is still wrong, open a terminal window and enter the following command with the current time and date:

    ```bash
    sudo date -s "1 MAY 2016 12:00:00"
    ```

## Send a tweet from Python

Now you have your API keys, and your date/time is set correctly, you're ready to send a tweet from Python!

1. Open Python 3 from the Programming menu.

1. Create a new file and paste your API keys from [apps.twitter.com](https://apps.twitter.com) into variables, like so:

    ```python
    consumer_key        = 'ABCDEFGHIJKLKMNOPQRSTUVWXYZ'
    consumer_secret     = '1234567890ABCDEFGHIJKLMNOPQRSTUVXYZ'
    access_token        = 'ZYXWVUTSRQPONMLKJIHFEDCBA'
    access_token_secret = '0987654321ZYXWVUTSRQPONMLKJIHFEDCBA'
    ```

1. Save the file as `auth.py`.

1. Create another new file and import `Twython` from the `twython` module:

    ```python
    from twython import Twython
    ```

1. Also, import the variables from `auth.py`:

    ```python
    from auth import (
        consumer_key,
        consumer_secret,
        access_token,
        access_token_secret
    )
    ```

    Save this file as `twitter.py`.

1. Make a connection with the Twitter API using this set of keys:

    ```python
    twitter = Twython(
        consumer_key,
        consumer_secret,
        access_token,
        access_token_secret
    )
    ```

1. Start with a basic "Hello world" tweet to test the connection works:

    ```python
    message = "Hello world!"
    twitter.update_status(status=message)
    print("Tweeted: %s" % message)
    ```

    This uses the API's `update_status()` function to send a tweet containing the text "Hello world!".

1. Now save (`Ctrl + S`) and run with `F5`. You should see the message "Tweeted: Hello world!". Go to your Twitter profile in a web browser to verify it was sent! This will be at `twitter.com/username`, where `username` is your Twitter account's username.

![Twitter Hello World](images/twitter-hello-world.png)

Note that sending multiple tweets with the exact same text are classed as duplicates and rejected by Twitter. If you want to test it again, try tweeting a different message.

If you see an error, your API keys may be incorrect. Be sure to copy them exactly and check the spelling of the variables. You should also check that your Pi is connected to the internet.

![Twitter API Error](images/twitter-api-error.png)

## Tweet random messages

Now that we can send some text as a tweet, let's mix it up a bit.

1. First, import the random module:

    ```python
    import random
    ```

    This module contains a `choice` function, which takes a list and returns a single entry at random.

1. Now create a list of messages, like so:

    ```python
    messages = [
        "Hello world",
        "Hi there",
        "What's up?",
        "How's it going?",
        "Have you been here before?",
        "Get a hair cut!",
    ]
    ```

1. Replace `message = "Hello world!"` with `message = random.choice(messages)`. This chooses a single item from the `messages` list at random.

1. Run the code again two or more times to see different messages being tweeted at random.

## Tweet a picture

Now that the Twitter connection has been tested, try to upload a picture.

1. Find a picture, copy it to your Raspberry Pi or download it from the internet, and save it. Make a note of its location (something like `/home/pi/Downloads/image.jpg`).

1. Modify the code accordingly:

    ```python
    message = "Hello world - here's a picture!"
    with open('/home/pi/Downloads/image.jpg', 'rb') as photo:
        twitter.update_status_with_media(status=message, media=photo)
    ```

    Make sure to specify the full path to the image correctly.

    This opens the file and uses the `update_status_with_media()` function to upload the image, along with the tweet text.

1. Run the code and see if it tweets the text and image together!

    ![Tweet Image](images/tweet-image.png)

To take this further, you could take your own pictures with the camera module and tweet those.

## Test the Twython Streamer

Another feature of the Twython library is the ability to listen out for tweets containing a certain term. You can perform a particular action when a matching tweet is found.

1. Create another new file and import `TwythonStreamer` from the `twython` module:

    ```python
    from twython import TwythonStreamer
    ```

1. Also, import the variables from `auth.py`:

    ```python
    from auth import (
        consumer_key,
        consumer_secret,
        access_token,
        access_token_secret
    )
    ```

    Save this file as `stream.py`.

1. In order to perform a custom action when a tweet is found, you must modify the default behaviour of `TwythonStreamer`. Since `TwythonStreamer` is a class, we can extend it by creating a new class which inherits the functionality of `TwythonStreamer`, and we can modify any parts we need to. Start by creating the new class:

    ```python
    class MyStreamer(TwythonStreamer):
    ```

1. The original `TwythonStreamer` class has a method (function) called `on_success`. This is the code which is run when a matching tweet is found. A simple example is to just print out the contents of a tweet found when we search the stream:

    ```python
    class MyStreamer(TwythonStreamer):
        def on_success(self, data):
            if 'text' in data:
                print(data['text'])
    ```

1. Underneath your `MyStreamer` class definition, add some code to create an instance of your own streamer, and use the status filter to start tracking a particular term, like `raspberry pi`:

    ```python
    stream = MyStreamer(
        consumer_key,
        consumer_secret,
        access_token,
        access_token_secret
    )
    stream.statuses.filter(track='raspberry pi')
    ```

1. When a tweet is found, it sends a collection of data about the tweet into the `on_success` method. `data` is a dictionary containing the tweet text, along with lots of metadata.

1. Printing out `data['text']` just gives us the tweet text. Another example might be to print the username, followed by the tweet text. Modify your streamer's `on_success` method to change the behaviour, for example:

    ```python
    class MyStreamer(TwythonStreamer):
        def on_success(self, data):
            if 'text' in data:
                username = data['user']['screen_name']
                tweet = data['text']
                print("@%s: %s" % (username, tweet))
    ```

## What next?

- Make a [Tweeting Babbage](https://www.raspberrypi.org/learning/tweeting-babbage/)
- Make your own Twitter bot
- Tweet some information from sensors from the Sense HAT or GPIO components
- Use the Sense HAT or GPIO components to light up lights or drive motors when a term is tweeted
- Use the Twython Streamer to poll which terms are more popular than others
- Make a Twitter-controlled robot
