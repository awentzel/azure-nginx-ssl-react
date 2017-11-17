## Azure Web App for Containers running Linux / Nginx / React Configuration
Azure now has Web App for Containers. Essentially, the exact same thing as Web App for Linux or Windows only configured for Containers. 
 
### Project details
Azure Web App for Linux does not yet support running static HTML web sites on Nginx. This solves that problem. Additionally, on Azure it's not necessary to configure SSL/443 or http2 as this is done automatically upstream from the AASL. Note, that if you only want to run https you can set this using the resource manager on Azure as there isn't yet a UI feature available to turn this on. Search the resource file for your Web App instance of "httpsOnly" and set to "true"..

- Running latest Nginx version
- Serving static html sites
- Serving Linux file defaults not Windows
- Configured for SSL through http to https redirection.
- 1 and 30 day caching for core asset file types

### Pre-requisites
Installation, configuration, and understanding of the latest [Docker](https://docs.docker.com/get-started/)

### Build, compile, and run
1. Fetch and clone the source repository.
    ``` 
    $ git clone https://github.com/awentzel/azure-nginx-ssl-react.git
2. Build with Docker
    ``` 
    $ docker build -t azure-nginx .
3. Running as Docker and listening to web traffic. This is useful to determine if there are any configuration or run-time errors.
    ``` 
    $ docker run -p 80:80 azure-nginx
3. Running as Docker with -d parameter to
    ``` 
    $ docker run -p 80:80 -d azure-nginx
4. Browsing the web site. You may want to comment out the redirect statement to test site is loading correctly. Otherwise, you'll be redirected to https and site will not load except on Azure.
    ``` 
    $ curl http://localhost    

### Project changes and recompiling
1. Review running containers on Docker
    ``` 
    $ docker ps
2. Find the unique "CONTAINER ID" from #1 above to use after the stop command.
    ``` 
    $ docker stop 0dce4d4e5f4f 
3. Make edits and return to setp #2 for re-building and running Docker

#### Inspiration
A big thanks for giving inspriration and ideas on best way to organize, build, and run the solution.
- [Prashanth Madi](https://github.com/prashanthmadi/apps/tree/master/azure-nginx)
- [ngineered](https://github.com/ngineered/nginx-static)
- [Kyle Mathews](https://www.bricolage.io/hosting-static-sites-with-docker-and-nginx/)
- [h5bp](https://github.com/h5bp/server-configs-nginx)