# Camel based implementation of the _Skosmos API_ API

## API Description ##
The Skosmos REST API is a read-only interface to the data stored on the vocabulary server. The URL namespace is the base URL of the Skosmos instance followed by &#96;/rest/v1/&#96;. &#10;&#10;Most methods return the data as UTF-8 encoded JSON-LD, served using the &#96;application/json&#96; MIME type. The data consists of a single JSON object which includes JSON-LD context information (in the &#96;@context&#96; field) and one or more fields which contain the actual data. Some methods (&#96;data&#96;) return other formats (RDF/XML, Turtle, RDF/JSON) with the appropriate MIME type.&#10;&#10;The API supports Cross-Origin Resource Sharing by setting the Access-Control-Allow-Origin HTTP header to &#96;&quot;*&quot;&#96; for all requests.&#10;&#10;The API supports the JSONP convention of appending a callback parameter to any URL. The returned data will then be wrapped in a JavaScript function call using the function name provided as the callback parameter value. JSONP wrapped data will be served using the &#96;application/javascript&#96; MIME type.&#10;

### Building

    mvn clean package

### Running Locally

    mvn spring-boot:run

Getting the API docs:

    curl http://localhost:8080/openapi.json

## Running on OpenShift

    mvn fabric8:deploy

You can expose the service externally using the following command:

    oc expose svc skosmos-api

And then you can access it's OpenAPI docs hosted by the service at:

    curl -s http://$(oc get route skosmos-api --template={{.spec.host}})/openapi.json
