## Tweet a picture

Now that the Twitter connection has been tested, try to upload a picture.

- Find a picture, and copy or download it to your computer. Save it in the same directory as your program.

- Modify the code accordingly to change the message and open your image:

    ```python
    message = "Hello world - here's a picture!"
    image = open('image.jpg', 'rb')
    ```

    Make sure to change `image.jpg` to the name of your image file.

- Upload your image to Twitter and get the **media_id**, which you will need to send your tweet:

    ```python
    response = twitter.upload_media(media=image)
    media_id = [response['media_id']]
    ```

- Send the tweet with the uploaded image:

    ```python
    twitter.update_status(status=message, media_ids=media_id)
    ```

- Run the code and see if it tweets the text and image together!

    ![Tweet Image](images/tweet-image.png)

To take this further, you could take your own pictures with the [Camera Module](https://projects.raspberrypi.org/en/projects/getting-started-with-picamera) and tweet those.

--- collapse ---

---
title: Completed code
---

```python
from twython import Twython
from auth import (
    consumer_key,
    consumer_secret,
    access_token,
    access_token_secret
)

twitter = Twython(
    consumer_key,
    consumer_secret,
    access_token,
    access_token_secret
)

message = "Hello World - here's a picture!"

image = open('image.jpg', 'rb')
response = twitter.upload_media(media=image)
media_id = [response['media_id']]
twitter.update_status(status=message, media_ids=media_id)
print("Tweeted: " + message)
```

--- /collapse ---
