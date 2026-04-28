API
===

.. autosummary::
   :toctree: generated

API Routes for different parts of the app.

Responses are in JSON format but are portrayed in this documentation as the Python dictionaries used to generate the JSON contained within the source code.

Authentication
--------------

Authentication encompasses logging in and signing up.

Logging in
^^^^^^^^^^

Route: ``/login``
Request type: POST and DELETE.

Sending a DELETE request will delete the user.

POST
""""

Parameters:
- ``email``, string, required
- ``password``, string, required

Response: ::
   
   {
      "process": "Sign In",
      "result": True,
      "user_id": user.get("user_id"),
      "email": user.get("email"),
      "first_name": user.get("first_name") or user.get("name"),
      "last_name": user.get("last_name") or user.get("lastname"),
      "name": user.get("first_name") or user.get("name"),
      "lastname": user.get("last_name") or user.get("lastname"),
      "access_token": token,
      "token_type": "Bearer",
      "expires_in": JWT_EXPIRES_MINUTES * 60,
   }, 200


DELETE
""""""

Parameters: Same as POST.

Response (on success): ::
   
   {
      "process": "Delete User",
      "name": user["name"],
      "result": True
   }, 200

Response (on failure): ::
   
   {"process": "Delete User", "error": "An error occurred while deleting the user"}, 500

Signing up
^^^^^^^^^^

Creates a new user

POST
""""

Route: ``/signup``

Parameters:
- ``name``, string, required
- ``lastname``, string, required
- ``email``, string, required
- ``password``, string, required


Response (on success): ::
   
   {
      "process": "Sign Up",
      "result": True,
      "user_id": created_user.get("user_id"),
      "first_name": name,
      "last_name": lastname,
      "name": name,
      "lastname": lastname,
      "email": email,
   }, 201


Response (on failure): ::
   
   {
      "process": "Sign Up",
      "result": False,
      "error": "An error occurred during sign up",
   }, 500

Car parks (listing and creating)
--------------------------------

Methods for listing and creating new car parks.

Route: `/car-park`

GET
^^^

Returns a list of all car parks.

Parameters: None.

Response: ::
   
   {
      "data": CarParkSchema().dump(car_park_data)
   }, 200

POST
^^^^

Parameters:
- ``name``, string, required
- ``spaces``, int, required
- ``location``, float, required

Response: ::
   
   {
      "data": CarParkSchema().dump(response.data[0])
   }, 201
