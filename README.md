# Microsoft Graph Tips
Feel free to open a pull request to add a tip or trick to this list.


## Authentication
#### V2 auth Postman collection
[![Run in Postman](https://raw.githubusercontent.com/Azure/azure-content/master/articles/active-directory/media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)

You don't even need a server running for this to work. It will redirect you to a broken URL, but you can still copy the `code` from the URL in your browser.
#### Shorter scope lists
When sending a list of scopes in V2 Auth, you don't need the URL prefix like `https://graph.microsoft.com/`. Instead of sending `https://graph.microsoft.com/mail.read`, just send `mail.read` or `Calendars.ReadWrite`.

#### Decoding access tokens
You can decode JWT access tokens from the graph using tools like https://jwt.io/ .  It will show info like appid, name, onprem_sid, and scopes.

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
## Query Examples
#### Search for users in multiple properties (name, email, etc.)
https://graph.microsoft.com/beta/me/people?$search=satya

#### List users and expand manager object
https://graph.microsoft.com/beta/users?$expand=manager

#### List recent messages and get names of attachments (note that $select can be used in $expand)
https://graph.microsoft.com/v1.0/me/messages?$expand=attachments($select=name)

#### Get names of drive items in root and thier permissions ($expand supports comma separated names)
https://graph.microsoft.com/v1.0/me/drive/root?$expand=children($select=name),permissions

#### Search OneDrive for Word documents
https://graph.microsoft.com/v1.0/me/drive/root/search(q='.docx')


## Graph explorer
The graph explorer is open source and hosted on github at https://github.com/yiil/apiExplorer.
You can locally host this and supply your own clientId to have a postman like experience on the Graph.
Swap the clientId out at https://github.com/yiil/apiExplorer/blob/master/src/api-explorer-init.js#L16

## Todo
- [x] Add more query examples
- [x] Check if $select can be used in $expand to limit response size
- [ ] Add dates section talking about DateTimeTimeZone and DateTimeOffset
