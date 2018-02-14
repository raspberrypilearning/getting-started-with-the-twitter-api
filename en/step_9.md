## Test the Twython Streamer

Another feature of the Twython library is the ability to listen out for tweets containing a certain term. You can perform a particular action when a matching tweet is found.

- Create another new file and import `TwythonStreamer` from the `twython` module:

    ```python
    from twython import TwythonStreamer
    ```

- Also, import the variables from `auth.py`:

    ```python
    from auth import (
        consumer_key,
        consumer_secret,
        access_token,
        access_token_secret
    )
    ```

    Save this file as `stream.py`.

- In order to perform a custom action when a tweet is found, you must modify the default behaviour of `TwythonStreamer`. Since `TwythonStreamer` is a class, we can extend it by creating a new class which inherits the functionality of `TwythonStreamer`, and we can modify any parts we need to. Start by creating the new class:

    ```python
    class MyStreamer(TwythonStreamer):
    ```

- The original `TwythonStreamer` class has a method (function) called `on_success`. This is the code which is run when a matching tweet is found. A simple example is to just print out the contents of a tweet found when we search the stream:

    ```python
    class MyStreamer(TwythonStreamer):
        def on_success(self, data):
            if 'text' in data:
                print(data['text'])
    ```

- Underneath your `MyStreamer` class definition, add some code to create an instance of your own streamer, and use the status filter to start tracking a particular term, like `raspberry pi`:

    ```python
    stream = MyStreamer(
        consumer_key,
        consumer_secret,
        access_token,
        access_token_secret
    )
    stream.statuses.filter(track='raspberry pi')
    ```

- When a tweet is found, it sends a collection of data about the tweet into the `on_success` method. `data` is a dictionary containing the tweet text, along with lots of metadata.

- Printing out `data['text']` just gives us the tweet text. Another example might be to print the username, followed by the tweet text. Modify your streamer's `on_success` method to change the behaviour, for example:

    ```python
    class MyStreamer(TwythonStreamer):
        def on_success(self, data):
            if 'text' in data:
                username = data['user']['screen_name']
                tweet = data['text']
                print("@{}: {}".format(username, tweet))
    ```

--- collapse ---

---
title: Completed code
---

```python
from twython import TwythonStreamer
from auth import (
    consumer_key,
    consumer_secret,
    access_token,
    access_token_secret
)

class MyStreamer(TwythonStreamer):
    def on_success(self, data):
        if 'text' in data:
            username = data['user']['screen_name']
            tweet = data['text']
            print("@{}: {}".format(username, tweet))

stream = MyStreamer(
    consumer_key,
    consumer_secret,
    access_token,
    access_token_secret
)
stream.statuses.filter(track='raspberry pi')
```

--- /collapse ---