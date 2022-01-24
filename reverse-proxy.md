# NGinx as reverse proxy
If individual servers such as a GIT, blog, WIKI and a CMS-managed web server based on Docker are running on the same or multiple host servers in a closed network, these services can be made externally accessible via a reverse proxy and then all accessed from the outside under port 80 and 443. A separate URL for each individual service then forwards the request to the correct server.

Of course, we will also look at an application example under Docker - but first, the website "mallowz" is to be hosted on one of the Raspberrys - and this is to be accessible from NGinx at http://aurorafox.de/mallowz.
