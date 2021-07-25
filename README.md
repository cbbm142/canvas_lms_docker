# Canvas LMS for LTI testing


This container is a prebuilt version of [Canvas LMS](https://github.com/instructure/canvas-lms).  It should only be used for local development and never in production.  The dockerfiles have been taken from the Canvas repo and altered to make a smaller image for easier portability.

----

## Configuring

Grab the example yaml files from the Canvas repo and put them in their own folder.  Edit the files and update them for the values you want to use for testing.  More information is available in the Docker and production start documentation provided by Instructure.

----

## Creating the compose file

The easiest way to run this is with docker-compose.  A sample compose file is provided that can help you boot strap your own instance.  Update the sample as needed.  Most importantly the volumes have to map from where ever your config files are stored locally to /usr/src/app/config in the container.  You will also have to make sure you build from the root of the repo to make sure the Postgres container is built properly.  You may also want to add in a reverse proxy to handle SSL off load for you since this container will not do that for you.  Once done you can bring the project up with:
`docker-compose up`

----

## Configuring the database

Once both containers are up and running, you can create and setup the database with the following commands.

`docker-compose exec ${canvas service name} bundle exec rake db:create`

`docker-compose exec ${canvas service name} bundle exec rake db:initial_setup`

`docker-compose exec ${canvas service name} bundle exec rake db:migrate`

And then restart the Canvas container so it can reload the now populated DB.  Once it comes back up, you should be able to log into Canvas. 

