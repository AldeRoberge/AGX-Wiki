### ✅ Why this happens:

- **ASP.NET Core does not bind `[FromBody]` on `GET` methods** by default.
- `GET` requests are meant to be **idempotent and have no body**.
- Even Refit is trying to send a JSON body on a `GET` request, which the server rejects.

