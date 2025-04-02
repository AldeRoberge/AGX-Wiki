Domain driven design : 

Domain
* Entities
* Business rules

Isolated core from external concerns : controlling coupling. Define an abstraction to represent the external concern. 

The lower level components should not reference components higher.


Application





We use FluentResults for encapsulating :
* Success, which contains the Value
* Error, which contains one or more Errors

We also use FluentValidation for validating our messages.

We emit domain events 


