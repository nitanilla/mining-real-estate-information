# Easy Trade
### Web application for posting advertisements for selling, buying, renting, and leasing in various areas like real estates, cars, etc.

## Application structure
![Folder structure](https://rawgit.com/KonstantinAdamu/EasyTrade/master/app_structure.jpg)

### Users and roles
The website offers different accessibility options and functionality for admins, users or visitors. Anyone can browse the site and view the home page, login and register screens, various ad details. Visitors can also search by different criteria.

Registered and logged in users have access to their profiles that can be updated or deleted. They can also create new ads, and edit and delete the ones that they have published.

Admin users can create, update or delete other users and also to change their roles.

### Cars and Real Estates
Cars and Real Estates ads have many properties that offer users various filters when searching. 

There are several views, showing details, search options, the paged and sorted results of various searches, etc.
All ads provide detailed and thorough information and photos.

## Routes and functionality
```Javascript
	app.get('/api/all-users', auth.isAuthenticated, controllers.users(app, services.users).getAllUsers);
    app.get('/register', controllers.users(app, services.users).getRegister);
    app.post('/register', controllers.users(app, services.users).postRegister);
    app.get('/login', controllers.users(app, services.users).getLogin);
    app.post('/login', auth.login);
    app.get('/logout', auth.isAuthenticated, auth.logout);
    app.get('/all-users', auth.isAuthenticated, controllers.users(app, services.users).getAllUsers);
    app.get('/profile', controllers.users(app, services.users).getProfile);
    app.post('/profile', auth.isAuthenticated, controllers.users(app, services.users).updateUser);
    app.get('/profile/:username', auth.isAuthenticated, controllers.users(app, services.users).getAllUsers);
    app.post('/profile/:username', auth.isAuthenticated, controllers.users(app, services.users).updateUser);
    app.get('/profile/delete/:id', auth.isAuthenticated, controllers.users(app, services.users).deleteUser);
    app.get('/admin-panel', auth.isAuthenticated, controllers.users(app, services.users).getAdminPanel);

    app.get('/real-estates/search', controllers.realestates(app, services.realestates).getSearch);
    app.get('/real-estates/create', controllers.realestates(app, services.realestates).getCreateForm);
    app.post('/real-estates/create', upload.single('image'), controllers.realestates(app, services.realestates).create);
    app.get('/real-estates', controllers.realestates(app, services.realestates).getSearch);
    app.post('/real-estates/delete/:id', controllers.realestates(app, services.realestates).deleteEstate);
    app.get('/real-estates/:id', controllers.realestates(app, services.realestates).getRealEstate);
    app.get('/real-estates/:id/edit', controllers.realestates(app, services.realestates).getEditView);
    app.post('/real-estates/:id', controllers.realestates(app, services.realestates).edit);

    app.get('/cars', controllers.cars(app, services.cars).getMainView);
    app.get('/cars/create', auth.isAuthenticated, controllers.cars(app, services.cars).getCreate);
    app.post('/cars/create', upload.single('image'), auth.isAuthenticated, controllers.cars(app, services.cars).postCreate);
    app.get('/cars/update/:id', auth.isAuthenticated, controllers.cars(app, services.cars).getUpdate);
    app.post('/cars/update/:id', upload.single('image'), auth.isAuthenticated, controllers.cars(app, services.cars).postUpdate);
    app.get('/cars/all', controllers.cars(app, services.cars).getAllCars);
    app.get('/cars/search', controllers.cars(app, services.cars).getSearch);
    app.get('/cars/delete/:id', controllers.cars(app, services.cars).deleteCar);
    app.get('/cars/details/:id', controllers.cars(app, services.cars).getCar);

    app.get('/', controllers.home(app, services.cars, services.realestates).getLast);

    app.get('*', function (req, res) {
        req.session.error = 'Invalid page!';
        res.redirect('/');
    });
```
There are several controllers that use the data-services for the corresponding type, which communicate with the data-layer that makes the actual requests to the database.
The application provides server-side paging, sorting, and filtering.
There are several levels of validation of data - at the client, in some of the controllers, and in the data-base models.
## Presentation
The site presents the relevant information in an intuitive, easy to use way. The good user experience is enhanced by several tables and a Kendo UI Grid that offer multiple searching, sorting, paging and filtering options.
Every important user action results in a user-friendly success or error notification.