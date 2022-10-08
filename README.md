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


def send_user(endpoint, id: str, name: str):
  user = User(id=id, name=name)
  user.submit(endpoint)


def get_user(endpoint):
  user = User.fetch(endpoint)
```

