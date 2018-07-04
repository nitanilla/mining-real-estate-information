# Unreal Estate

Unreal Estate is a simple RESTful web app that allows the user to find Real Estate listings they might be interested in. Unreal Estate is built on Laravel 5 and PHP 7.

## Listing Updates

The application maintains its own database of real estate listings. These listings are updated daily (2:00AM EST) from an external source.

## API Usage

There are two endpoints available for reading listing data, and one endpoint for modifying listing data.

### Get All Listings

Retrieves all listings as an array of JSON objects

- **URL** `/listings`
- **Method** `GET`
- **Success Response**
  - **Code**: 200
  - **Content**: `{ [ { <Listing0> }, ... ] }`

### Get Paginated Listings

Retrieves a partial collection of all listings as an array of JSON objects. Sorting, filtering, and pagination is done via query parameters.

- **URL** `/paginated_listings`
- **Method** `GET`
- **URL Parameters** _All parameters are optional, some have default values if not specified_

| Parameter | Description | Allowed Values |  Default |
| ----- | ------ | ------ | ------ |
| page | specifies the page to show | any positive, non-zero integer | 1 |
| results_per_page | specifies the number of results to show per page | any positive, non-zero integer | 1 |
| photos_only | returns only photos from the listings | `true` or `false` | `false` |
| sort | specifies how to sort the returned listings | [Sorting Expression](https://github.com/thejettdurham/unrealestate/wiki/Sorting-Expressions), only `list_price` and `listing_date` fields | _none_ |

_if no sorting is specified, no sorting will be explicitly applied and there are no guarantees what order the results will be in_

- **Success Response**
  - **Code**: 206
  - **Content**: `{ [ { <Listing0> }, ... ] }`
- **Error Responses**
  - _Errors in URL parameters_
    - **Code**: 400
    - **Content**: `{ "error": "there was an error with the query parameters" }`
  - _No data for given pagination parameters_
    - **Code**: 404
    - **Content**: _none_


### Toggle Listing Activation

Allows user to activate or deactivate a listing. The behavior of this endpoint is toggling, so calling the endpoint when the listing is inactive will activate it, and vice-versa.

The endpoint also returns the representation of the affected listing as a JSON object.

- **URL** `/listings/:id/toggle_activation`
- **Method** `PUT`
- **Success Response**
  - **Code**: 200
  - **Content**: `{ <Listing> }`
- **Error Responses**
  - _No Listing for id_
    - **Code**: 404
    - **Content**: _none_ 
