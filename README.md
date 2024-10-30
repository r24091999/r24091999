package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class LoginPage {
    private WebDriver driver;

    private By usernameField = By.id("username");
    private By passwordField = By.id("password");
    private By loginButton = By.id("login");

    public LoginPage(WebDriver driver) {
        this.driver = driver;
    }

    public void login(String username, String password) {
        driver.findElement(usernameField).sendKeys(username);
        driver.findElement(passwordField).sendKeys(password);
        driver.findElement(loginButton).click();
    }
}
package tests;

import org.testng.Assert;
import org.testng.annotations.Test;
import pages.LoginPage;
import utils.BaseTest;

public class LoginTest extends BaseTest {

    public void testValidLogin() {
        LoginPage loginPage = new LoginPage(driver);
        loginPage.login("validUsername", "validPassword");
        
        Assert.assertTrue(driver.getCurrentUrl().contains("dashboard"));
    }
    public void testInvalidLogin() {
        LoginPage loginPage = new LoginPage(driver);
        loginPage.login("invalidUsername", "invalidPassword");

        String errorMessage = driver.findElement(By.id("error")).getText();
        Assert.assertTrue(errorMessage.contains("Invalid credentials"));
    }
}

// pages/HomePage.java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class HomePage {
    private WebDriver driver;

    public HomePage(WebDriver driver) {
        this.driver = driver;
    }

    // Locator for search bar
    private By searchBox = By.name("search");

    public void searchProduct(String product) {
        driver.findElement(searchBox).sendKeys(product);
        driver.findElement(searchBox).submit();
    }
}
// pages/ProductPage.java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class ProductPage {
    private WebDriver driver;

    public ProductPage(WebDriver driver) {
        this.driver = driver;
    }

    private By addToCartButton = By.id("add_to_cart");  // Change ID according to actual site

    public void addToCart() {
        driver.findElement(addToCartButton).click();
    }
}
// pages/CartPage.java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class CartPage {
    private WebDriver driver;

    public CartPage(WebDriver driver) {
        this.driver = driver;
    }

    private By cartItem = By.className("cart_item");  // Change locator as per site
    private By checkoutButton = By.id("checkout");

    public boolean isProductInCart() {
        return driver.findElements(cartItem).size() > 0;
    }

    public void proceedToCheckout() {
        driver.findElement(checkoutButton).click();
    }
}

