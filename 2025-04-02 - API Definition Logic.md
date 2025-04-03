
| Path                                                                 | Type           |
| -------------------------------------------------------------------- | -------------- |
| Application/Accounts/Account<br>                                     | **Entity**     |
| Application/Accounts/AccountErrors<br>                               | **Error List** |
| Application/Accounts/Get/ByName/AccountGetByNameRequest<br>          | **Request**    |
| Application/Accounts/Get/ByName/AccountGetByNameRequestClient        | **Client**     |
| Application/Accounts/Get/ByName/AccountGetByNameRequestValidator<br> | **Validator**  |
| Application/Accounts/Get/ByName/AccountGetByNameRequestHandler<br>   | **Handler**    |
| Application/Accounts/Get/ByName/AccountGetByNameResponse<br>         | **Response**   |
| Application/Accounts/Get/ByName/AccountGetByNameErrors               | **Error List** |

**This architecture provides a well defined contract, with clear logic that is explicit.**

| Path                                              | Type          |                        |
| ------------------------------------------------- | ------------- | ---------------------- |
| Entities/Account                                  | **Entity**    |                        |
| Components/Name/NameComponent                     | **Component** |                        |
| Components/Name/Update/NameUpdateRequest          | **Request**   |                        |
| Components/Name/Update/NameUpdateRequestClient    | **Client**    |                        |
| Components/Name/Update/NameUpdateRequestValidator | **Validator** |                        |
| Components/Name/Update/NameUpdateRequestHandler   | **Handler**   | Validation, rate limit |
| Components/Name/Update/NameUpdateSuccess          | **Response**  |                        |
| Components/Name/Update/NameUpdateError            | **Response**  |                        |

### How would you represent a complex transaction, like an item trade, in these terms?

Components/Inventory/Trade/

**InventoryTradeComponent**


Are written from the perspective of the client.

| Topology         | Component | Feature    | Verb        | Description                            |
| ---------------- | --------- | ---------- | ----------- | -------------------------------------- |
| Client -> Server | Trade     | Invitation | **Send**    | Sends an invitation to another player. |
| Server -> Client | Trade     | Invitation | *Received*  | Received an invitation to trade.       |
| Client -> Server | Trade     | Invitation | **Cancel**  | Cancel a sent invitation.              |
| Server -> Client | Trade     | Invitation | *Cancelled* |                                        |
| Client -> Server | Trade     | Invitation | **Accept**  | Accepts a trade invitation.            |
| Server -> Client | Trade     | Items      | *Started*   | Trade started                          |
| Client -> Server | Trade     | Invitation | **Reject**  | Reject a trade invitation.             |
| Client -> Server | Trade     | Items      | **Update**  | Select or deselect items.              |
| Client -> Server | Trade     | Items      | **Accept**  | Accepts the ongoing trade.             |
| Client -> Server | Trade     | Items      | **Cancel**  | Cancels the ongoing trade.             |



* InventoryTradeStartRequest
* InventoryTradeStartSuccess
* InventoryTradeStartError

* InventoryTradeCancelRequest
* InventoryTradeCancelSuccess
* InventoryTradeCancelError

* InventoryTradeAcceptRequest
* InventoryTradeAcceptSuccess
* InventoryTradeAcceptError

* InventoryTradeRejectRequest
* InventoryTradeRejectSuccess
* InventoryTradeRejectError

* InventoryTradeUpdateRequest
* InventoryTradeUpdateSuccess
* InventoryTradeUpdateError

* InventoryTradeCompleteRequest
* InventoryTradeCompleteSuccess
* InventoryTradeCompleteError



Example implementation of entity component Name :


```csharp
public sealed class NameComponent : EntityComponent  
{  
     public string Path => "Components/Name";
	 public NameData Name { get; }
	 public NameEvents Events { get; }

	 public void Rename(string newName) {
		 
	 }
}

public sealed class NameEvents 
{
	public Action<NameChangeSuccessEvent> OnNameChanged { get; } = new();
	public Action<NameChangeErrorEvent> OnNameChangeRejected { get; } = new();
}

public sealed record NameChangeSuccessEvent
{
	public NameData NewName;
	public NameData? PreviousName;
	public Entity RequestBy;
	public Entity Target;
}

public sealed class NameData : EntityComponentData
{
	public NameSnapshot Name { get; }
	public List<NameSnapshot> PreviousNames { get; }
}

public sealed class NameDataSnapshot {
	public string Name { get; }
	public DateTime NamedDate { get; }
}
```


**Validation rules for names**

| Validation Error Type                   | Description                          |
| --------------------------------------- | ------------------------------------ |
| ValidationErrors.Name.Empty             | Must not be empty                    |
| ValidationErrors.Name.Length.TooShort   | Must meet minimum length requirement |
| ValidationErrors.Name.Length.TooLong    | Must not exceed maximum length       |
| ValidationErrors.Name.InvalidCharacters | Must contain only valid characters   |
| ValidationErrors.Name.Profanity         | Must not contain profanity           |
| ValidationErrors.Name.Duplicated        | Must be unique                       |



If a player wants to rename himself, the handler must verify that : 
1. The validation passes (see above)
2. Has the rights to rename
	1. The NameComponent is owned by the Sender











```csharp
public sealed record CompleteTodoCommand(Guid TodoItemId) : ICommand;
```


```csharp
return Result.Failure(TodoItemErrors.NotFound(command.TodoItemId));
```

