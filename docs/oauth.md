
## OAuth

PeeringDB now offers OAuth2 authentication for third-party applications to allow users to authenticate against PeeringDB.

Implementation details are at <https://github.com/peeringdb/peeringdb/issues/131>.  For an example, see <https://github.com/inex/IXP-Manager/issues/322>.  

### What is OAuth?

There is a good write up at <https://aaronparecki.com/oauth-2-simplified/>.

### Register an application

First you need to register your application at <https://peeringdb.com/oauth2/applications/>.

### URLs

- `ACCESS_TOKEN_URL` = https://auth.peeringdb.com/oauth2/token/
- `AUTHORIZE_URL` = https://auth.peeringdb.com/oauth2/authorize/
- `USER_PROFILE_URL` = https://auth.peeringdb.com/profile/v1


### Fields

The fields are based largely on OpenID Connect.

Scopes currently are defined as 

- `profile` : user profile
- `email` : adds fields `email` and `verified_email`
- `networks` : add field `networks`

The `perms` field is a bitmask for [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) as the 4 least significant bits. See following:

```
0b0000 1 1 1 1
       | | | +-- Delete
       | | +---- Update
       | +------ Read
       + ------- Create
```

Example for my user:

```json
{
  "id": 3,
  "name": "Matt Griswold",
  "given_name": "Matt",
  "family_name": "Griswold",
  "email": "grizz@20c.com",
  "verified_user": true,
  "verified_email": true,
  "networks": [
    {
      "perms": 15,
      "asn": 63311,
      "name": "20C",
      "id": 20
    }, 
    {
      "perms": 15,
      "asn": 33713,
      "name": "United IX",
      "id": 7889
    }
  ]
}
```
