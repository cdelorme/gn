
# coding challenge

A summary of the instructions and my interpretation of other requirements:

A single page webapp which connects to an API to retreive data, and displays it on screen with at least one means of user-interaction.

**My conclusion is that this is not a full-stack application request, since there is no need for data storage or centralized processing, this is a purely demonstration of client-side programming.**


## initial ideas

I wanted to do something unique, and had plans to develop a new portfolio site system that used markdown and nodejs to automatically generate new static pages and update from anywhere using a post-receive hook, but I realized that it would not have fulfilled the requirements of this project so I had to think of something different.


## project decision

I chose to build a page that uses javascript to request data from github.

The page will display:

- username entry
- repositories by user
    - ordered by most recent activity
- commits per repository
    - displays list of all contribitors /w username in bold

The user may:

- enter a username
- click a repository (links to github)

This should fulfill all of the requirements:

- communications with github via their REST api to gather data
- displays repositories in a relevant order with commit total
- allows the user to enter a username and open the repository page

_Github provides a stellar API, it's very well documented, and easy to use and make sense of.  This makes it a great choice for a quick application, and was the leading reason for choosing it for this project._


## notes

I've already had some experience using the github api; when I created my [dot-files](https://github.com/cdelorme/dot-files) repo install script I added options to accept the username and password to run curl commands from bash that pull down the users keys as `~/.ssh/authorized_keys` and if the system is running OSX to grab a token for [homebrew](http://brew.sh/), as well as an option to generate a new key and automatically add it to github.

Looking over the API, it appears that a request such as this one:

    https://api.github.com/users/cdelorme/repos

Will yield a JSON blob per project which has the following valuable resources:

- name
- html_url
- updated_at
- contributors_url

I can display the list by `name` field.
I can order them by the `updated_at` field.
I can link to them with the `html_url` field.
Using the `contributor_url` I can display a list of contributions per person.


## operations design

What I will need:

- a form
- an ajax handler
- rendering logic

_For IE8 support I may use `attachEvent` and `ActiveXObject`._

Expected requests:

- request repositories by supplied user
- request contributions for that repository

Operations:

- send request for users
- capture & handle non-existent users (failed operation)
- render list of repositories
- send request for contributions (by repo)
- render contributions list per user, with current user in bold

_I may instead simply ignore failed requests for the time being, or handle them in the same method as rendering._


## conclusions

As I described in detail above, the requirements do not indicate a need for a full stack application, merely a client-side page that can communicate with an API.

It can be run on your local machine, or through any web server.

I also chose the write the code without using jQuery or other external libraries in order to demonstrate that I can do it without dependencies.  If I had chosen to use jQuery the code may have been a bit more reliable in a cross-browser context.

Finally, I have only tested this page in google chrome, but I am confident it will work in most modern browsers.


## possible feature additions

While the webapp is a single-page application, the use of history pushState might allow me to do some pretty cool things.  If I have time I may play with this idea a little bit.  Combined with localStorage it should be possible to do some neat things.

One area to consider is how to handle parallel asynchronous requests.  Whether to limit the number of requests to prevent getting blocked by github, or pull down contributions for every repository all at once and store them in localStorage.


## references

- [github api docs](https://developer.github.com/v3/)
- [github api repositories](https://developer.github.com/v3/repos/)
- [used some css for button decoration](http://www.webdesignerwall.com/demo/css-buttons.html)
- [client-side json cache](https://github.com/cdelorme/lscache)
