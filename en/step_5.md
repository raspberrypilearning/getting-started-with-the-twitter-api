## Set the system date/time

You'll need to make sure your system date/time is set correctly in order to connect to Twitter.

- Check your Raspberry Pi's system time is correct. It's usually set from the internet, but it may be set to the wrong timezone or may not have been set correctly. If it's correct, you can skip to the next step.

- Set the timezone in the **Raspberry Pi Configuration Tool**.

- If the date/time is still wrong, open a terminal window and enter the following command with the current time and date:

    ```bash
    sudo date -s "1 MAY 2016 12:00:00"
    ```

