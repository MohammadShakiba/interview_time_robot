
# Interview Time Robot

Hey everyone!

So, at the end of January, a friend reached out asking if I could build a robot to help her snag an F-1 visa interview slot at a U.S. embassy in Canada. What an idea, right? 😄 I wasn’t sure at first if I could pull it off, but I had some experience using Python’s Selenium package for automating web browsing (nothing shady or illegal, I promise!).

I coded the robot that same day, and in just a few hours, I managed to book her an interview for that month. Since then, I’ve reused the code to help a few others get interview slots at different embassies (Armenia, Dubai, Canada). Now, more people are asking for help, so I figured, why not share it with everyone?

I know there are companies that charge for this service—and hey, I get it, people will pay to make sure they can get to the U.S.! 😊 In my humble opinion, those companies are probably using Selenium or some other automation tool, maybe sending HTTP `POST` and `GET` requests with `curl` or `requests`. But I’m not 100% sure since the U.S. visa system doesn’t provide an API. Plus, the site is pretty secure and might block you if you log in or refresh too many times. Still, you can try tracking things using Postman or your browser’s Network tab if you’re curious.

Just a heads up: this robot is **MINIMAL**—it just automates the basic process a human would follow to reserve an interview. It’s **NOT OPTIMIZED**. You can use it for a few weeks to see if it helps you land an interview slot. If not, you can go ahead and request a service from those companies!

Before we dive into how it works, I should note: this code comes with **NO SUPPORT**. If you’re not familiar with Python, you might want to consult someone who is, and make sure you have Python and Jupyter installed. The code is pretty simple, and you’ll just need to `inspect` elements on the website. The comments in the code should guide you. If you get stuck, ChatGPT is always there to help! 😄 The best way to find elements is by using XPATH.

If you're using a newer version of Selenium, you might see an error about `find_element_by_xpath` not working. Here’s the fix:

```python
from selenium.webdriver.common.by import By
```
Then replace `find_element_by_xpath` with `find_element`, like this:

```python
email = driver.find_element_by_xpath('//*[@id="user_email"]')
```

becomes:

```python
email = driver.find_element(By.XPATH, '//*[@id="user_email"]')
```

I wrote this in Jupyter Notebook because it gives you more flexibility for debugging and finding elements, and you won’t lose your variables. You can export it to a `.py` file with `jupyter nbconvert --to script Canada.ipynb`, but I personally prefer Jupyter!

Make sure to download `geckodriver` if you’re using Firefox, or the Chrome WebDriver for Chrome, and place it in the same folder as your code. If you’re using WSL or Linux/Ubuntu, you can move the executables to `/usr/bin` or add them to your `$PATH`. Honestly, it's easiest to run this on Windows with Firefox (just download `geckodriver`).

If you're using a Mac with Safari, you need to do the following:
- Run Jupyter as `sudo` from the terminal.
- Add a cell at the top with this code:
  
```bash
!sudo safaridriver --enable
```

and run it! But one important thing—don’t touch anything while it’s running in Safari! 😅

If some elements aren’t found, re-inspect them in the same browser that you're running the code (right-click on the element, like “Reschedule” and select “Inspect”).

This code is specifically for **RESCHEDULING** interview times, so you need to have paid and scheduled an initial appointment before using it.

There is also another line in the code for which you can have control over the time it has selected:
```python
if int(date_of_app.get_attribute('value').split('-')[1])<=12 and date_of_app.get_attribute('value').split('-')[0]=='2024':
```
Then it will click on the Reschedule botton!

## Some Ideas

I’ve used quite a few `time.sleep()` calls, and they’re not really optimized. You might find some of them unnecessary or reduce the sleep time.

You can also use Postman to track the `POST` and `GET` requests, figure out how to set tokens in `curl`, and maybe automate it using Python’s `requests` library.

**NOTE**: I really hope this works for you! If you manage to optimize it or make the instructions clearer, feel free to submit a pull request, and I’d be happy to check it out!


Here's a GIF showing how it's looking for empty slots! If it doesn't show check the `robot_demo.gif` file!

[Interview Robot Demo](./robot_demo.gif)

