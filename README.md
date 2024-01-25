# punchout.json
Punchout Implementation in Json

### Login Request (sent by procurement)

POST https://punchout.cloud/json/xxxxxxx

```
{
    "user_id": "user_id", // can also be email
    "email": "example@email.com",
    "buyer_session_id": "buyer_session_id",
    "cart_url": "https://wheretosendcart.com/path"
}
```

### CART Request (sent by instapunchout)

POST https://wheretosendcart.com/path (picked from login request cart_url field)

```
{
    "user_id": "user_id", // can also be email
    "email": "example@email.com",
    "buyer_session_id": "buyer_session_id",
    "currency": "USD",
    "items": [
        {
            "id": "lineid1",
            "line_number": 1,
            "sku": "sku1",
            "name": "Product's name",
            "quantity": 3,
            "price": 120, // all prices are multiplied by 1000 to avoid floating point errors
            "unit": "EA",
            "requested_delivery_date": "2020-12-12",  // can also be null/undefined
            "punchout_id": "xxxxxxxxxx",
            "tax": 0, // can also be null/undefined
            "unspsc": "12345678", // can also be null/undefined
            "comments": "comment", // can also be null/undefined
            "lead_time": 1 // can also be null/undefined
        }
    ],
    "shipping_cost": 0, // can also be null/undefined
    "tax": 0, // can also be null/undefined
}
```

- After we send cart to the cart_url, what to do to signal to the procurement that sessions is over.
An option is that you pull your backend for info, but I can also send a message to parent window maybe? that is probably more efficient.

### Order Request

POST https://punchout.cloud/json/xxxxxxx

```
{
    "user_id": "user_id", // can also be email
    "email": "example@email.com",
    "buyer_session_id": "buyer_session_id",
    "currency": "USD",
    "items": [
        {
            "id": "lineid1",
            "line_number": 1,
            "sku": "sku1",
            "name": "Product's name",
            "quantity": 3,
            "price": 120, // all prices are multiplied by 1000 to avoid floating point errors
            "unit": "EA",
            "requested_delivery_date": "2020-12-12",  // can also be null/undefined
            "punchout_id": "xxxxxxxxxx",
            "tax": 0, // can also be null/undefined
            "unspsc": "12345678", // can also be null/undefined
            "comments": "comment", // can also be null/undefined
            "lead_time": 1 // can also be null/undefined
        }
    ],
    "shipping_cost": 0, // can also be null/undefined
    "tax": 0, // can also be null/undefined,
    "billing": {
      "id": "address_id_in_procurement",
      "name": "a label of the address",
      "email": "shippingemail@test.com",
      "deliver_to": [
        "usually company name",
        "or person's name or departement or all"
      ],
      "street": [
        "building, number, street"
      ],
      "city": "city",
      "state": "state", // can be null/undefined // 2/3 letter code if possible
      "postal_code": "99999",
      "country": "US", // 2 letter code if possible
      "phone": "+1 800 5555555",
      "fullname": null, // can be null/undefined , always a person's name if exists
      "company": null // can be null/undefined, always a company name if exists
    },
    "shipping": {
      "id": "address_id_in_procurement",
      "name": "a label of the address",
      "email": "shippingemail@test.com",
      "deliver_to": [
        "usually company name",
        "or person's name or departement or all"
      ],
      "street": [
        "building, number, street"
      ],
      "city": "city",
      "state": "state", // can be null/undefined // 2/3 letter code if possible
      "postal_code": "99999",
      "country": "US", // 2 letter code if possible
      "phone": "+1 800 5555555",
      "fullname": null, // can be null/undefined , always a person's name if exists
      "company": null // can be null/undefined, always a company name if exists
    }
}
```
