Question 1:

My test plan would be to investigate usability of the site from the perspective of a potential or current customer, in order to ensure a smooth customer experience and to both minimise and highlight potential risks to the user experience. There are a number of testing methodologies that could be used here, however given the lack of prior access to the code, expected behaviour or acceptance criteria, this black box testing is best suited to user stories to drive functional testing. 

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
Step 2 - Register button is clicked - The page continues to the create acccount page
Step 3 - Valid user information is inserted into all fields - The fields all validate and allow entry
Step 4 - Data is submitted via "Register" - The screen confirms submission and an email is received confirming details
Step 5 - Email is received - Details within the email are correct and a confirmation link is provided
Step 6 - Confirmation link is followed - Web page opens confirming registration with correct details and access to the users profile

These can then be used as a basis to expand further and cover negative tests to run alongside the positive tests.

Regards the experience based testing, attacking known areas that can cause user difficulties such as:
- Validation of credentials 
- Retaining details between page and accounts
- Ensuring the page is correctly navigatable
- Checking the subdomains for potential phishing vulnerabilities

Each of these ad hoc exploratory methods generate further test cases beyond following the initial scope of the investigation so it would be harder to outline in detail beforehand beyond listing initial concerns and areas to target.

Question 2:

| Test Number     | Test Name | Outcome     | Evidence |  Further notes/Exploratory findings |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| Test 1     | Creating a profile using the "Register" option to ensure a profile is generated with the correctly submitted information       | Failed (Defect 1)      | [Image 1](https://github.com/TMoore89/ENSEKTest/blob/d4a7bad70524b70ed43b06d25b394efdad454fc7/Images/Test1-1.png) [Image2](https://github.com/TMoore89/ENSEKTest/blob/d4a7bad70524b70ed43b06d25b394efdad454fc7/Images/Test1-2.png) | Email Validation is in place and working for correct name@dom.ain, password validation is also active for both presence and 6 digit length and matching, complexity is also present - more test cases needed for next run. Defect also confirmed from the registration option held on the "Log in" page |
| Test 2      | Signing in using the "Log in" option to ensure the user profile can be accessed and is accurate | Blocked  | Test 1 failing prevents this form proceeding futher |  The ASP.NET login methods linked would need investigating in further test runs |
| Test 3     | Following the "Find out more", "about" and "about us" options to ensure the link reaches the correct location with relevant information | Failed (Defect 2)     | ["About" link](https://github.com/TMoore89/ENSEKTest/blob/803d7b04b4efdadd34f4c82bf668097d4c1fc193/Images/About.png) ["About us" link](https://github.com/TMoore89/ENSEKTest/blob/1996dc4e9b6395895e420e9e1f055b2f5d7be8a6/Images/About%20us.png) ["Find out more" link](https://github.com/TMoore89/ENSEKTest/blob/803d7b04b4efdadd34f4c82bf668097d4c1fc193/Images/Find%20out%20more.png)|  An additional link appears on "About us" and "About". This can be followed and successfully loads this: [Image 1](https://github.com/TMoore89/ENSEKTest/blob/803d7b04b4efdadd34f4c82bf668097d4c1fc193/Images/About-About%20us%20link.png) |
| Test 4     | Test Name | Outcome     | Evidence |  Further notes/Exploratory findings |
| Test 5     | Test Name | Outcome     | Evidence |  Further notes/Exploratory findings |
| Test 6     | Test Name | Outcome     | Evidence |  Further notes/Exploratory findings |
| Test 7     | Test Name | Outcome     | Evidence |  Further notes/Exploratory findings |

- Test 1  - Creating a profile using the "Register" option to ensure a profile is generated with the correctly submitted information - Failed (Defect 1)
- Test 2 - Signing in using the "Log in" option to ensure the user profile can be accessed and is accurate
- Test 3 - Following the "Find out more", "about" and "about us" options to ensure the link reaches the correct location with relevant information
- Test 4 - Following the "Contact" option to ensure the link reaches the correct location and that all appropriate links work as expected
- Test 5 - Following the "home" option to ensure the link reaches the correct location and that all appropriate links work as expected
- Test 6 - Selecting "Buy some energy" and following the process through to completion to ensure I am able to place an order
- Test 7 - Selecting "Sell some energy" and following the process through to completion to ensure I am able to create a sale

Defect 1:
Description:
The register button does not complete the command and fails to communicate to SQL

User Story: As a prospective ENSEK customer I would like to be able to create a new account so that I may proceed to buy and sell energy and review my profile

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
