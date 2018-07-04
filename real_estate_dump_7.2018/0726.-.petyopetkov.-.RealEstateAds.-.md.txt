# RealEstateAds
Web services for real estate ads using ASP.NET Web API 2 

## Routes

* Login and Register Services
	* Register User
		* Url: http://localhost:XXXXX/api/account/register
		* Method: Post
		* Headers: Content-Type: application/x-www-form-urlencoded
		* Request Body: Username=ivanivanov&Email=ivan@ivan.com&Password=123456&ConfirmPassword=123456
	* Login User
		* Url: http://localhost:XXXXX/api/account/login
		* Method: Post
		* Headers: Content-Type: application/x-www-form-urlencoded
		* Request Body: Username=ivanivanov&Password=123456
* Real estate Services
	* Get public real estates: 
	Does not require authentication. Returns paged real estates, added previously from users. Skip and Take are optional query string parameters. If they are missing, default skip is 0 and default take is 10. Take cannot be more than 100. Real estates are sorted by their time of creation in descending order.
		* Url: http://localhost:XXXXX/api/RealEstates?skip=2&take=5 
		* Method: GET
		* Headers: Content-Type: application/json
		* Request Body: Empty
	* Get public real estate details:
	Does not require authentication. Returns part of the full information for a real estate by the provided ID.
		* Url: http://localhost:XXXXX/api/RealEstates/ID
		* Method: GET
		* Headers: Content-Type: application/json
		* Request Body: Empty
	* Get private real estate details:
	Requires an authentication. Returns the same as above but with additional contact information and comments for each real estate.
		* Url: http://localhost:XXXXX/api/RealEstates/ID
		* Method: GET
		* Headers: Content-Type: application/json, Authorization: Bearer ACCESS_TOKEN (received after login)
		* Request Body: Empty
	* Create new real estate ad:
	Requires authentication. Creates a new real estate ad.
		* Url: http://localhost:XXXXX/api/RealEstates
		* Method: Post
		* Headers: Content-Type: application/json, Authorization: Bearer ACCESS_TOKEN (received after login)
		* Request Body: 
			Example:
			{
				"Title": "title 1",
				"Description": "Description 1",
				"Address": "Address 1",
				"Contact": "555-555-555",
				"ConstructionYear": 2005,
				"SellingPrice": 100000,
				"RentingPrice": 500,
				"Type": 2
			}
* Comments Services
	* Get comments for real estate:
	Requires an authentication. Returns paged comments for a real estate provided by real estate id, added previously from users. Skip and Take are optional query string parameters. If they are missing, default skip is 0 and default take is 10. Take cannot be more than 100. Comments are sorted by their time of creation in ascending order.
		* Url: http://localhost:XXXXX/api/Comments/ID?skip=2&take=5  
		* Method: GET
		* Headers: Content-Type: application/json, Authorization: Bearer ACCESS_TOKEN (received after login)
		* Request Body: Empty
	* Get comments for specific users:
	Requires an authentication. Returns paged comments from specific user provided by username. Skip and Take are optional query string parameters. If they are missing, default skip is 0 and default take is 10. Take cannot be more than 100. Comments are sorted by their time of creation in ascending order.
		* Url: http://localhost:XXXXX/api/Comments/ByUser/USERNAME?skip=2&take=5
		* Method: GET
		* Headers: Content-Type: application/json, Authorization: Bearer ACCESS_TOKEN (received after login)
		* Headers: Empty
	* Add new comment for real estate:
	Requires an authentication. Adds a comment to a specific real estate.
		* Url: http://localhost:XXXXX/api/Comments
		* Method: Post
		* Headers: Content-Type: application/json, Authorization: Bearer ACCESS_TOKEN (received after login)
		* Request Body:
			Example:
			{
				"RealEstateId": 2,
				"Content": "Some text some text"
			}
* Users Services
	* User Details:
	Does not require authentication. Returns statistics about a user by providing his/her username – total real estates, total comments, average rating.
		* Url: http://localhost:XXXXX/api/Users/USERNAME
		* Method: GET
		* Headers: Content-Type: application/json
		* Request Body: Empty
	* Rate user
	Adds new rating to the user, from 1 to 5. Users cannot rate themselves. Multiple ratings can be given by the same user.
		* Url: http://localhost:XXXXX/api/Users/Rate 
		* Method: PUT
		* Headers: Content-Type: application/json, Authorization: Bearer ACCESS_TOKEN (received after login)
		* Request Body:
			Example:
			{
			   "UserId": "97bfc79b-896b-42a9-b20e-efff78508689",
			   "Value": "4"
			}






	


