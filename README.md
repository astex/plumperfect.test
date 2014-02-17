plumperfect.test
================

A webdev test using flask and sqlalchemy to evaluate new plumperfect candidates.  The application is set up in a fairly typical MVC-ish way.  The views should remain database-agnostic with all queries and processing of input being done at the controller level.  Utility functions can be added as needed in the `lib` folder or in the respective model class if necessary.

The Application
---------------

The application can be understood from the product perspective.  These have a one-to-many relationship with colors and brands.  Colors, in turn, have a many-to-many relationship with users.  These are all [SQLAlchemy](http://www.sqlalchemy.org/) models and the project as a whole uses [Flask-SQLAlchemy](http://pythonhosted.org/Flask-SQLAlchemy/).  A custom base class for the models is defined in `/models/base.py`.

Views use [Flask-Classy](http://pythonhosted.org/Flask-Classy/) to make things a little easier.  They are primarily based off of `RestView` in `/views/base.py`, which provides automatic methods for index, get, post, put, patch, and delete.

Controllers are similarly built.  They are primarily built off of `RestCtrl` in `/controllers/base.py`, which provides automatic methods for index, get, post, put, patch, and delete.  This class also provides a default query and orderby statement to use.

How to Setup and Use
--------------------

Set-up is more or less typical for python web projects.  Requirements can be installed using pip with `pip install -r requirements.txt`.  If you don't know how to set up a virtualenv yet, you should read [this](http://www.virtualenv.org/en/latest/).

The APIs are restful and jsonic.  They can take in either json objects or form-data (for the convenience of not having to set up headers, I usually just use [POSTman](https://chrome.google.com/webstore/detail/postman-rest-client/fdmmgilgnpjigdojojpjoooidkmcomcm?hl=en) with form-data for testing).  The routes are set up to be served at `http://localhost:5001/api/<route>`.  In order to start the server, just install the necessary packages and run `python run.py` (make sure it is set up to use an open port in `config.py` first).

Tasks
-----

While the project is entirely functional, there are some key bits lacking.  Please fork this repo and do one or more of the following on your fork:

- Add authentication.  The post, put, patch, and delete methods should require authentication except for user.post.  Passwords should be hashed using [bcrypt](https://code.google.com/p/py-bcrypt/).
- Add filtering based on `brand_ids`, `product_ids`, `color_ids`, and `user_ids` to the index methods.
- Add views across relationships (e.g `/product/<id>/color` ).
- Add search.
- Add fields at the ColorUser level (e.g `has`, `wants`, `hates`, `once_left_in_a_crowded_bar`, ...) and make them accessable to some APIs.
- Add ProductType model in a many-to-many relationship with Product and associated views and controllers.

I would prefer to see work at the model-, controller-, and view-level, so that I can confirm you have some idea of best-practice in placing your methods.  You can also do anything you like within the code if you think it will better demonstrate what you can do.  Please try to stay stylistically consistent with this repo as this is the general style for the plumperfect.com code.
