# SAFE API and React Helper For Web Apps (Preliminary)

#### Purpose: to make it as easy as possible to make web apps that interact with the SAFE Network created by MaidSafe

As of this writing (2016-02-14) the SAFE api has not been released, but a general idea of its workings allows for an api to be created that will resemble the real thing. This library serves multiple purposes:

* provides an API wrapper that makes CRUD operations on SAFE very easy
* establishes guidelines on how to structure/organize entities and collections in an app
* takes care of state and cache management
* provides an additional wrapper that makes writing [React](https://facebook.github.io/react/) apps a breeze

The "network" currently uses Firebase to replicate SAFE functionality, as they offer many similarities such as built-in authentication, URI based data, GET/PUT/DELETE functionality, etc. Firebase will be replaced with the test network as soon as possible.

**This api is in a pre-alpha state, and is subject to breaking changes. Use at your own risk.**

[Click here](https://github.com/eblanshey/safe-demo) for a demo app created using this API.

### Theory and Understanding App Architecture

In order to use the API, a common convention for organizing data must be used. I will use the example of a simple app that functions as a directory of apps on the SAFE network. Users can post SAFE apps they are working on, as well as "like" other peoples' apps. The demo I made is exactly this directory. Having an app that contains other apps is confusing, so I will refer to the apps that users submit as "posts" from now on.

There are two types of objects that can be stored: entities and collections. An **entity** stores the actual information. In our case, a "post" is an entity that holds a "name", "description", and other values related to the post. A **collection** is an array of *pointers* to other entities, unless the data is *static* in that it usually doesn't change (e.g. created by the admin only, such as a list of categories). The list of posts would be our collection. It is important that entities are not contained within collection objects, but rather the information that allows us to locate the entities.

In SAFE, data is distributed without any central servers, so content is self-moderated. There is no organization that owns your data, which means that the users who submit data actually own it themselves in their own "virtual drive" that exists on the network; no one else can modify or delete them.

In order to allow for efficient storage, retrieval, caching, maintenance, and more, entities and collections should be as *flat* as possible, only holding information not shared with other objects (such as category names). Think of a post that can be assigned to multiple categories. Instead of having an entity that looks like this...

```javascript
{
	title: 'My App',
    description: 'The best app',
    categories: [
    	'finance',
        'real estate'
    ]
}
```

the app creator should have a separate collection of categories, which the entities point to:

```javascript
// The admins's collection
{
	"1": "finance",
    "2": "chat",
    "3": "real estate"
}

// Entity
{
	title: 'My App',
    description: 'The best app',
    categories: ["1", "3"]
}
```

There are numerous benefits.

* It's easy to rename or change categories across the app -- the admin simply renames them
* The complete list of categories only needs to be downloaded once
* Entities takes a lot less hard drive space and bandwidth

The more complex the data structure, the more benefits such a flat structure has. The same idea should be used for all relations between all objects.

Let us analyze the owners of objects in our app: there needs to be one source for the collection of posts in our directory. The admin, or app creator, is a natural choice, so this collection would be located on his "virtual drive". Each post would be owned by its submitter, so those entities will be located on the submitter's drive. The posts collection on the admin's drive will contains pointers to the location of each post entity on *other* peoples' drives. 

Each post can have many likes: that sounds like a collection! Since the collection is related to the submitter's post, the submitter is the one that owns the collection. But what if he cheats and alters the amount of likes on his post? That's where the "like" entity comes in: every person that likes a post will have a "like" entity created on his own drive, that contains information on the post he likes, creating a two-way reference between the likes collection and like entities. To count the number of likes on a post, the app developer will fetch both the collection and entities of likes. For each collection item, there must be a matching like entity that points back to the post.

In a perfect world, no malicious manipulation would occur. It is still possible that a collection owner can remove *references* to entities that exist on others' drives, thereby effectively removing their ability to be seen. However, since all data is public, backup and caching features could be implemented straight into the app that would make this very easy to detect. For example, in the case of an evil administrator removing posts from his app for no good reason, another app could easily take its place, *while making use of the same data, because it is public.* All of the entities still exist and could be re-referenced by another collection owner.

Every object requires 4 "identifiers" in order to be able to locate it:

1. is it an **entity** or **collection**?
2. what is the name of the entity or collection? e.g. "post", "postList", "thread", "profile", etc
3. what is the userid of the owner of the object?
4. what is the unique ID of the object? (applicable to entities only)

With this information, we can locate an object using a URI like so:

`/users/userNumber1/entities/posts/4224`

OR 

`/users/userNumber1/collections/posts`

In fact, this is exactly how information is stored on Firebase, and a similar structure will be used on the SAFE network. In the case of the entity, the "file" at "4224" will contain the entity data. Thus the file name acts as the object ID; it does not need to be contained within the object data.

It is important to note that the implementation of collections in this api will most likely differ greatly from the real thing, using structured data. There is currently little info available about how it will work, so the implementation as described here will suffice for now. Here is what a collection of posts stored at the above URI (`/users/userNumber1/collections/posts`) could look like:

```javascript
{
	"postid1": {
    	userid: "userNumber1",
        createdAt: 1455497107 // timestamp
    },
    "postid2": {
    	userid: "userNumber2",
        createdAt: 1455497107
    }
    // ...
}
```

The above structure will allow the app developer to find each entity in the collection. *(Discussion point: should the app know that this collection contains entities, or should it be explicit with a `objectType` key? This might allow for automated nested object retrieval in the future)*

All of the above concepts are used in the [demo React app](https://github.com/eblanshey/safe-demo).

### Installation and Setup

Assuming you have NPM installed: `npm install safe-api`

Since this api currently uses Firebase, create a free account and an application there. At the entry point of your code, set the config to use your application:

```javascript
import { setup } from 'safe-api'

// e.g. if your app is at https://my-app.firebaseio.com
setup({ firebaseApp: 'my-app' }) 
```

In the Firebase Rules section, copy and paste the contents of `firebase-rules.json` into the box and press "Save Rules". The rules are set up to allow full read permissions on all data. Only entity owners have write permissions on their entities, and everyone has write permissions on collections. This is a temporary security hole until we transition to SAFE collections. Ideally only the owners of a specific collection item would be able to edit or remove those collection items.

### Raw API Methods

```javascript
import { api } from 'safe-api'
```

Methods on the "api" object:

#### signup(email, password) (Firebase only)

Creates a new authenticated user on Firebase with the provided email and password, and automatically logs him in. No email verification required. Not sure at this time how this will look like with the SAFE Network. Will authentication/signup be done by the SAFE browser extension, or will apps assume everyone is automatically logged in?

**Returns:** a promise with the userid as generated by firebase. Example: `42d9c8e2-4b4b-4879-918c-633fb2474b9b`

**Example:**
```javascript
api.signup('my@email', 'somethingaboutahorsestaple')
   .then((userid) => console.log('The userid is ' + userid))
```

#### login(email, password) (Firebase only)

Logs a user in by email and password.

**Returns:** a promise with the userid as generated by firebase. Example: `42d9c8e2-4b4b-4879-918c-633fb2474b9b`

**Example:**
```javascript
api.login('my@email', 'somethingaboutahorsestaple')
   .then((userid) => console.log('The userid is ' + userid))
```

#### getEntity(name, userid, id)

Fetches the requested entity, identified by the the owner (userid), the entity ID, and the name of the entity.

**Arguments**: 

`name` (*string*): the name of the entity. For example, "posts", "profiles", "likes", etc. Names can be singular if you prefer, just make sure to keep it consistent across your app.

`userid` (*string*): the owner of the entity. Use the userid that Firebase provides.

`id` (*string*): a unique ID for the entity. The app will need to generate this using its own UUID generator. Example: `b2509e6d-1a7f-44f4-96d7-06c1df9efdef`. *Please raise an issue if you think the UUID generator should be an API method.*

**Returns**: a promise containing the exact data on the network.

**Example**:

```javascript
api.getEntity('posts', '42d9c8e2-4b4b-4879-918c-633fb2474b9b', 'b2509e6d-1a7f-44f4-96d7-06c1df9efdef')
   .then((postData) => console.log(postData))
```

#### loadEntity(name, userid, id)

Same as above, but if the entity was previously fetched, it will return the cached copy. It is safe and fast to use this throughout the app in order to prevent GETTING the same entity numerous times. Use `getEntity()` above if you need to ensure up-to-date data.

#### putEntity(name, userid, id, data)

Puts the provided `data` as-is to the location as specified by name, userid, and id. If data already exists at that location, it will be overwritten. You may provide an object, string, integer, or array.

**Returns**: a promise containing the exact data added to the network, resolved when the PUT was completed.

**Example**:

```javascript
const post = {
	title: "My app",
    description: "The best app"
}

api.putEntity('posts', '42d9c8e2-4b4b-4879-918c-633fb2474b9b', 'b2509e6d-1a7f-44f4-96d7-06c1df9efdef', post)
   .then((postData) => console.log('Successfully added the post!', postData))
```

#### deleteEntity(name, userid, id)

Deletes the entity at the given location.

**Returns**: promise

**Example**:

```javascript
api.deleteEntity('posts', '42d9c8e2-4b4b-4879-918c-633fb2474b9b', 'b2509e6d-1a7f-44f4-96d7-06c1df9efdef')
   .then((postData) => console.log('Successfully deleted the post!', postData))
```

#### getCollection(name, userid)

Fetches the entire collection, identified by the the owner (userid) and the name of the collection. Pagination and ordering is not currently supported as it is not yet clear how it will work on SAFE.

**Arguments**: 

`name` (*string*): the name of the collection. For example, "posts", "profiles", "likes", etc. You can have names that have entities with the same name if you wish, or differentiate them like "postEntity" and "postCollection". It doesn't matter.

`userid` (*string*): the owner of the collection. Use the userid that Firebase provides.

**Returns**: a promise containing an object with all the items in the collection. The keys of the object are whatever you specified as the id of the collection items you put (see `putCollectionItem()` below).

**Example**:

```javascript
api.getCollection('posts', '42d9c8e2-4b4b-4879-918c-633fb2474b9b')
   .then((posts) => {
      for (let id in posts) {
      	 console.log('I am doing something with post '+id+'!', posts[id])
      }
   })
```

#### loadCollection(name, userid)

Same as above, but if the collection was previously fetched, it will return the cached copy. It is safe and fast to use this throughout the app in order to prevent GETTING the same entity numerous times. Use `getEntity()` above if you need to ensure up-to-date data.

#### putCollectionItem(name, userid, collectionItemId, collectionItem)

Adds a new item to an existing collection, or if no collection exists, a new collection is created. The collection is an object containing key-value pairs. The key is the ID of the collection item (such as a post id), and the value is whatever data you set there, such as an object containing the userid of the post owner.

**Returns**: a promise containing the collectionItem data.

**Example**:

```javascript
const postId = 'b2509e6d-1a7f-44f4-96d7-06c1df9efdef',
	postMeta = {
    	userid: "c4630597-1c32-4bc1-8385-f66e3fa93a7b" // who owns the post
    }

// The admin owns the "posts" collection, and a new post is added to it with its ID and its owner's userid.
api.putCollectionItem('posts', adminId, postId, postMeta)
   .then((post) => console.log('Successfully added the collection item!', post))
```

#### deleteCollectionItem(name, userid, collectionItemId)

Delete the collection item at it `collectionItemId`.

**Returns**: promise

**Example**:

```javascript
api.deleteCollectionItem('posts', adminId, postId)
   .then(() => console.log('Deleted the post collection item!'))
```

#### deleteEntireCollection(name, userid)

Deletes the *entire* provided collection. *Note: this will likely not have a corresponding SAFE action, and might be deleted in the future.*

**Returns**: promise

**Example**:

```javascript
api.deleteEntireCollection('posts', adminId)
   .then(() => console.log('Deleted the whole posts collection!'))
```

#### getAuthData()

Gets the `auth` object that Firebase provides. It contains a `uid` property which is the logged-in userid. A similar object will be provided by the SAFE application.

### Advanced Usage

Behind the scenes, [Redux](http://redux.js.org/index.html) is used to manage the state and cache of all the objects. In addition to storing data, it also holds errors and loading indicators for all requests. You can tap into this to help build your application. The api object includes a `getStore()` method that returns the redux store. You may use it to subscribe to any changes that happen to the entire store using the pub-sub pattern. This will allow you to be notified when an object is being loaded, when it has completed, or the error if it failed. Look at `store-structure.js` to see the architecture of the store. ImmutableJS is used to store and manipulate the state.

Please read the Redux documentation if you wish to use this feature, **--OR--** if you use React, just use the React helper below for an easy way to tap into those features without having to know anything about Redux or state management!

### React Library

If you are familiar with the excellent React framework, then using the React helper will make app development even easier. It allows you to easily inject SAFE objects directly into your components, and automatically update components whenever state changes, which can be used for displaying loading gifs, error messages, immediately loading object relations, and more. This library can act as your primary state manager, so usage of other libraries such as Flux implementations are not required. Note that in this section I am assuming you are already familiar with React.

```javascript
import React, { Component } from 'react'
import { connectToSafe, h } from 'safe-api'

class ToDoList extends Component {
  render() {
    const props = this.props

    if (!props.auth.uid) {
      return <div>You must be logged in to view this list!</div>
    }

    if (!props.toDoList.data) {
      return <div>Loading to-do list...</div>
    }

    let toDos = [],
      data = props.toDoList.data

    for (let key in data) {
      toDos.push(<li>{data[key].title}</li>)
    }

    return (
      <ul>
        {toDos}
      </ul>
    )
  }
}

function mapPropsToSafe(props) {
  return [
    h(['toDoCollection', props.userid], 'toDoList'),
    h('auth', 'auth'),
  ]
}

export default connectToSafe(mapPropsToSafe)(ToDoList)
```

There are two functions you should be familiar with: `connecToSafe()` and `h()`.

#### connectToSafe(mapPropsToSafe)

Attaches SAFE objects to an existing component. The existing component is not altered, but additional props (your SAFE objects) will be passed to it.

Its argument takes a function that returns an array of SAFE object identifiers called SafeObject (see `h()` below). This array will be used to determine which objects you want your component to use. Every time a SAFE operation is made, whether GETTING or PUTTING, this function will be called.

Instead of using the component you made, use the one that `connectToSafe()` will return instead. Note that it should be invoked two times: the first time with the function that returns the array of object identifiers, and the second with the actual component that you wish to be injected with those objects: `connectToSafe(mapPropsToSafe)(ToDoList)`

The SAFE props added to your component will have the following format: 

```javascript
{
	// true if it's currently being fetched
	loading: false, 
    // String error message if there was an issue fetching the object. 
    // Reverts to null when loading or putting entity.
    error: null, 
    // If data has not yet been fetched at all, data will be 'undefined'
    // If data has been fetched but the object does not exist, it will be null
    // If data was fetched and fount, it will be set to the "data" property as-is.
    data: {}
}
```

Additionally, by default there will always be an `api` prop added to each injected component; it will contain all the methods found in the **Raw API Methods** section above.

The entities and collections you request will automatically be retrieved from the SAFE network. If a cached copy already exists, it will be used. Use the `getEntity()` or `getCollection()` API methods to force an update.

#### h(identification, propName, hierarchyCallback)

When returning the array of object identifiers from `mapPropsToSafe`, each array element should return the result of this function, which we will call a SafeObject. This object will be used for instructions on how to fetch the objects from SAFE.

**Arguments**: 

`identification` (*array|string*): This indicates how to find the object you want.

For *collections*, pass an array with the collection name as the first value, and the userid that owns the collection as the second value: `['appList', 'c4630597-1c32-4bc1-8385-f66e3fa93a7b']`.

For *entities*, pass an array with the entity name as the first value, the userid that owns the entity as the second value, and the id of the entity as the third value: `['appList', 'c4630597-1c32-4bc1-8385-f66e3fa93a7b', 'b2509e6d-1a7f-44f4-96d7-06c1df9efdef']`. Three array values indicates an entity, two array values indicates a collection.

For `auth data`, pass the string `'auth'`.

`propName` (*string*): the name of the prop your component will use. In the example code above, the *toDoCollection* will be passed with a prop of `toDoList`, and the *auth data* with a prop name of `auth`. You can use it like normal in your component: `this.props.auth`. If you append `{}` to the end of the prop name, then the prop will be an object map that contains your SAFE object. See below for details.

`hierarchyCallback` (*function*): what if you want to load objects from SAFE, but rely on other SAFE objects to determine which ones to load? For example, you may load a collection of posts, but the collection only points to the location of the post entities. You won't know which posts to fetch until the collection is fetched.

There are two solutions: once you fetch the collection, in your `render()` method you can pass the collection data to another component, and that component will GET the required data. In our example code above, instead of returning an array of `<li>` items, we could have returned a new custom component that would in turn be connected to SAFE and fetch the entity.

The other solution is to use this hierarchy callback function. It allows you to fetch related objects within the same component. Once the initial object is fetched (e.g. a `toDoCollection` collection), your function will be called for every item in the collection, with the first argument being the value, and second the key. The function should return a new array of SafeObjects (using the `h()` function). Example:

```javascript
// Assume we have an entity called 'toDo'
// and a collection with mappings to these toDo entities.
// The collection object can look like this:
{
	toDoIdNumber1: {
    	userid: 'auserid'
    },
    toDoIdNumber2: {
    	userid: 'anotheruserid'
    },
}

// Entity at location 'toDoIdNumber1' (in the drive of 'auserid')
{
	name: 'clean the dishes'
}

// We can fetch both the collection and entities like this:
function mapPropsToSafe(props) {
  return [
    h(['toDoList', props.userid], 'toDoList', (item, key) => (
      [
        h(['toDo', item.userid, key], 'toDos{}')
      ]
    ))
  ]
}
```

First, the `toDoList` collection owned by the `props.userid` user will be fetched. After it is fetched, the callback will be called for each collection item, with the to-do id as the second argument, and the object (containing the userid) as the first argument. The function will return a new array of SafeObjects that will also be added to the same component. The `{}` indicates not to make each to-do its own prop, but rather combine them all in a single prop called `toDos`. The keys of the objects will be the entity IDs.

For a complete example of hierarchyCallback, please see the [Like component](https://github.com/eblanshey/safe-demo/blob/master/src/components/Like.js) in the demo app.

### To Do / Future Ideas

* ~~**Deletes** -- add a DELETE operation.~~ DONE
* **Nested locations** -- objects are currently stored with their name serving as the location. Allow using nested locations. E.g. allow storing a collection of 'likes' for a particular post at `/users/userid/collections/postLikes/mypostid/likes/1234`.
* **Models** -- allow passing in specialized Models to the "h" function. These models will have built-in functions that automatically validate the data retrieved from SAFE. It is possible for users to modify data on their own drives to have invalid, bogus, or even dangerous data. Validation will ensure that the application will retrieves data it knows how to use. See issue for discussion (coming soon)
* **Versioning** -- also to be added to models. As apps evolve, their data naturally change. Since users own their own data, it is impossible for a site admin to update all data to use new rules. Adding versioning capability will allow the app to easily process outdated data by transforming it to a modern format. See issue for discussion (coming soon)
* **Test coverage** -- add comprehensive unit tests
* **Performance upgrades** -- a lot of calculations are initiated every time an interaction with SAFE is done when using the React helper. Optimize for better performance, such as batching Redux actions together to prevent too many state updates, and thus too many component renders.
* Separate raw API and React helper to their own repositories

### Contribution

Pull requests and issues are welcome!

### License

MIT
