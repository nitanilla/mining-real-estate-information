It is a site for a Real Estate company with the Admin Panel. There are three types of users with different privileges (super_admin, admin and realtor). There should be possibility to manage users, real estate items and posts.

For the project next client-side and server-side technologies are used:
- Servlets (an authorization filter for Admin Panel);
- JPA (EclipseLink as an implementation);
- EJB (Stateless – the classes that contain methods for CRUD operations. Singleton – the class that registers all logged in users.);
- JSF (PrimeFaces and BootsFaces frameworks);
- i18n – the project completely internationalized (including messages added to the Context from the managed beans);
- Sass (Scout is used for running .scss files);
- AJAX (used intensively via PrimeFaces functionality);
- jQuery (used slightly).

Tools that are used for the project: Eclipse, GlassFish, Git, SLF4J + log4j.
