# webscraping
from selenium import webdriver
from selenium.webdriver.common.by import By
import time

driver = webdriver.Chrome()
driver.get("https://www.amazon.in/")
driver.maximize_window()

search_box = driver.find_element(By.ID, "twotabsearchtextbox")
search_box.send_keys("smartphones under 10000")
time.sleep(2)

search_button = driver.find_element(By.ID, "nav-search-submit-button")
search_button.click()
# scraping the products
products = []

for i in range(10):
    print('Scraping page', i + 1)

    product_elements = driver.find_elements(By.XPATH, "//span[@class='a-size-medium a-color-base a-text-normal']")

    for product in product_elements:
        products.append(product.text)

    next_button = driver.find_element(By.CLASS_NAME, "s-pagination-next")
    next_button.click()
    time.sleep(5)

print("Number of products:", len(products))
print("Products:", products[:5])

driver.quit()
