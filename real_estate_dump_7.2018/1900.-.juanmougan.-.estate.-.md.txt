# estate
Microservice API to manage real estate. Based on https://thenewstack.io/make-a-restful-json-api-go/  
and also https://www.mongodb.com/blog/post/running-mongodb-queries-concurrently-with-go

Use a valid project structure, check https://golang.org/doc/code.html for details

E. g. `[some folder]/src/github.com/juanmougan/estate` where `estate` is this project's root path

Run the project like this:

    $ go run *.go

Check the API using curl:

    curl 'http://localhost:8080/estates' | jq .

Should get back something like this:

    [
      {
        "name": "Departamento en Palermo",
        "lat": -34.594142,
        "long": -58.422036,
        "created": "0001-01-01T00:00:00Z"
      },
      {
        "name": "Casa en San Isidro",
        "lat": -34.46761,
        "long": -58.510191,
        "created": "0001-01-01T00:00:00Z"
      }
    ]

And if you want to add a new Estate:

    curl -H "Content-Type: application/json" -d '{"name":"Casa de Maria", "Lat": -34.566610, "Long": -58.411191}' http://localhost:8080/estates | jq .

You would get something like this:

    {
      "id": 4,
      "name": "Casa de Maria",
      "lat": -34.56661,
      "long": -58.411191,
      "created": "0001-01-01T00:00:00Z"
    }

Steps missing

1. Add missing endpoint

2. Add MongoDB support

3. Eventually... DB cache?
