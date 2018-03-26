## Set the system date/time

Your system date/time will be need to be set correctly in order to connect to Twitter.

For most operating systems it will be set from the internet, but it may be set to manual or the wrong timezone.

If its correct you can skip to the next step.

--- collapse ---

---
title: Setting the time on a Raspberry Pi
---

- Set the timezone in the **Raspberry Pi Configuration Tool**.

![pi configuration](images/pi_configuration.PNG)

- If the date/time is still wrong, open a terminal window and enter the following command with the current time and date:

    ```bash
    sudo date -s "31 APR 2015 09:26:53"
    ```
--- /collapse ---

--- collapse ---

---
title: Setting the time on Windows
---

- Right-click on the time and date on the taskbar

- Select **Adjust date/time** from the Menu

![windows set time](images/windows_set_time.PNG)

--- /collapse ---

---
title: Setting the time on MacOS
---

- Click Menu, System Preferences, Date and Time

--- /collapse ---


