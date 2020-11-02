Automating input fields can be a pain. If `element.send_keys('text')` isn't 
working, try these techniques.

1. Be sure you're actually targeting the input field rather than a div wrapper
2. Try clicking the field first (some pages seem to have it read-only until 
   it's clicked)  
```
element.click()
element.send_keys('text')
```
3. Sometimes adding `element.clear()` after `element.click()` helps
4. If it still doesn't work, try using [action chains](https://selenium.dev/selenium/docs/api/py/webdriver/selenium.webdriver.common.action_chains.html)  
```
action_chains = ActionChains(driver)
action_chains.move_to_element(element)
action_chains.send_keys('text')
action_chains.perform()
```

5. I've [heard](https://stackoverflow.com/a/14577670) that using pyWinauto may 
   work as a workaround if all else fails, but I haven't tried it. Usually my 
   test environments are Linux anyway so this really is a last resort as it's 
   obviously Windows-only.  
```
driver = webdriver.Firefox()
element = driver.find_element_by_name('element_name')
element.clear()
app = Application.Application()
app.window_(title_re='*.Firefox.*').TypeKeys('text')
```
