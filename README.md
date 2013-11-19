UltimateDeveloperEvent-Server-Rails
-==================================

Ultimate Developer Event Server for Demo application.

# REST API example application

This is a bare-bones example of a Sinatra application providing a REST
API to a DataMapper-backed model.

The entire application is contained within the `app.rb` file.

## Install

    bundle install

## Run the app

    unicorn -p 7000

# REST API

The REST API to the example app is described below.

## Get list of Devices

### Request

`GET /devices/`

    curl -i -H 'Accept: application/json' http://localhost:7000/devices/

### Response

    HTTP/1.1 200 OK
    Date: Thu, 24 Feb 2011 12:36:30 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 2

    []

## Create a new Device

### Request

`POST /devices/`

    curl -i -H 'Accept: application/json' -d 'name=Foo&status=new' http://localhost:7000/device

## Get a specific Device

### Request

`GET /devices/id`

    curl -i -H 'Accept: application/json' http://localhost:7000/devices/1

## Get a non-existent Device

### Request

`GET /devices/id`

    curl -i -H 'Accept: application/json' http://localhost:7000/devices/9999

### Response

    HTTP/1.1 404 Not Found
    Date: Thu, 24 Feb 2011 12:36:30 GMT
    Status: 404 Not Found
    Connection: close
    Content-Type: application/json
    Content-Length: 35

    {"status":404,"reason":"Not found"}

## Change a Device's state

### Request

`PUT /devices/:id/status/changed`

    curl -i -H 'Accept: application/json' -X PUT http://localhost:7000/devices/1/status/changed

### Response

    HTTP/1.1 200 OK
    Date: Thu, 24 Feb 2011 12:36:31 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 40

    {"id":1,"name":"Foo","status":"changed"}

## Change a Device

### Request

`PUT /devices/:id`

    curl -i -H 'Accept: application/json' -X PUT -d 'name=Foo&status=changed2' http://localhost:7000/devices/1

### Response

    HTTP/1.1 200 OK
    Date: Thu, 24 Feb 2011 12:36:31 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 41

    {"id":1,"name":"Foo","status":"changed2"}


## Change a Device using the _method hack

### Request

`POST /devices/:id?_method=POST`

    curl -i -H 'Accept: application/json' -X POST -d 'name=Baz&_method=PUT' http://localhost:7000/devices/1

### Response

    HTTP/1.1 200 OK
    Date: Thu, 24 Feb 2011 12:36:32 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 41

    {"id":1,"name":"Baz","status":"changed4"}

## Delete a Device

### Request

`DELETE /devices/id`

    curl -i -H 'Accept: application/json' -X DELETE http://localhost:7000/devices/1/

### Response

    HTTP/1.1 204 No Content
    Date: Thu, 24 Feb 2011 12:36:32 GMT
    Status: 204 No Content
    Connection: close

