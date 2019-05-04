Selenium Installation

What is Selenium? https://www.seleniumhq.org/
Selenium is a tool to test your web application. You can do this in various ways, for instance
1-Permit it to tap on buttons
2-Enter content in structures
3-kim your site to check whether everything is "OK" and so on.

Installing selenium 
1-Download chromedriver based on your Google Chrome Version (Help>About Google Chrome)
https://chromedriver.storage.googleapis.com/index.html?path=74.0.3729.6/

2-Open terminal
a-Move the chromedriver to the following location /usr/local/bin 
b-type in ChromeDriver

3-Jupyter Notebook (# Dependencies)
a-from selenium import webdriver
b-from selenium.webdriver.common.keys import Keys
c-from selenium.webdriver.support.ui import WebDriverWait

4-Code to press a button (Type in your button Class Name inside the Quotation Marks)
button = driver.find_element_by_class_name('Class Name')
button.click()
