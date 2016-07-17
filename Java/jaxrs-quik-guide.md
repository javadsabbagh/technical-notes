
```bash
curl http://www.apress.com/resource/csv/bookcategory?cat=32 | sed -n 2~1p | wc -l

curl -v http://www.apress.com/book/catalog?category=32
	-v means verbose
	-X specifies http method
```	

Content Types
	text/html
	text/plain
	image/gif, image/jpeg, image/png
	text/xml, application/xm
	application/json


```java
@Path("/book")
public class BookResource {
	@GET
	@Produces("text/plain")
	public String getBookTitle() {
		return "H2G2";
	}
}



@Path("books")
@Stateless
@Produces({"application/xml", "application/json"})
@Consumes({"application/xml", "application/json"})

@Produces({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})
@Consumes({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})


MIME Types Defined in javax.ws.rs.core.MediaType
	APPLICATION_ATOM_XML			"application/atom+xml"
	APPLICATION_FORM_URLENCODED		"application/x-www-form-urlencoded"
	APPLICATION_JSON 				"application/json"
	APPLICATION_OCTET_STREAM 		"application/octet-stream"
	APPLICATION_SVG_XML 			"application/svg+xml"
	APPLICATION_XHTML_XML 			"application/xhtml+xml"
	APPLICATION_XML 				"application/xml"
	MULTIPART_FORM_DATA 			"multipart/form-data"
	TEXT_HTML 						"text/html"
	TEXT_PLAIN 						"text/plain"
	TEXT_XML 						"text/xml"
	WILDCARD 						"*/*"


@Path("/customers")
@Produces(MediaType.TEXT_PLAIN)
public class CustomerResource {

	@GET
	public String getAsPlainText() {
	// ...
	}

	@GET
	@Produces(MediaType.TEXT_HTML)
	public String getAsHtml() {
	// ...
	}

	@GET
	@Produces(MediaType.APPLICATION_JSON)
	public List<Customer> getAsJson() {
	// ...
	}

	@PUT
	@Consumes(MediaType.TEXT_PLAIN)
	public void putBasic(String customer) {
	// ...
	}

	@POST
	@Consumes(MediaType.APPLICATION_XML)
	public Response createCustomer(InputStream is) {
	// ...
	}

}
```

If a resource is capable of producing more than one Internet media type, the resource method
chosen will correspond to the most acceptable media type, as declared by the client in the Accept
header of the HTTP request. For example, if the Accept header is:
	Accept: text/plain

Accept: text/plain; q=0.8, text/html

Note Jersey adds a BadgerFish mapping of JAXB XML to JSON. BadgerFish ( http://badgerfish.ning.com/ )
is a convention for translating an XML document into a JSON object so it’s easy to manipulate within JavaScript.


```java

@Context
private UriInfo uriInfo;

@GET
public List<Book> getAllBooks()

@POST
public Response createNewBook(JAXBElement<Book> bookJaxb)

// return response after persisting bookJaxb

URI bookUri = uriInfo.getAbsolutePathBuilder().path(book.getId().toString()).build();
return Response.created(bookUri).build();

@Path("/customers/{customername}")


@DELETE
@Path("{itemid}")
public void deleteItem(@PathParam("itemid") String itemid)


@GET
@Path("/books/{bookid}")
public Book getBook(@PathParam("bookid") String bookid


Extracting Parameters
	JAX-RS provides a rich set of annotations to extract the different parameters that a request could send (@QueryParam, @MatrixParam, 
		@CookieParam, @HeaderParam, and @FormParam)


@GET
public Customer getCustomerByZipCode(@QueryParam("zip") Long zip)

@GET
public Book getBook(@CookieParam("sessionid") int sessionid)

@FormParam
@DefaultValue
@GET
public Response getCustomers(@DefaultValue("50") @QueryParam("age") int age)

```


```bash
curl -X POST --data-binary "{ \"title\":\"H2G2\", \"description\":\"Scifi IT book\", \"illustrations\":\"false\",\"isbn\":\"134-234\",\"nbOfPage\":\"241\", \"price\":\"24.0\" }" -H "Content-Type: application/json"  http://localhost:8080/chapter15-resource-2.0/rs/books –v
curl -X GET -H "Accept: application/json"  http://localhost:8080/chapter15-resource-2.0/rs/books/601
curl -X GET -H "Accept: application/xml"  http://localhost:8080/chapter15-resource-2.0/rs/books/601
curl -X DELETE http://localhost:8080/chapter15-resource-2.0/rs/books/601 -v
```

```java
@ApplicationPath("rs")
public class ApplicationConfig extends Application {
}
```

```bash
curl -X GET -H "Accept: application/json"  http://localhost:8080/chapter15-resource-2.0/rs/books
curl -X DELETE http://localhost:8080/chapter15-resource-2.0/rs/books/601


$ asadmin deploy chapter15-resource-2.0.war

$ asadmin list-components
	chapter15-resource-2.0 <ejb, web>


// Creates a book
curl -X POST --data-binary "{ \"title\":\"H2G2\", \"description\":\"Scifi IT book\", \"illustrations\":\"false\",\"isbn\":\"134-234\",\"nbOfPage\":\"241\", \"price\":\"24.0\" }" -H "Content-Type: application/json" http://localhost:8080/chapter15-resource-2.0/rs/books


// Returns all the books
curl -X GET -H "Accept: application/json" http://localhost:8080/chapter15-resource-2.0/rs/books 


// Returns the book with ID 601 in JSON
curl -X GET -H "Accept: application/json" http://localhost:8080/chapter15-resource-2.0/rs/books/601 
{"description":"Scifi IT book","illustrations":"false","isbn":"1234-234","nbOfPage":"241","price":"24.0","title":"H2G2"}


// Returns the book with ID 601 in XML
curl -X GET -H "Accept: application/xml"  http://localhost:8080/chapter15-resource-2.0/rs/books/601
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<book><description>Scifi IT book</description>
<illustrations>false</illustrations><isbn>1234-234</isbn>
<nbOfPage>241</nbOfPage><price>24.0</price><title>H2G2</title></book>


// Deletes the book with ID 601
curl -X DELETE http://localhost:8080/chapter15-resource-2.0/rs/books/601
```

