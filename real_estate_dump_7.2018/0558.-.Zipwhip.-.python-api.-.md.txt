
==================
Zipwhip Python API
==================

Thank you for expressing interest in the Zipwhip API for Python.

Zipwhip offers are a range of tools and support to transform your idea or
business into a texting reality.Texting is powerful high-priority medium,
one that offers prime real estate on cell phones all across the globe.

Using the Zipwhip API:
Zipwhip uses Java internally, but we are accessible by all languages.
Recently, we began creating a Python API to access Zipwhip. We use it quite
a bit in our Arduino projects around the office.

To begin we created a wrapper of all of the basic web calls available. Even
with the web calls provided in the Python-Api, you can turn an already powerful
medium into something even more.

The sessionKey provided after a log in is a representation of the logged in
user. sessionKeys do not expire, this means if you are a business with a
number of customers using the Zipwhip text enabled landlines/toll-free numbers
then you only need to track the phone number to sessionKey relationship.

For developers maybe just trying out the service with their text enabled mobile
number; we also encourage you to log in once and then save the sessionKey to a
local database.

Basic Usage
===========
    #!/usr/bin/env python

    from ZipwhipApi.calls.WebCalls import WebCalls

    zipwhipClient = WebCalls()

    jsonResponse = zipwhipClient.log_in(username="8559479447",
                                        password="&qYDgGyT[q[62T>TrG^]")

    {
        "response": "8ef1211f-d9f2-4c81-906f-7d27da5a32f8:309626613",
        "success": "true"
    }

    jsonResponse = zipwhipClient.messsage_send(
                        session_key="8ef1211f-d9f2-4c81-906f-7d27da5a32f8:309626613",
                        recipient="ptn:/8559479447",
                        message_body="Hello World, from Zipwhip's Python Api!")

    {
      "response": {
        "fingerprint": "4236521183", #fingerprint identifies the conversation.
        "root": "327559093363723008", #messageId used for read & delete
        "tokens": [
        {
          "contact": 1989548603,
          "device": 309626613,
          "fingerprint": "42336654183",
          "message": "327545678963723008"
        }
        ]
      },
      "success": "true"
    }