Blogging-Site-Project-
Author Model:- { fname: { mandatory}, lname: {mandatory}, title: {mandatory, enum[Mr, Mrs, Miss]}, email: {mandatory, valid email, unique}, password: {mandatory} }

Blogs Model:- { title: {mandatory}, body: {mandatory}, authorId: {mandatory, refs to author model}, tags: {array of string}, category: {string, mandatory, examples: [technology, entertainment, life style, food, fashion]}, subcategory: {array of string, examples[technology-[web development, mobile development, AI, ML etc]] }, createdAt, updatedAt, deletedAt: {when the document is deleted}, isDeleted: {boolean, default: false}, publishedAt: {when the blog is published}, isPublished: {boolean, default: false}}

-- Author APIs /authors --

Create an author - atleast 5 authors Create a author document from request body. Endpoint: BASE_URL/authors

-- POST /blogs --

Create a blog document from request body. Get authorId in request body only.

Make sure the authorId is a valid authorId by checking the author exist in the authors collection.

Return HTTP status 201 on a succesful blog creation. Also return the blog document. The response should be a JSON object like this

Create atleast 5 blogs for each author

Return HTTP status 400 for an invalid request with a response body like this

-- GET /blogs --

Returns all blogs in the collection that aren't deleted and are published Return the HTTP status 200 if any documents are found. The response structure should be like this If no documents are found then return an HTTP status 404 with a response like this Filter blogs list by applying filters. Query param can have any combination of below filters. By author Id By category List of blogs that have a specific tag List of blogs that have a specific subcategory example of a query url: blogs?filtername=filtervalue&f2=fv2

-- PUT /blogs/:blogId --

Updates a blog by changing the its title, body, adding tags, adding a subcategory. (Assuming tag and subcategory received in body is need to be added) Updates a blog by changing its publish status i.e. adds publishedAt date and set published to true Check if the blogId exists (must have isDeleted false). If it doesn't, return an HTTP status 404 with a response body like this Return an HTTP status 200 if updated successfully with a body like this Also make sure in the response you return the updated blog document.

-- DELETE /blogs/:blogId --

Check if the blogId exists( and is not deleted). If it does, mark it deleted and return an HTTP status 200 without any response body. If the blog document doesn't exist then return an HTTP status of 404 with a body like this

DELETE /blogs?queryParams

Delete blog documents by category, authorid, tag name, subcategory name, unpublished If the blog document doesn't exist then return an HTTP status of 404 with a body like this

Add authentication and authroisation feature POST /login Allow an author to login with their email and password. On a successful login attempt return a JWT token contatining the authorId If the credentials are incorrect return a suitable error message with a valid HTTP status code

Add an authorisation implementation for the JWT token that validates the token before every protected endpoint is called. If the validation fails, return a suitable error message with a corresponding HTTP status code Protected routes are create a blog, edit a blog, get the list of blogs, delete a blog(s) Set the token, once validated, in the request - x-api-key Use a middleware for authentication purpose.

Make sure that only the owner of the blogs is able to edit or delete the blog. In case of unauthorized access return an appropirate error message. Testing (Self-evaluation During Development) To test these apis create a new collection in Postman named Project 1 Blogging Each api should have a new request in this collection Each request in the collection should be rightly named. Eg Create author, Create blog, Get blogs etc Each member of each team should have their tests in running state Refer below sample

A Postman collection and request sample

Response Successful Response structure { status: true, data: {

} } Error Response structure { status: false, msg: "" } Collections Blogs { "title": "How to win friends", "body": "Blog body", "tags": ["Book", "Friends", "Self help"], "category": "Book", "subcategory": ["Non fiction", "Self Help"], "published": false, "publishedAt": "", // if published is true publishedAt will have a date 2021-09-17T04:25:07.803Z "deleted": false,