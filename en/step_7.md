## Tweet random messages

Now that we can send some text as a tweet, let's mix it up a bit.

- First, import the random module:

    ```python
    import random
    ```

    This module contains a `choice` function, which takes a list and returns a single entry at random.

- Now create a list of messages, like so:

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

- Replace `message = "Hello world!"` with `message = random.choice(messages)`. This chooses a single item from the `messages` list at random.

- Run the code again two or more times to see different messages being tweeted at random.

