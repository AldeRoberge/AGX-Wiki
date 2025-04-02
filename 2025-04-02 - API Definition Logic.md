
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

This architecture provides a well defined contract, with clear logic that is explicit.


| Path                                              | Type           |     |
| ------------------------------------------------- | -------------- | --- |
| Entities/Account                                  | **Entity**     |     |
| Components/Name/NameComponent                     | **Component**  |     |
| Components/Name/Update/NameUpdateRequest          | **Request**    |     |
| Components/Name/Update/NameUpdateRequestValidator | **Validator**  |     |
| Components/Name/Update/NameUpdateRequestHandler   | **Handler**    |     |
| Components/Name/Update/NameUpdateEvent            | **Event**      |     |
| Components/Name/Update/NameUpdatePermission       | **Permission** |     |
| Components/Name/Update/NameUpdateErrors           | **Error List** |     |


**Validation rules for names**

| Validation Error Type                    | Description                          |
| ---------------------------------------- | ------------------------------------ |
| Validation.Errors.Name.Empty             | Must not be empty                    |
| Validation.Errors.Name.TooShort          | Must meet minimum length requirement |
| Validation.Errors.Name.TooLong           | Must not exceed maximum length       |
| Validation.Errors.Name.InvalidCharacters | Must contain only valid characters   |
| Validation.Errors.Name.ContainsProfanity | Must not contain profanity           |
| Validation.Errors.Name.IsNotUnique       | Must be unique                       |



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

