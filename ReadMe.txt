_________________________________________________________________________________________________

Page Object Model example
________________________________________________________________________________________________________________

using OpenQA.Selenium;
using STAF.Framework.BaseClasses;

namespace WAF.Pages
{
	class YourClass
	{
		#region Elements
		static internal By element = By.XPath("");

		#endregion

		#region Actions
		public static void VerifyPageElements()
		{
			VerifyElement.IsPresent(element);
		}

		#endregion

		#region Navigation
		public static void NavigateToPage()
		{
			Driver.ClickOn(element);
			VerifyElement.AreEqual(element, "");
		}

		#endregion
	}
}


________________________________________________________________________________________________________________

Test Case class example
________________________________________________________________________________________________________________

	[TestFixture]
	class YourClass : BaseSetup
	{
		[Test]
		public void Test_01()
		{

		}
	}

________________________________________________________________________________________________________________

Action methods
________________________________________________________________________________________________________________

	Driver.ClickOn(locator);
	Driver.PressEnter(locator);
	Driver.InsertText(locator, "");
	Driver.SelectDropdown(locator, "");
	Driver.WaitForElement(locator);
	Driver.Wait(2);

	VerifyElement.AreEqual(locator, "");
	VerifyElement.IsPresent(locator);
	VerifyElement.IsNotPresent(locator);
	VerifyElement.TitleIsPresent("");
	VerifyElement.ButtonIsDisabled(locator);
	VerifyElement.ElementPresentBool(locator);

	Browser.Open();
	Browser.NavigateToUrl(url);
	Browser.Close();
	Browser.Maximize();
	Browser.GoBack();
	Browser.RefreshPage();
	Browser.SwitchToWindow();
	Browser.SwitchToParent();
	Browser.SwtichToIFrame();
	Browser.ScrollToElement(location);

________________________________________________________________________________________________________________

XPath samples
________________________________________________________________________________________________________________

//button[normalize-space(text())='Sign In']

//button[contains(., 'Save')]

(//button[@id='dropdownMenu1'])[2]

//input[@value='Save']

//th[contains(., 'Description')]

//th[normalize-space(text())='Description']

//a[@href='/MCCDashboardTest/ReleaseNotes']

//tr[10]/td[2][normalize-space(text())='Discussion Topic']

//tr/td[normalize-space(text())='Labs/Procedures']//following-sibling::td[2][normalize-space(text())='Immediately']

//tbody/tr[2]/td[2][contains(., 'Abc Automation')]//preceding-sibling::td[1]/input

//ul[@class=' ']/li[contains(., ' ')]

// 	Select button with user name
//td[normalize-space(text())='User, Auto']//following-sibling::td/button


//	Message popup
//div[@class='toast-message']

// 	Checkbox with Label
//label[contains(., 'Administrator')]//preceding-sibling::div

//  Select with Partial Attribute
//ul[contains(@style,'display: block;')]



________________________________________________________________________________________________________________

Script samples
________________________________________________________________________________________________________________

// Dismiss the Print popup window

			IAlert alert = Browser.Instance.SwitchTo().Alert();
			alert.Dismiss();

**************************************************************
// Select the checkbox if its not been selected.

			if (!Instance.FindElement(locator).GetAttribute("aria-checked").Equals("true"))
			{
				Instance.FindElement(locator).Click();
			}

***************************************************************
// Convert Date to different format

DateTime.Parse("05/22/2017").ToString("dddd MMM dd, yyyy")
// Get todays date
string todaysEndDate = DateTime.Now.ToString("dddd MMMM dd, yyyy");

*****************************************************************

// Read total rows and verify

            // Row path
            By xPath = By.XPath("//tr[@ng-repeat='set in Settings track by $index']");
            // Collect total rows
            IReadOnlyCollection<IWebElement> collection = Browser.Instance.FindElements(xPath);
            // Convert to String
            string totalRow = collection.Count.ToString();
            // Verify 
            VerifyElement.AreEqual(totalSettings, "Total " + totalRow + " Settings");

******************************************************************************************************

// Global String 

static string globalString = null;

    [Test, Order(1)]
    public void Test1()
    {
        string claimNumber = SuspendClaim();
        globalString = claimNumber;
    }
    [Test, Order(2)]
    public void Test2()
    {
		System.Console.WriteLine(globalString);        
    }

	// Method to get the other string 

	internal static string SuspendClaim()
        {
            string claimNumber = Browser.Instance.FindElement(VerifySidebarMenu.claimNumber).Text;
            return claimNumber;
        }

******************************************************************************************************