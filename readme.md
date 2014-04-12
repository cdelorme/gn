
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


## references

- [github api docs](https://developer.github.com/v3/)
- [github api repositories](https://developer.github.com/v3/repos/)
- [used some css for button decoration](http://www.webdesignerwall.com/demo/css-buttons.html)
