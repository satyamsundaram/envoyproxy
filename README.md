Here, we configure envoy proxy to:
- handle http request at port 80 and use apache to serve backend website
- configure mirror traffic and mirror http requests to another backend website (say, served by Nginx)
- configure access logs to be stored in a file in JSON format
- configure LUA filter for POST request body and fetch this key value pair: "name: <random>" to be set as header dynamically
- configure decompression filter

Any traffic coming to port 80 will be handled by envoy proxy and will be forwarded to the apache server and mirrored to our nginx server as well. The apache server will serve the website and the response will be sent back to the client. The client will not be aware of the proxy in between.

**What our custom log looks like:**
```json
{"path":"/","http.request.method":"POST","http.response.body.bytes":"219","upstream_service_time":"1","method":"POST","start_time":"2023-09-06T05:07:05.484Z","response_flags":"-","status_code":"200","name":"satyam","response_duration":"3","bytes_received":"18","bytes_sent":"219"}
```
