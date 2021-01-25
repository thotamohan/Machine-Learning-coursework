# NEW YORK STATE COUNTY COVID 19 TEST DATA BASE SYSTEM

The designed system enables data team to perform analysis on COVID 19 daily test data. Designed workflow runs everyday at 9:00 AM. and the obtained test data run through an ETL
pipeline and is stored in respective County tables in database.

## Data Source:

Incoming data is an API response from API given below.

https://health.data.ny.gov/api/views/xdss-u53e/rows.json?accessType=DOWNLOAD

API request is made everyday at 9:00 AM through AirFlow Scheduled jobs.

## TRANSFORM:

Resultant API response is stored in a dataframe with only selected columns as requested by analyst team. A snapshot of the dataframe is as follows:

Image

But all the columns in the dataframe are stored as strings. It can be seen from below.

Image

Therefore all the columns need to changed to appropriate data types to load them into database tables. A snapshot of the changed data types.

Image

Here the database tables are stored in Postgres Database and the ETL jobs are automated using Apache AirFlow. and Docker is utilized to run the database locally.

Steps to run the application on your database locally:

Pre-requiste:

Make sure you have Docker and Docker compose on the local system.

The project file structure is as below:

Image

## APPLICATION RUNNING STEPS

Now run this command inside the project directory where yml file present

sudo docker-compose -f docker-compose-LocalExecutor.yml up -d

This should create a postgres Container and a Airflow container in your docker environment. A snapshot of the created containers are as follows:

Image

After the containers are created make sure you give the same container Id in the RestAPI call operator code for connecting to PostgreSQL database in Docker.

Then use the following command

docker exec -it 3a3e483a2944 bash

To enter the airflow, use following command

psql -h localhost -U airflow airflow

Now Go to the browser, localhost:8080 or localhost:8081

This should open AirFlow UI as follows, and the steps are given as images

Image






