FROM ubi9/ubi-minimal

LABEL maintainer="Nick Schuetz <nschuetz@redhat.com>"

WORKDIR /app
RUN chgrp -R 0 /app && \
    chmod -R g=u /app
COPY ["./epicpinball/package.json", "./epicpinball/_site", "./"]
RUN microdnf update -y && microdnf install npm -y && microdnf clean all
RUN npm install && npm audit fix --force && npm cache clean --force 
EXPOSE 8080
ENV npm_config_cache="/app"
CMD [ "npm", "run", "start", "--loglevel=verbose" ]
