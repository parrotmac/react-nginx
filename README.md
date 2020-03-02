# react-nginx
Bare minimum to serve a SPA (such as a React build) with Nginx

# Use

No artifacts are setup, but there's really nothing here. You can build locally with
```
docker build -t react-nginx https://github.com/parrotmac/react-nginx.git
```

To run, mount a directory with an `index.html` into `/usr/share/nginx/html`. If using `create-react-app` tooling, this directory is probably called `build` in your project root. In that case, you might run
```
docker run -it --rm -p 80:80 -v $(pwd)/build:/usr/share/nginx/html react-nginx
```

### Bonus

Here's a slightly absurt oneliner of this whole thing:

```
docker run -it --rm --name react_nginx -p 80:80 -v $(pwd)/build:/usr/share/nginx/html $(echo "FROM nginx:alpine\nRUN echo 'server {server_name _;root /usr/share/nginx/html/;index index.html;location / {try_files \$uri /index.html =404;}}' > /etc/nginx/conf.d/default.conf" | docker build -q -)
```
