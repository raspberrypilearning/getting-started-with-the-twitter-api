## Tweet a picture

Now that the Twitter connection has been tested, try to upload a picture.

- Find a picture, copy it to your Raspberry Pi or download it from the internet, and save it. Make a note of its location (something like `/home/pi/Downloads/image.jpg`).

- Modify the code accordingly to change the message and open your image:

    ```python
    message = "Hello world - here's a picture!"
    image = open('/home/pi/Downloads/image.jpg', 'rb')
    ```

    Make sure to specify the full path to the image correctly.

- Upload your image to twitter and get the **media_id** which you will use when sending your tweet:

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

To take this further, you could take your own pictures with the camera module and tweet those.

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

image = open('/home/pi/Downloads/image.jpg', 'rb')
response = twitter.upload_media(media=image)
media_id = [response['media_id']]
twitter.update_status(status=message, media_ids=media_id)
print("Tweeted: " + message)
```
