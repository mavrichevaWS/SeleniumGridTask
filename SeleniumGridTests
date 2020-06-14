using System;
using System.Collections.Generic;

using NUnit.Framework;

using OpenQA.Selenium;
using OpenQA.Selenium.Remote;

using OpenQA.Selenium.Chrome;
using OpenQA.Selenium.Firefox;

namespace WebDriverTasks
{
    [TestFixture]
    public class WebDriverTasks
    {
        // Options select test
        [Test]
        public void MultiselectTest()
        {
            RemoteWebDriver driver;
            ChromeOptions Options = new ChromeOptions();
            Options.PlatformName = "windows";
            Options.AddAdditionalCapability("platform", "WIN8_1", true);
            Options.AddAdditionalCapability("version", "latest", true);

            // We configure launch remotely in a current machne using node 
            driver = new RemoteWebDriver(new Uri("http://192.168.100.4:5555/wd/hub/"), Options.ToCapabilities(), TimeSpan.FromSeconds(600)); // NOTE: connection timeout of 600 seconds or more required for time to launch grid nodes if non are available

            try {
                driver.Manage().Window.Maximize();
                driver.Navigate().GoToUrl(UserConstantData.URL1);
                driver.Manage().Timeouts().ImplicitWait = new TimeSpan(5000);

                string state1 = "California";
                string state2 = "New York";
                string state3 = "Pennsylvania";

                IList<IWebElement> elements = driver.FindElements(By.CssSelector("select[name='States'] > option:nth-child(3n+1)"));
                foreach (IWebElement e in elements)
                {
                    e.Click();
                    if (e.Selected)
                    {
                        Assert.IsTrue(e.Text == state1 || e.Text == state2 || e.Text == state3);
                        Console.WriteLine("Value of the option item is selected: " + e.Selected + " " + e.Text);
                    }
                }
            }
            finally {
                Console.WriteLine("Driver session: " + driver.SessionId);
                driver.Close();
            }
        }

        // Confirm box test
        [Test]
        public void ConfirmBox()
        {
            RemoteWebDriver driver;
            FirefoxOptions Options = new FirefoxOptions();
            Options.PlatformName = "windows";
            Options.AddAdditionalCapability("platform", "VISTA", true);
            Options.AddAdditionalCapability("version", "77", true);

            // We configure launch remotely in a virtual machine Oracle VM (Windows 7)
            driver = new RemoteWebDriver(new Uri("http://10.0.2.15:5557/wd/hub/"), Options.ToCapabilities(), TimeSpan.FromSeconds(600)); // NOTE: connection timeout of 600 seconds or more required for time to launch grid nodes if non are available

            try
            {
                driver.Manage().Window.Maximize();
                driver.Navigate().GoToUrl(UserConstantData.URL2);
                driver.Manage().Timeouts().ImplicitWait = new TimeSpan(5000);

                IWebElement searchConfirmButton = driver.FindElement(By.CssSelector("button[onclick='myConfirmFunction()']"));
                searchConfirmButton.Click();

                var confirm = driver.SwitchTo().Alert();
                confirm.Accept();

                IWebElement clickResult = driver.FindElement(By.Id("confirm-demo"));
                Console.WriteLine(clickResult.Text);
                if (clickResult.Text == "You pressed OK!") Console.WriteLine("Confirm test successful");
            }
            finally
            {
                Console.WriteLine("Driver session: " + driver.SessionId);
                driver.Close();
            }
        }
    }
}
