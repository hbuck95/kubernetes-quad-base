#Use a base node image

#copy contents into image

#execute command to download dependancies
# execute command to construct node project

# use a new image

# copy through the build directory created in a previous step

# run the command to download dependacies - but append it with -g serve

# create an entrypoint instruction - it will take 3 arguments "serve"(make sure you get the correct location), "-l", and a port number

FROM node:10 as base
COPY . . 
RUN npm install
RUN npm run build
FROM node:10
COPY --from=base /build .
RUN npm install -g serve
ENTRYPOINT ["usr/local/bin/serve", "-l", "3000"]
