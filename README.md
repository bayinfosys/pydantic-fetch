# Pydantic-fetch

Extension of `pydantic.BaseModel` which supports sending and parsing from HTTP endpoints.

## Description

`BaseModel` is extended with two class functions:

+ `fetch` to recieve a json payload from an endpoint and validate it as the pydantic model
+ `submit` to send a pydantic model to an endpoint as a json payload.

## Usage

```python3
from pydantic_fetch import BaseModel

class User(BaseModel):
  id: str
  name: str


# this endpoint refers to the User model in POST/GET requests
endpoint = "http://localhost:8000/myapi"


def send_user(endpoint):
  """send a user model to the endpoint"""
  user = User(id="new-id", name="username")
  user.submit(endpoint)


def get_user(endpoint):
  """fetch user data from the endpoint"""
  user = User.fetch(endpoint)


def get_authenticated_response(endpoint):
  """include a jwt token to authenticate the request"""
  token = "my-jwt-token"
  user = User.fetch(
      endpoint,
      headers={"Authorization": f"Bearer {token}"}
  )

def get_with_existing_client(endpoint):
  """create an httpx client to make the request, persist the connection, etc"""
  with httpx.Client() as client:
    user = User.fetch(endpoint, httpx_client=client)
    user.name = "new-username"
    user.submit(endpoint, httpx_client=client)
```
