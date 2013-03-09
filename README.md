# web-dna

This is an Express based REST API for discovering the content type of URLs.

## Installation
```
$ npm install
```

## Configuration

The server is configured by changing the settings in `config/default.json`. These settings include:

  - `server` settings for the server
    - `bindIP` the IP or hostname to use for the server (e.g., localhost).
    - `bindPort` the Port number to use for the server (e.g., 8888).  If using a port number lower than 1024, the server will have to be run as root.

## How to use
```
$ node app.js
```

## API

The web-dna server expects a URL in the following form:

    http://<bindIP>:<bindPort>/api/url/<url>

The server takes the URL and attempts to do two things. First, it gets the actual URL in the case that a URL shortener has been used, or other redirects. Second, it requests the HTTP headers for this resource, and determins the `content-type` that is being used. Both pieces of information are returned as JSON.

Assuming a web-dna server running on `http://localhost:8888`, the following are valid API calls:

### Example 1: simple url
```
http://localhost:8888/api/url/http://google.com

{
  "href": "http://www.google.ca/",
  "contentType": "text/html; charset=ISO-8859-1"
}
```

### Example 2: shortened url
```
http://localhost:8888/api/url/http://bit.ly/900913

{
  "href": "http://www.google.ca/",
  "contentType": "text/html; charset=ISO-8859-1"
}
```

### Example 3: image resource
```
http://localhost:8888/api/url/http://i.imgur.com/syPS3rG.jpg

{
  "href": "http://i.imgur.com/syPS3rG.jpg",
  "contentType": "image/jpeg"
}
```

### Example 4: video resource
```
http://localhost:8888/api/url/http://archive.org/download/PET1018_R-2_LA/PET1018_R-2_LA.mp4

{
  "href": "http://ia700805.us.archive.org/2/items/PET1018_R-2_LA/PET1018_R-2_LA.mp4",
  "contentType": "video/mp4"
}
```

## License

Copyright 2013 David Humphrey <david.humphrey@senecacollege.ca>

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.