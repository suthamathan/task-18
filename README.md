# task-18
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

import java.util.concurrent.TimeUnit;

public class FacebookSignUpAutomation {

    public static void main(String[] args) {
        // Set the path to the chromedriver executable
        System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");

        // Create a Chrome browser instance
        WebDriver driver = new ChromeDriver();

        // Maximize the browser window
        driver.manage().window().maximize();

        // Navigate to Facebook website
        driver.get("https://www.facebook.com/");

        // Verify that the website is redirected to the Facebook homepage
        if (driver.getCurrentUrl().equals("https://www.facebook.com/")) {
            System.out.println("Successfully redirected to the Facebook homepage.");
        } else {
            System.out.println("Redirection to the Facebook homepage failed.");
            driver.quit();
            return;
        }

        // Click on the "Create new account" button
        WebElement createAccountButton = driver.findElement(By.xpath("//a[@data-testid='open-registration-form-button']"));
        createAccountButton.click();

        // Wait for the sign-up page to load
        driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);

        // Fill in the registration form
        driver.findElement(By.name("firstname")).sendKeys("Test");
        driver.findElement(By.name("lastname")).sendKeys("User");
        driver.findElement(By.name("reg_email__")).sendKeys("testuser@test.com");
        driver.findElement(By.name("reg_passwd__")).sendKeys("StrongPassword");

        // Select date of birth
        WebElement dayDropdown = driver.findElement(By.id("day"));
        WebElement monthDropdown = driver.findElement(By.id("month"));
        WebElement yearDropdown = driver.findElement(By.id("year"));

        dayDropdown.sendKeys("11");
        monthDropdown.sendKeys("May");
        yearDropdown.sendKeys("1985");

        // Select gender
        WebElement genderRadioButton = driver.findElement(By.xpath("//input[@type='radio' and @value='2']"));
        genderRadioButton.click();

        // Click on the "Sign Up" button
        WebElement signUpButton = driver.findElement(By.name("websubmit"));
        signUpButton.click();

        // Wait for the registration process to complete
        driver.manage().timeouts().implicitlyWait(15, TimeUnit.SECONDS);

        // Verify that the user is successfully registered and redirected to the Facebook homepage
        if (driver.getCurrentUrl().equals("https://www.facebook.com/")) {
            System.out.println("User successfully registered and redirected to the Facebook homepage.");
        } else {
            System.out.println("Registration process failed.");
        }

        // Close the browser
        driver.quit();
    }
}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;

public class DragAndDropAutomation {

    public static void main(String[] args) {
        // Set the path to the chromedriver executable
        System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");

        // Create a Chrome browser instance
        WebDriver driver = new ChromeDriver();

        // Maximize the browser window
        driver.manage().window().maximize();

        // Navigate to QueryUI droppable website
        driver.get("https://jqueryui.com/droppable/");

        // Switch to the iframe containing the droppable elements
        driver.switchTo().frame(driver.findElement(By.cssSelector("iframe.demo-frame")));

        // Find the source element and the target element
        WebElement sourceElement = driver.findElement(By.id("draggable"));
        WebElement targetElement = driver.findElement(By.id("droppable"));

        // Perform the drag-and-drop operation
        Actions actions = new Actions(driver);
        actions.dragAndDrop(sourceElement, targetElement).perform();

        // Verify that the drag and drop operation is successful by checking the color property
        String targetElementColor = targetElement.getCssValue("color");
        if (targetElementColor.equals("rgba(0, 128, 0, 1)")) {
            System.out.println("Drag and drop operation is successful. Target element color is green.");
        } else {
            System.out.println("Drag and drop operation failed.");
        }

        // Verify that the text of the target element has changed to "Dropped!"
        String targetElementText = targetElement.getText();
        if (targetElementText.equals("Dropped!")) {
            System.out.println("Text of the target element has changed to 'Dropped!'");
        } else {
            System.out.println("Text of the target element did not change.");
        }

        // Close the browser
        driver.quit();
    }
}
