Requests come in (from a Web API), they go into the Application, which is broken down by feature, use cases. The user is performing an Action, that has associated business logic. This application defines interfaces for it's services (like the database, message bus, notifications)

```csharp
GET users/{userId}/notifications // List notifications
POST users/{userId}/notifications // Create notification
```

INotificationService
* Game
* Push
* Email
* Discord


Presentation Layer : 

* Notifications.Contracts
	* CreateNotificationRequest
	* NotificationResponse
* Notifications.Api
	* Controllers
		* NotificationsController

Application Layer : 
* Notifications
	* Commands
		* Create
		* Dismiss
		* Delete
	* Queries
		* Get *single*
		* List *all*
* Common
	* Interfaces
		* INotificationsRepository
		* IUsersRepository

Domain Layer : 
* Notifications
	* Notification
	* NotificationErrors
* Users
	* User

Infrastructure Layer
* Notifications
	* NotificationsRepository
* Users
	* UsersRepository


---
### Concerns

BookStore
* BookStore.Application
	* Commands
	* Interfaces
	* Validators
* BookStore.Domain
* BookStore.Infrastructure
* BookStore.WebUI

>[!error] Concerns
>This causes features to be spread across the code base. Requires navigating the entire code base to find and modify the pieces of a single feature. High coupling between features. Unnecessary complexity.

### Vertical Slice Architecture

Code is organized by features, high level functionalities.

Yes, there is coupling between the core domain models (entities), but this comes at the benefits of consistency.

From the client's persepctive : 
`Request -> Handler -> Response`

If the request changes somethings, it's called a command (writing). If it only gets data, it's a query (reading).


Architecture : 
`UI -> Application -> Domain -> Infrastructure`


BookStore 
* BookStore.Cart
	* AddItem
	* ComputeTotal
		* ComputeTotalHandler
	* RemoveItem
* BookStore.Catalog
	* AddItem
		* Controller
		* Repository
		* Validator
	* ApplyFilter
	* RemoveItem
* BookStore.Search


>[!info] Benefits
>* Maximizes cohesion within a slice
>* Minimizes coupling between slices
>* Avoids unnecessary abstractions


> A use case is a description of the way that an automated system is used. It specifies the input to be provided by the user, the output to be returned to the user, and the processing steps involved in producing that output.


---



UserGetByNameRequest
UserGetByIdRequest