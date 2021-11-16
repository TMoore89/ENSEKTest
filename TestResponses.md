# Question 1:

My test plan would be to investigate usability of the site from the perspective of a potential or current customer, in order to ensure a smooth customer experience and to both minimise and highlight potential risks to the user experience. In particular I want to ensure the user is able to create a profile, validate their details, then both purchase and sell some volume of energy. There are a number of testing methodologies that could be used here, however given the lack of prior access to the code, expected behaviour or acceptance criteria, this black box testing is best suited to user stories to drive functional testing. 

Some experienced based testing is also appropriate however, utilising knowledge of areas that can cause vulnerabilities or increase chance of risk to the end product.

With that in mind, I would outline some key user scenarios:

- Creating a profile using the "Register" option to ensure a profile is generated with the correctly submitted information
- Signing in using the "Log in" option to ensure the user profile can be accessed and is accurate
- Following the "Find out more", "about" and "about us" options to ensure the link reaches the correct location with relevant information
- Following the "Contact" option to ensure the link reaches the correct location and that all appropriate links work as expected
- Following the "home" option to ensure the link reaches the correct location and that all appropriate links work as expected
- Selecting "Buy some energy" and following the process through to completion to ensure I am able to place an order
- Selecting "Sell some energy" and following the process through to completion to ensure I am able to create a sale

Given more time these could be expanded out to bespoke test cases each, such as:

Step 1 - Open page - Register button is available
Step 2 - Register button is clicked - The page continues to the create account page
Step 3 - Valid user information is inserted into all fields - The fields all validate and allow entry
Step 4 - Data is submitted via "Register" - The screen confirms submission and an email is received confirming details
Step 5 - Email is received - Details within the email are correct and a confirmation link is provided
Step 6 - Confirmation link is followed - Web page opens confirming registration with correct details and access to the users profile

These can then be used as a basis to expand further and cover negative tests to run alongside the positive tests.

Regards the experience-based testing, attacking known areas that can cause user difficulties such as:
- Validation of credentials 
- Retaining details between page and accounts
- Ensuring the page is correctly navigable
- Checking the subdomains for potential phishing vulnerabilities

Each of these ad hoc exploratory methods generate further test cases beyond following the initial scope of the investigation so it would be harder to outline in detail beforehand beyond listing initial concerns and areas to target.

# Question 2:
## Test execution:

| Test Number     | Test Name | Outcome     | Evidence |  Further notes/Exploratory findings |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| Test 1     | Creating a profile using the "Register" option to ensure a profile is generated with the correctly submitted information       | Failed (Defect 1)      | [Image 1](https://github.com/TMoore89/ENSEKTest/blob/d4a7bad70524b70ed43b06d25b394efdad454fc7/Images/Test1-1.png), [Image 2](https://github.com/TMoore89/ENSEKTest/blob/d4a7bad70524b70ed43b06d25b394efdad454fc7/Images/Test1-2.png) | Email Validation is in place and working for correct name@dom.ain, password validation is also active for both presence and 6 digit length and matching, complexity is also present - more test cases needed for next run. Defect also confirmed from the registration option held on the "Log in" page |
| Test 2      | Signing in using the "Log in" option to ensure the user profile can be accessed and is accurate | Blocked  | Test 1 failing prevents this from proceeding further |  The ASP.NET login methods linked would need investigating in further test runs |
| Test 3     | Following the "Find out more", "about" and "about us" options to ensure the link reaches the correct location with relevant information | Failed (Defect 2)     | ["About" link](https://github.com/TMoore89/ENSEKTest/blob/803d7b04b4efdadd34f4c82bf668097d4c1fc193/Images/About.png) ["About us" link](https://github.com/TMoore89/ENSEKTest/blob/1996dc4e9b6395895e420e9e1f055b2f5d7be8a6/Images/About%20us.png) ["Find out more" link](https://github.com/TMoore89/ENSEKTest/blob/803d7b04b4efdadd34f4c82bf668097d4c1fc193/Images/Find%20out%20more.png)|  An additional link appears on "About us" and "About". This can be followed and successfully loads this: [Image 3](https://github.com/TMoore89/ENSEKTest/blob/803d7b04b4efdadd34f4c82bf668097d4c1fc193/Images/About-About%20us%20link.png) |
| Test 4     | Following the "Contact" option to ensure the link reaches the correct location and that all appropriate links work as expected | Failed - (Defect 3 & Defect 4)   | [Image 4](https://github.com/TMoore89/ENSEKTest/blob/79a10c77cc4e479afcfb62834f624c33ab2a3318/Images/Contact.png) |  No further notes beyond the defect |
| Test 5     | Following the "home" option to ensure the link reaches the correct location and that all appropriate links work as expected | Pass   | [Gif 1](https://github.com/TMoore89/ENSEKTest/blob/aaba7e28f8e71a742906de33e28efecc4294ca9c/Images/Home_button.gif) |  Confirmed to work from all pages with a home option available |
| Test 6     | Selecting "Buy some energy" and following the process through to completion to ensure I am able to place an order | Failed (Defect 5, Defect 6, Defect 7, Defect 8, Defect 9 & Defect 10)    | [Image 5](https://github.com/TMoore89/ENSEKTest/blob/9371d08b4c92e33ad3434a096865e90a025009d0/Images/Purchases.png), [Image 6](https://github.com/TMoore89/ENSEKTest/blob/9371d08b4c92e33ad3434a096865e90a025009d0/Images/Order%20Submitted.png), [Image7](https://github.com/TMoore89/ENSEKTest/blob/9371d08b4c92e33ad3434a096865e90a025009d0/Images/After%20Order%20Submitted.png) |  Many further tests required, each energy type needs a positive and negative test adding alongside some tests to ensure the values update correctly post-sale, the confirmation page needs a suite of tests adding, the discounts, market status and times all need a test to validate them |
| Test 7     | Selecting "Sell some energy" and following the process through to completion to ensure I am able to create a sale | Failed (Defect 11)     | [Image 8](https://github.com/TMoore89/ENSEKTest/blob/4ade5581ae009169f3c226bb809acc133d533917/Images/Sales.png) |  No further notes beyond the defect |

## Defects

### Defect 1:
<details>
  <summary>The register button does not complete</summary>
Description:
The register button does not complete the command and fails to communicate to SQL, presenting the user with an error dump

User Story: As a prospective customer I would like to be able to create a new account so that I may proceed to buy and sell energy and review my profile

Reproduction Steps:
- Open the homepage
- Select Register from the access bar at the top of the page
- Enter a valid username and password on the registration page
- Submit the details for registration

Expected Behaviour:
- The details are submitted and saved back to SQL
- The user receives a confirmation email

Actual Behaviour:
- The request times out
- No email is sent
- The user is given an error dump

Acceptance Criteria:
Given I have completed a registration form
When I click submit
Then the details are saved back into the SQL database
And A confirmation email is sent

Note: 
- Verified against the registration link inside the "Log in" page
- Please see the error entry below:
<details>
  <summary>Error text</summary>
  
  ```Error
An error occurred while processing your request
A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)
at System.Data.ProviderBase.DbConnectionPool.TryGetConnection(DbConnection owningObject, UInt32 waitForMultipleObjectsTimeout, Boolean allowCreate, Boolean onlyOneCheckConnection, DbConnectionOptions userOptions, DbConnectionInternal& connection) at System.Data.ProviderBase.DbConnectionPool.TryGetConnection(DbConnection owningObject, TaskCompletionSource`1 retry, DbConnectionOptions userOptions, DbConnectionInternal& connection) at System.Data.ProviderBase.DbConnectionFactory.TryGetConnection(DbConnection owningConnection, TaskCompletionSource`1 retry, DbConnectionOptions userOptions, DbConnectionInternal oldConnection, DbConnectionInternal& connection) at System.Data.ProviderBase.DbConnectionInternal.TryOpenConnectionInternal(DbConnection outerConnection, DbConnectionFactory connectionFactory, TaskCompletionSource`1 retry, DbConnectionOptions userOptions) at System.Data.ProviderBase.DbConnectionClosed.TryOpenConnection(DbConnection outerConnection, DbConnectionFactory connectionFactory, TaskCompletionSource`1 retry, DbConnectionOptions userOptions) at System.Data.SqlClient.SqlConnection.TryOpenInner(TaskCompletionSource`1 retry) at System.Data.SqlClient.SqlConnection.TryOpen(TaskCompletionSource`1 retry) at System.Data.SqlClient.SqlConnection.Open() at System.Data.Entity.Infrastructure.Interception.DbConnectionDispatcher.<Open>b__36(DbConnection t, DbConnectionInterceptionContext c) at System.Data.Entity.Infrastructure.Interception.InternalDispatcher`1.Dispatch[TTarget,TInterceptionContext](TTarget target, Action`2 operation, TInterceptionContext interceptionContext, Action`3 executing, Action`3 executed) at System.Data.Entity.Infrastructure.Interception.DbConnectionDispatcher.Open(DbConnection connection, DbInterceptionContext interceptionContext) at System.Data.Entity.SqlServer.SqlProviderServices.<>c__DisplayClass33.<UsingConnection>b__32() at System.Data.Entity.SqlServer.DefaultSqlExecutionStrategy.<>c__DisplayClass1.<Execute>b__0() at System.Data.Entity.SqlServer.DefaultSqlExecutionStrategy.Execute[TResult](Func`1 operation) at System.Data.Entity.SqlServer.DefaultSqlExecutionStrategy.Execute(Action operation) at System.Data.Entity.SqlServer.SqlProviderServices.UsingConnection(DbConnection sqlConnection, Action`1 act) at System.Data.Entity.SqlServer.SqlProviderServices.UsingMasterConnection(DbConnection sqlConnection, Action`1 act) at System.Data.Entity.SqlServer.SqlProviderServices.CreateDatabaseFromScript(Nullable`1 commandTimeout, DbConnection sqlConnection, String createDatabaseScript) at System.Data.Entity.SqlServer.SqlProviderServices.DbCreateDatabase(DbConnection connection, Nullable`1 commandTimeout, StoreItemCollection storeItemCollection) at System.Data.Entity.Core.Common.DbProviderServices.CreateDatabase(DbConnection connection, Nullable`1 commandTimeout, StoreItemCollection storeItemCollection) at System.Data.Entity.Core.Objects.ObjectContext.CreateDatabase() at System.Data.Entity.Migrations.Utilities.DatabaseCreator.Create(DbConnection connection) at System.Data.Entity.Migrations.DbMigrator.EnsureDatabaseExists(Action mustSucceedToKeepDatabase) at System.Data.Entity.Migrations.DbMigrator.Update(String targetMigration) at System.Data.Entity.Internal.DatabaseCreator.CreateDatabase(InternalContext internalContext, Func`3 createMigrator, ObjectContext objectContext) at System.Data.Entity.Internal.InternalContext.CreateDatabase(ObjectContext objectContext, DatabaseExistenceState existenceState) at System.Data.Entity.Database.Create(DatabaseExistenceState existenceState) at System.Data.Entity.CreateDatabaseIfNotExists`1.InitializeDatabase(TContext context) at System.Data.Entity.Internal.InternalContext.<>c__DisplayClassf`1.<CreateInitializationAction>b__e() at System.Data.Entity.Internal.InternalContext.PerformInitializationAction(Action action) at System.Data.Entity.Internal.InternalContext.PerformDatabaseInitialization() at System.Data.Entity.Internal.LazyInternalContext.<InitializeDatabase>b__4(InternalContext c) at System.Data.Entity.Internal.RetryAction`1.PerformAction(TInput input) at System.Data.Entity.Internal.LazyInternalContext.InitializeDatabaseAction(Action`1 action) at System.Data.Entity.Internal.LazyInternalContext.InitializeDatabase() at System.Data.Entity.Internal.InternalContext.Initialize() at System.Data.Entity.Internal.InternalContext.GetEntitySetAndBaseTypeForType(Type entityType) at System.Data.Entity.Internal.Linq.InternalSet`1.Initialize() at System.Data.Entity.Internal.Linq.InternalSet`1.get_InternalContext() at System.Data.Entity.Infrastructure.DbQuery`1.System.Linq.IQueryable.get_Provider() at System.Data.Entity.QueryableExtensions.FirstOrDefaultAsync[TSource](IQueryable`1 source, Expression`1 predicate, CancellationToken cancellationToken) at System.Data.Entity.QueryableExtensions.FirstOrDefaultAsync[TSource](IQueryable`1 source, Expression`1 predicate) at Microsoft.AspNet.Identity.EntityFramework.UserStore`6.<GetUserAggregateAsync>d__67.MoveNext() --- End of stack trace from previous location where exception was thrown --- at System.Runtime.CompilerServices.TaskAwaiter.ThrowForNonSuccess(Task task) at System.Runtime.CompilerServices.TaskAwaiter.HandleNonSuccessAndDebuggerNotification(Task task) at Microsoft.AspNet.Identity.TaskExtensions.CultureAwaiter`1.GetResult() at Microsoft.AspNet.Identity.UserValidator`2.<ValidateUserName>d__14.MoveNext() --- End of stack trace from previous location where exception was thrown --- at System.Runtime.CompilerServices.TaskAwaiter.ThrowForNonSuccess(Task task) at System.Runtime.CompilerServices.TaskAwaiter.HandleNonSuccessAndDebuggerNotification(Task task) at Microsoft.AspNet.Identity.UserValidator`2.<ValidateAsync>d__13.MoveNext() --- End of stack trace from previous location where exception was thrown --- at System.Runtime.CompilerServices.TaskAwaiter.ThrowForNonSuccess(Task task) at System.Runtime.CompilerServices.TaskAwaiter.HandleNonSuccessAndDebuggerNotification(Task task) at Microsoft.AspNet.Identity.UserManager`2.<CreateAsync>d__73.MoveNext() --- End of stack trace from previous location where exception was thrown --- at System.Runtime.CompilerServices.TaskAwaiter.ThrowForNonSuccess(Task task) at System.Runtime.CompilerServices.TaskAwaiter.HandleNonSuccessAndDebuggerNotification(Task task) at Microsoft.AspNet.Identity.UserManager`2.<CreateAsync>d__79.MoveNext() --- End of stack trace from previous location where exception was thrown --- at System.Runtime.CompilerServices.TaskAwaiter.ThrowForNonSuccess(Task task) at System.Runtime.CompilerServices.TaskAwaiter.HandleNonSuccessAndDebuggerNotification(Task task) at EnsekAutomationTest.UI.MVC.Controllers.AccountController.<Register>d__15.MoveNext() in C:\GIT\configurationTest\Test Application\EnsekAutomationTest.UI.MVC\Controllers\AccountController.cs:line 155 --- End of stack trace from previous location where exception was thrown --- at System.Runtime.CompilerServices.TaskAwaiter.ThrowForNonSuccess(Task task) at System.Runtime.CompilerServices.TaskAwaiter.HandleNonSuccessAndDebuggerNotification(Task task) at System.Web.Mvc.Async.TaskAsyncActionDescriptor.EndExecute(IAsyncResult asyncResult) at System.Web.Mvc.Async.AsyncControllerActionInvoker.<>c__DisplayClass8_0.<BeginInvokeAsynchronousActionMethod>b__1(IAsyncResult asyncResult) at System.Web.Mvc.Async.AsyncResultWrapper.WrappedAsyncResult`1.CallEndDelegate(IAsyncResult asyncResult) at System.Web.Mvc.Async.AsyncResultWrapper.WrappedAsyncResultBase`1.End() at System.Web.Mvc.Async.AsyncControllerActionInvoker.EndInvokeActionMethod(IAsyncResult asyncResult) at System.Web.Mvc.Async.AsyncControllerActionInvoker.AsyncInvocationWithFilters.<>c__DisplayClass11_0.<InvokeActionMethodFilterAsynchronouslyRecursive>b__0() at System.Web.Mvc.Async.AsyncControllerActionInvoker.AsyncInvocationWithFilters.<>c__DisplayClass11_2.<InvokeActionMethodFilterAsynchronouslyRecursive>b__2() at System.Web.Mvc.Async.AsyncControllerActionInvoker.<>c__DisplayClass7_0.<BeginInvokeActionMethodWithFilters>b__1(IAsyncResult asyncResult) at System.Web.Mvc.Async.AsyncResultWrapper.WrappedAsyncResult`1.CallEndDelegate(IAsyncResult asyncResult) at System.Web.Mvc.Async.AsyncResultWrapper.WrappedAsyncResultBase`1.End() at System.Web.Mvc.Async.AsyncControllerActionInvoker.EndInvokeActionMethodWithFilters(IAsyncResult asyncResult) at System.Web.Mvc.Async.AsyncControllerActionInvoker.<>c__DisplayClass3_6.<BeginInvokeAction>b__4() at System.Web.Mvc.Async.AsyncControllerActionInvoker.<>c__DisplayClass3_1.<BeginInvokeAction>b__1(IAsyncResult asyncResult)
  ```
 
</details>
  </details>

### Defect 2:
  <details>
  <summary>Information links do not route correctly</summary>
Description:
The various links to read more information about the company do not all direct to the same location

User Story: As a prospective customer I would like to be able to research and find out consistent information about the company from any applicable link so that I may find out more about ENSEK and make an educated decision on my involvement with them

Reproduction Steps:
- Open the homepage
- Right click on the following links and open a new tab:
    - About
    - About us
    - Find out more
- Peruse the opened page

Expected Behaviour:
- All 3 pages have directed to the same information page

Actual Behaviour:
- About & About us direct to one page
- Find out more directs to a different location

Acceptance Criteria:
Given I have followed any of the information links ("About", "About us" and "Find out more")
When I peruse the information presented
Then the same information is presented for all 3 pages

Note: 
- If there are further leaps to the information page as there are currently for About and About us, then this should also function and be identical
    </details>
  
### Defect 3:
  <details>
  <summary>The contact screen loads an image with incorrect spelling</summary>
Description:
Opening the contact screen presents a misspelt "Erorr" image

User Story: As a prospective or existing customer I would like to be able to contact the company from the contacts page so that I may raise any relevant queries

Reproduction Steps:
- Open the homepage
- Click on the contacts page
- Peruse the opened page

Expected Behaviour:
- Various contact methods are presented and accessible

Actual Behaviour:
- An image saying "Erorr" is presented

Acceptance Criteria:
Given I have navigated to the contact page
When I peruse the screen presented
Then a selection of communication methods are available
  </details>
    
### Defect 4:
  <details>
  <summary>Incorrect contact page header</summary>
Description:
The header for the "Contact us" page simply reads "Contact."

User Story: As a prospective or existing customer I would like to be able to correctly identify the page I was browsing from the header so that I may easily navigate the site and not be presented with the wrong information

Reproduction Steps:
- Open the homepage
- Click on the contacts page
- Peruse the opened page

Expected Behaviour:
- The header for the page correctly displays "Contact us"

Actual Behaviour:
- The header for the page incorrectly displays "Contact."

Acceptance Criteria:
Given I have navigated to the contact page
When I peruse the screen presented
Then the header reads "Contact us"
  </details>

### Defect 5:
  <details>
  <summary>Oil unit measurement is incorrect</summary>
Description:
The unit of measurement is incorrect for oil

User Story: As a customer purchasing energy I would like to see the measurements in the correct units so that I may make my purchases with no ambiguity on the volumes

Reproduction Steps:
- Open the homepage
- Click on the buy energy page
- Peruse the oil purchase line

Expected Behaviour:
- The measurement is "Per litre"

Actual Behaviour:
- The measurement is "per Litres"

Acceptance Criteria:
Given I have navigated to the buy energy page
When I check the prices/volume for oil
Then the measurement is in cost per litre
  </details>

### Defect 6:
  <details>
  <summary>Offers display contradictory figures</summary>
Description:
The current offer has a different amount of discount between the image and text

User Story: As a customer purchasing energy I would like to be able to have the correct percentage discount in both image and text so that I know what I will be spending and can plan accordingly
  
Reproduction Steps:
- Open the homepage
- Click on the buy energy page
- Peruse the available discount

Expected Behaviour:
- The text and image display the same discount or reduction

Actual Behaviour:
- The text and image display different values for the discount

Acceptance Criteria:
Given I have navigated to the buy energy page
When I peruse the screen presented
Then the discount panel correctly displays a matching amount in both text and on the image
  </details>
    
### Defect 7:
  <details>
  <summary>There is no validation the quantity on energy sold</summary>
Description:
There is no validation on the quantity of energy sold allowing figures too large to be submitted

User Story: As a customer purchasing energy I would like to be able to make sure there is validation in place so I cannot purchase more energy than is available

Reproduction Steps:
- Open the homepage
- Click on the buy energy page
- Attempt to purchase an amount of energy greater than is available for each energy type

Expected Behaviour:
- There is a warning noting that the number exceeds available volume and the purchase is prevented

Actual Behaviour:
- The purchase continues and sets the available amount into a negative figure
- The negative figure is then represented on the buy energy page once confirmed

Acceptance Criteria:
Given I have navigated to the buy energy page
When I purchase a volume of an energy that exceeds the available amount
Then the submission fails
And the available amount is not altered
And I am presented with a warning/message explaining this
  </details>
  
### Defect 8:
  <details>
  <summary>There is no subtotal and confirmation screen</summary>
Description:
There is no subtotal and confirmation before the order is completed to check the values

User Story: As a customer purchasing energy I would like to be presented with a subtotal and order confirmation so that I may confirm the amount and cost of the energy I'm purchasing and so I can ensure the discounts are applied
  
Reproduction Steps:
- Open the homepage
- Sign in as a valid user
- Return to the homepage
- Click on the buy energy page
- Enter a valid amount of energy to purchase
- Select purchase

Expected Behaviour:
- A subtotal with breakdown is provided with an order confirmation

Actual Behaviour:
- The order is placed and immediately processed

Acceptance Criteria:
Given I have entered an amount of energy to purchase
And I am signed in as a valid user
When I submit my purchase request
Then I am presented with a subtotal screen with breakdown
And the values are correct
And there is a button to confirm
  
Given I have submitted a purchase
And I am signed in as a valid user
And I have checked the subtotal
When I click on confirm
Then the order is completed
And an email is generated confirming the order
  </details>
    
### Defect 9:
  <details>
  <summary>Purchases can be made without being signed in</summary>
Description:
There is no requirement for an account holder to be signed in to make a purchase which in turn affects the amount to supply

User Story: As an energy supplier I would like to ensure that all potential purchases are by a user with a valid account so that I can ensure the delivery and billing is correct

Reproduction Steps:
- Open the homepage
- Click on the buy energy page
- Enter a valid amount of energy to purchase
- Select purchase

Expected Behaviour:
- The submission is failed and the user is presented with a log in screen

Actual Behaviour:
- The submission continues 

Acceptance Criteria:
Given I have entered an amount of energy to purchase
And I am not signed in as a valid user
When I submit my purchase request
Then I am presented with a sign in request
  </details>
    
### Defect 10:
  <details>
  <summary>Dev tools left visible to the public</summary>
Description:
The reset button and message regards using it for testing are not to be included in a customer facing site

User Story: As a potential or current customer I would like to ensure I don't encounter any developer tools and debugging artifacts that I can be sure that I am entering a valid order that will not be used as test data or fail to complete

Reproduction Steps:
- Open the homepage
- Click on the buy energy page
- Peruse the page

Expected Behaviour:
- There are no development tools or debug artifacts

Actual Behaviour:
- There is a reset button with a caption that it is intended for test purposes

Acceptance Criteria:
Given I have navigated to the buy energy page
When I peruse the screen presented
There are no references to using the on-screen tools for test purposes
And the reset button is labelled "reset amounts"
  </details>
    
### Defect 11:
  <details>
  <summary>The sell page does not load</summary>
Description:
When opening up the "Sell energy" page it produces an image stating the page is under maintenance

User Story: As a prospective or existing customer I would like to be able to load the "Sell energy" page so that I may both check the current rates and also to place sales if appropriate

Reproduction Steps:
- Open the homepage
- Click on the "Sell energy" page
- Peruse the opened page

Expected Behaviour:
- Various energy types are available to sell with given rates

Actual Behaviour:
- An image saying "Maintenance" is presented

Acceptance Criteria:
Given I have navigated to the "sell energy" page
When I peruse the screen presented
Then a selection of energy types and their current rates are presented
  </details>

# Question 3:
## Identifying tests for automation:
Whilst this is not a comprehensive list, some reasonable candidates for automation and why include:
- Register new profile
    - This is a screen where the elements will rarely change thus reducing the amount of maintenance and there are clearly defined rules for each field. As such it is easy to have variables with a large volume of generated values. This will remove a lot of overhead from a manual tester as it can be ensured that the rules for the fields can be complied with and the obvious points of failures checked with ease. It also enables some stress testing of the fields by continually generating longer email addresses/passwords until such point as the field rejects the value (if at all).
- Log in
    - Much as with the new profile generation, these are elements that rarely change and as such it would be easy to ensure there pre-defined values that can be quickly and efficiently checked against the database for existing users. It can also be used to confirm negative test behaviour and also could be adapted for some load testing to simulate a large volume of users signing in simultaneously.
- Placing an order
    - There are a large range of strings that can be used here to test various combinations of entries into the various energy values both simultaneously or independently, both for positive outcomes but also to ensure that the validation on the fields is acting as expected. This is a process that may take a manual tester a long time to check all the combinations of boundaries for validation against the various combinations of populated fields, so there is a lot of scope for increased efficiency.
- Ensuring the links on the pages navigate to the intended place
    - Inevitably there are a lot of links on each page, ensuring that every link works is a basic task that can be time consuming to keep travelling to/from pages and check the address. This task is well suited to automation as it would remove the bulk of the strain and effort from the manual testers in a regression situation, allowing them to focus on the more complex or exploratory aspects.
  
## Elements, locators and tools
  
To identify the elements on screen I utilised the Selenium IDE Chrome plugin, I was also able to find the details via the chrome developer console and also some of the values via Accessibility Insights for Windows. The below again is an example but not a comprehensive list utilising the most appropriate target type, although I am aware others are available:
  
  | On screen element     | Locator |
  | ----------- | ----------- | 
  | Number of units required - Gas     | id=energyType_AmountPurchased      |
  | Number of units required - Nuclear     | css=tr:nth-child(2)#energyType_AmountPurchased      |
  | Number of units required - Electricity   | css=tr:nth-child(3)#energyType_AmountPurchased      |
  | Number of units required - Oil     | css=tr:nth-child(4)#energyType_AmountPurchased      |
  | Buy (any)     | name=Buy      |
  | Reset    | name=Reset      |
  | Remaining volumes - Gas     | css=tr:nth-child(1) > td:nth-child(5)     |
  | Remaining volumes - Nuclear     | css=tr:nth-child(2) > td:nth-child(5)      |
  | Remaining volumes - electricity    | css=tr:nth-child(3) > td:nth-child(5)      |
  | Remaining volumes - Oil     | css=tr:nth-child(4) > td:nth-child(5)      |
  | Discount text    | css=h3      |
  | Discount image    | css=.well > img      |
  | Back to homepage    | linkText=Back to Homepage      |
  | Home    | linktext=Home      |
  | About    | linktext=About      |
  | Contact    | linktext=Contact      |
  | Register    | id=registerlink      |
  | Log in    | id=loginlink      |
  
Note: The rest of the tables locations follow the same pattern, with the relevant row and column numbers replacing the child values.
  
 # Question 4:
## Unable to complete:
At the time of writing it is impossible to engage with question 4 due to a bug:

### Defect 1:
  <details>
  <summary>Unable to open the test application or swagger document</summary>
Description:
When following the link for the 4th test activity, the link leads to an unavailalbe service
    
User Story: As a prospective QA employee I would like to be able to open the required activity resources so I am to complete the tasks to a satisfactory or greater standard

Reproduction Steps:
- Open the test invitation email
- Open the ENSEK remote tester software exercise brief
- Attempt to follow the link for activity 4

Expected Behaviour:
- Access is granted to an API with a Swagger document

Actual Behaviour:
- A message is displayed stating the service is unavailable

Acceptance Criteria:
Given I have opened the ENSEK remote tester software exercise brief
When I follow the link for exercise 4
Then I am presented with a Swagger document
And I am presented with an API to test
  </details>
  
  
[Error image](https://github.com/TMoore89/ENSEKTest/blob/9603127899e766e7361905b951a10ceb70a260e7/Images/Question4.png)
