# readmetest

1. #Automation Framework

2. ##Project description
	* This is a generic C# Specflow/Nunit framework for usage on Edge projects
	* This framework uses the following technologies, all of which are open source:
		* BODI 
		* C# - 6.0 .Net Core
		* Gherkin
		* Log4Net
		* Selenium 
		* Specflow
		* SpecRun.Nunit
		* Nunit v3.*

3. ##Steps for installation
	* Things to check:
		* We must ensure that the version of the browsers that is installed on the machine is correct for this project.
		* We have a working version of Visual Studio installed with all of the required additional software, see screenshot below
		* The correct level of access to the repository   
	* Clone the Repo:
		* Open Visual Studio 
		* Click "Clone a repository" on the right hand side in the "Getting Started" section
		* Paste the repo URL into the "Repository Location" field and click clone
	* Build the project
		* Right-click on the project in the solution explorer which by default will be on the right hand pane of the screen
		* Click "Build"
		* If there are build errors reach out to an automation engineer for assistance
	* Install Specflow extension
		* Click on the extensions dropdown menu at the top of the Visual Studio window
		* Click "Manage Extensions", the "Manage Extensions" window will appear
		* Search for "SpecFlow for Visual Studio" and install
	* Create a Specflow account - You will not be able to run Specflow scenarios unless this is performed
		* In the "Test Explorer" pane right-click on a scenario and click run.  If there is no "Text Explorer" pane 
		  click "View" and click the "Test Explorer" option
		* At the bottom of the screen there will be a window named "Output", change the "Show output from" option to "tests"
		* Scroll through the output until you see a message that instructs you to create a Specflow account, there will be a link to the 
		  Specflow account creation page.
		* Click the link
		* Sign up with an email address, I would recommend creating a new email address for this purpose to avoid cluttering up a work email address with emails from Specflow
		* Once the account has been created and linked to Specflow you will be prompted to return to Visual Studio
	* Clean, Build & Run Tests
		* We should now have all of he required set up for you to run your first test.
		* First we will clean the solution, we do this by right-clicking on the project and selecting "Clean"
		* Next we build the solution as we did before
		* Now we run a test scenario as we attempted to before by right-clicking on a test in the "Test Explorer" pane and clicking "Run"
		* The scenario should run without any issues.  If any issues arise please reach out to an automation engineer for support.	

4. ##Framework Details
	* Framework Structure
		* BaseClass - The BaseClass contains the differnt browser configurations such as; Chrome, Edge, Firefox & Remote Driver's.
		* Hooks - This class contains before & after steps for the following:
			* Before/After Test Run
			* Before/After each Feature
			* Before/After each Scenario
			* Before/After each Step
		* Features - Feature files are where the scenarios are created using Gherkin language
		* Step Definition - Step definitions contains the code for each step inside the corresponding feature file.

		* Framework split into applicant, reviewer, API & Set up tests(advanced reporting) tests
			* Set up tests (Smoke Tests)
				* The set up tests are primarily used as Smoke Tests once the environment has been refreshed, these tests also create any features that may require other tests to run . E.g. Users will be created to use as part of login tests.
				(Setup folders structure screenshots)
			* Applicant Folder - These folders contain all test scenarios relating to the applicant site. Such as:
				* Applicant login
				* Project creation/submission
				* Track Changes
				* Auto-Roles
				(Screnshots applicantfolders structure)
			* Reviewer Folders - These folders contain all test scenarios relating to the reviewer site. Such as:
				* Login Scenarios
				* Advanced Reporting - UI Scenarios
				* Alert Scenarios
				* Applicant Role Scenarios
				* Application Type Scenarios
				* Auto-Roles Scenarios
				* Committee Scenarios
				* Create Meeting Scenarios
				* Custom Data Scenarios
				* Form Scenarios
				* Project Scenarios
				* Reviewer Type Scenarios
				* Roles Scenarios
				* Statuses
				* Documents (Upload & Delete)
				* User Creation						
			* API Folders - These folders contain test scenarios relating to the Advanced Reporting tree structure, include testing creation of reports using the different Themes; Meeting, User, Submissions, Project, Submission Contact.						
				
		* Utilities Folders - These include helper methods such as:
			* Api Helpers - Inside this folder are the helper methods for API scenarios.				
			* Component Helpers - Inside this folder will be helper methods for the following:
				* File Reader
				* Input Actions (e.g. Enter Data, Click button, selecting item from dropdown)
				* Page Actions (e.g. Get Title, Scroll to elements, navigate to URL)
				* Log4Net (Helper methods for logging output)
				* Generic Helper (Wait methods, Get elements, verifcation text)
				* File Readers
				***(Screenshots)
			* Table Classes
			
		* Allure Config - This file contains configuration for allure reporting 
		* App.config file has the following settings where the value can be edited:
			* Browser - There are multiple options that can be chosen for the browser, depending on what browser you would like tests to be run. Options are as follows:
				* Chrome
				* Edge
				* Firefox
				* Remote
				* API
			* Username - The value here can be changed to the email of the user that will be performing automated tests
			* Password - User password
			* PageLoadTimeOut - Sets value of how long the test steps will run for before timing out
			* ApplicantUrl - Set value to the URL of the Applicant site
			* ReviewerUrl - Set Value to the URL of the Reviewer Site
      
		### Example
		```xml
			
		<appSettings>
			<add key="Browser" value="Chrome" />
			<add key="RemoteCapabilities" value="" />
			<add key="Username" value="conor.thomson@edgetesting.co.uk" />
			<add key="Password" value="Infonetica@123" />
			<add key="PageLoadTimeout" value="30" />
			<add key="ApplicantUrl" value="https://edge-live.forms.ethicalreviewmanager.com" />
			<add key="ReviewerUrl" value="https://edge-live.review.ethicalreviewmanager.com" />
		</appSettings>
			
		```
		* Faker API - This is used to create random data that is used for different things inside the framework (e.g. Creating new User name or Form name). The Faker data that is generated will be different each time the code is run, which allowed us to decrease the risk of duplicating the names of forms, projects etc. See example code:
		 ** SCreenshot of Faker - (Copy User creation)
		 ### Example
		 ```csharp
		 
		int randint = Faker.RandomNumber.Next(100);
		string firstname = Faker.Name.First(); 
		string lastName = Faker.Name.Last(); 
		string emailid = Faker.Internet.Email(firstname); 
		string password = "Infonetica@" + randint;
		string organisation = Faker.Internet.DomainName(); 
		string department = Faker.Internet.DomainWord();
		string number = Faker.Phone.Number();
		string address = Faker.Address.StreetAddress();
		string town = Faker.Address.City();
		string postcode = Faker.Address.UkPostCode();
			
		 ```
		* Scenario Context - Scenario Contexts has been used throughout the framework. It is used to store data values, so these values can be used later in the scenario. This helps us as we do not need to hardcode any values, we can just use the scenario context throughout.
		(Scenario context screenshiot)
5. ##Branching Strategy
	* We will follow a GitHub - Flow branching strategy, please click the link for more info 
	[GitHub - Flow](https://docs.github.com/en/get-started/quickstart/github-flow?msclkid=1ee9e23bb42d11ec8ec54444d15d7c64)

6. ##Useful Links
	* [C# Coding best practices](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions?msclkid=72b98579b43311ecb0ee2b34c0bd76c2)
	* [Object Orientated Programming](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/object-oriented/)
	* [Selenium WebDriver](https://www.selenium.dev/documentation/webdriver/?msclkid=8e59ff9fb43311ec8897464babe0fbb5)
	* [SpecFlow](https://docs.specflow.org/projects/getting-started/en/latest/index.html)


