## Rails 

**Rails includes two hashes with every request: `params`, `session` and `flash`. What do they do, and what is the difference between them?**

* `params` is a hash containing the parameters sent by a user’s requests. It does not persist across requests unless if the user explicitly sends them again.
* `session` is a hash-like object that allows an application to associate small data items with a user’s session.
* `flash` works like `session`, but its values only persist from the current request to the next.

**For each of the following, indicate whether they belong in `params`, `session`, `flash`, or none, and why:**

* **A token that indicates a user has logged in.** `params` if the site is restful, such as using an API access token. `session` if the site save login information so that all subsequent requests should include the authentication data.
* **A warning that a form submission was rejected.** `flash` because only the subsequent request show the message.
* **A suggestion that the user try a different search term.** `flash` because the suggestion is improving on the previous page’s request.
* **A UI setting to expand all comments.** `params` in order to send the setting to the controller to begin with. `session` because the setting should apply in all subsequent requests. Also acceptable: none, if the site must be RESTful.)


**Redirects: What is an HTTP redirect? How does it work?**
A HTTP redirect is a response from the server to the client indicating that a resource has moved to another URI. Modern browsers follow redirects automatically, so the redirection is transparent to the user.

**How do you trigger a redirect in Rails?**
With `redirect_to` (ActionController::Base). This method can take a Hash or Record that provides the `url_for` method, a String (i.e. 'http://craftacademy.se'), or the symbol `:back` which return the user to the `HTTP_REFERER`.

**When might it be a good idea to redirect?**
After a user submits a form, it may not make sense to return the same submission page. Many applications will instead redirect to a page that lists the result of the submission, such as a newly-created object.

**SlowFood Online Say we want to add an option to the “New Product” page that allows the user to cancel and return to the index page (`/produvts`). What components of application do we need to change?
We need to update the `new` template to include a link back to the index page:
```ruby
= link_to 'Cancel', products_path
```

**HTTP Responses: In Rails, controllers primarily generate two kinds of responses: rendered pages and redirects. What is the difference between rendering and redirecting, and when is it appropriate to use each?**
A rendered page returns an HTML document, and a redirect instructs the browser to make a request to another URI. Redirects are returned when the application wants to send the user to another ‘place’ in the app, usually after a request that has no corresponding response. Rendered pages are returned when the invoked controller knows how to synthesize a HTML page for the request.


**Controllers, Routes, and RESTfulness: Does a route in Rails need to correspond to a CRUD operation?**
No, examples of non-CRUD routes are static pages, user authentication, or operations which don’t operate on resources.

**What is REST?**
REpresentational State Transfer, each URI contains all the information for describing what resource to operate on and what to do with it.

**CRUD: Your friend wants to set up his own blogging application, but doesn’t have a clue how to do it. Help him out by describing each CRUD operation to him in terms of a blog, as well whether it is a `PUT`, `POST`, `GET`, or `DELETE` action.**

(a) `index`: a `GET` operation, this renders a list of the latest entries
(b) `create`: a `POST` operation, creates a new blog entry
(c) `read` (show): a `GET` operation, shows a single entry
(d) `update`: a `PUT` operation, updates a single entry
(e) `destroy`: DELETE operation, deletes an entry


**CRUD in MVC: For (a) and (b) above, specify which actions should occur in the Model, which should occur in the Controller, and which occur in the View if the implementation follows the MVC model.**

(a)
**Model**: return latest n entries to controller
**View**: render the list of entries passed from the controller
**Controller**: query Model to get latest entries and past them as a list to the View

(b)
**Model**: insert new entry into db
**View**: give feedback that the entry was added
**Controller**: take fields from the POST operation and use them to create a new entry. Use Model to insert it into db


**Template Views and Haml: Are you allowed to write code in a View that directly accesses models?**
Yes, you can execute any arbitrary Ruby code in a View. However, having too much logic in the View is discouraged

**What are some reasons to have lightweight views?**
Separation of logic: the controller and model are in charge of taking user input and retrieving the data requested
