# Status Codes

## Learning Goals

- Define status codes and what they communicate to a client
- Describe the structure and various categories of status codes
- Set a response's status code in Rack 


## Why Status Codes are Important for the Client

Status codes allow your server to tell something special to the client. The responses you send need to be effective to both a human user and to the browser itself. That means that  response messages like `File Not Found` or `Item isn't in the cart` work if there is a human to read the English. Browsers also want to know the status of the response. To get that response, the HTTP protocol has an agreed upon contract for different "status codes". A status code is a 3-digit integer where the first digit represents the class of the response, and the remaining two digits represent a specific status. There are 5 primary values that the first digit can take.  

### Status Code Chart

<table border="1" cellpadding="4" cellspacing="0">
  <tr>
    <th>Status Number</th>
    <th>Code/Description</th>
  </tr>
  
  <tr>
    <td>1</td>
    <td>1xx: Informational (request received and continuing process)</td>
  </tr>
  <tr>
    <td>2</td>
    <td>2xx: Success (request successfully received, understood, and accepted)</td>
  </tr>
  <tr>
    <td>3</td>
    <td>3xx: Redirection (further action must be taken to complete request)</td>
  </tr>
  <tr>
    <td>4</td>
    <td>4xx: Client Error (request contains bad syntax and can't be completed)</td>
  </tr>
  <tr>
    <td>5</td>
    <td>5xx: Server Error (server couldn't complete request)</td>
  </tr>
</table>

You've probably seen a bunch of these before, the most common being `404`. This means that the server couldn't find the route you requested.

### Status Codes in Rack

In Rack, we are able to set the response's status code by just setting the status_code attribute. By default, Rack sets a status code of `200`. But when a user selects a route that doesn't exist, we need to set the `status` to `404`. 

```ruby
class Application
  
  def call(env)
    resp = Rack::Response.new
    req = Rack::Request.new(env)

    if req.path=="/songs"
      resp.write "You requested the songs"
    else
      resp.write "Route not found"
      resp.status = 404
    end

    resp.finish
  end
end
```

Now if you go to `localhost:9292/badURL` you'll get the error message, and if you open up the Inspect Element navigator you'll see something like this:

![](http://readme-pics.s3.amazonaws.com/rack-status-codes-readme/image1.png)

## Video Reviews

* [How the Web Works, Part 1](https://www.youtube.com/watch?v=gI9wqEDPiY0)

* [How the Web Works, Part 2](https://www.youtube.com/watch?v=LSUevS1PRTg)

### Resources
* [More on Status Codes](http://www.tutorialspoint.com/http/http_status_codes.htm)
