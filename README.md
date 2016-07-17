# Microsoft Graph tips
Feel free to open a pull request to add a tip or trick to this list.


## Query Examples
#### Search for users in multiple properties (name, email, etc.)
https://graph.microsoft.com/beta/me/people?$search=satya


## Authentication
#### V2 auth Postman collection
[![Run in Postman](https://raw.githubusercontent.com/Azure/azure-content/master/articles/active-directory/media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)


## OData
#### Enums can be sent by name or value
For example, the calendar resource has a [color property](https://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/calendar#properties):
> Specifies the color theme to distinguish the calendar from other calendars in a UI. The property values are: LightBlue=0, LightGreen=1, LightOrange=2, LightGray=3, LightYellow=4, LightTeal=5, LightPink=6, LightBrown=7, LightRed=8, MaxColor=9, Auto=-1

If sending the numeric value, be sure to wrap it in quotes as a string.
```javascript
// valid
{
  "color": "LightGreen",
  "name": "My Calendar"
}
// also valid and identical to above
{
  "color": "1",
  "name": "My Calendar"
}

```
