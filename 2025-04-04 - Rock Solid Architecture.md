Let's assume you have a User : 

**User**

Many services must access this user : 

* Website Frontend / Backend
* Game Client / Server
* Discord Bot


And perform operations on this user : 

| Operation        | Name                 | Permissions |
| ---------------- | -------------------- | ----------- |
| Get User by Name | UserGetByNameRequest | Low         |
| Get User by Id   | UserGetByIdRequest   | Low         |
| Delete User      | UserDeleteRequest    | High        |
| Create new User  | UserCreateRequest    | High        |
| Ban User         | UserBanRequest       | High        |
| Give a Gift      | UserGiftGiveRequest  | High        |


.NET Standard 2.1 Library



ADG.Contracts
* Users
	* User
				* Get
					* ByName
						* GetUserByNameRequest
						* GetUserByNameRequestValidator
					* ById
						* GetUserByIdRequest
				* Create
					* UserCreateClient
					* UserCreateRequest
					* UserCreateRequestValidator
* Notifications
	* Models
		* Notification
		* NotificationsErrors
	* Operations
		* Commands
			* Create
				* NotificationsCreateRequest
				* NotificationsCreateRequestValidator
				* NotificationsCreateEvent
				* NotificationsCreateResponse
			* Dismiss
				* NotificationsDismissRequest
				* NotificationsDismissRequestValidator
				* NotificationsDismissEvent
		* Queries
			* Search
				* NotificationsSearchRequest
				* NotificationsSearchRequestValidator
			* List
				* NotificationsListRequest
				* NotificationsListRequestValidator
			* Get
				* NotificationsGetRequest


ADG.Api
* Notifications
	* Controllers
		* NotificationsCreateController
		* NotificationsDismissController
		* NotificationsSearchController
		* NotificationsListController
		* NotificationsGetController
	* Repository
		* INotificationsRepository
		* NotificationsRepository


User
* Models
	* User
	* Queries
		* GetUserByNameRequest
		* GetUserByIdRequest
	* Commands
* Notifications
	* Models
		* Notification
	* Controllers
		* NotificationsController
	* Repositories
		
	* Operations



