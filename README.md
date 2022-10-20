## DataCROP Farro demo deployment
This is a Farro DataCROP version demo deployment instance. It deploys a full-fledged DataCROP infrastructure consisted from 1 stack and 12 containers simulating one edge and one cloud deployment.


### REQUIREMENTS

* [Docker-CE](https://www.docker.com/)

#### Start everything.

Run the following command.

    docker-compose -f farro-demo.yml -p farro-demo up -d

#### Make sure everything has started.

Wait.

Run the following command.

    docker ps --filter name=farro-demo --format "table {{.Image}}\t{{.Names}}"

Make sure you see the following.

    IMAGE                                        NAMES
    faredge/analytics-dashboard:1.0.1            farro-demo_analytics-dashboard_1
    faredge/edge-analytics-engine:1.0.3          farro-demo_edge-analytics-engine_1
    faredge/open-api-for-analytics:1.0.3         farro-demo_open-api-for-analytics_1
    faredge/data-router-and-preprocessor:1.0.3   farro-demo_data-router-and-preprocessor_1
    confluentinc/cp-enterprise-kafka:5.0.0       farro-demo_streams_1
    aksakalli/mqtt-client:latest                 farro-demo_message-echoer_1
    faredge/mqtt-random-data-publisher:1.0.3     farro-demo_random-data-publisher_1
    faredge/model-repository:1.0.3               farro-demo_model-repository_1
    mongo:3.6.4                                  farro-demo_edge-storage_1
    confluentinc/cp-zookeeper:5.0.0              farro-demo_configuration_1
    mongo:3.6.4                                  farro-demo_cloud-storage_1
    eclipse-mosquitto:latest                     farro-demo_messages_1

#### Make sure everything works.

Go to http://localhost:8000.

Select **Overview** from the menu on the left.

Make sure you see the following.

* There is 1 edge gateway.
* There are 2 data kinds.
* There are 2 data interfaces.
* There are 2 data source definitions.
* There is 1 analytics processor definition.
* There are 3 data sources.
* There is 1 analytics instance.

Select **Analytics instances** from the menu on the left.

Make sure the state of the single instance is **Stopped**.

Press the **|>** button.

Make sure the state of the single instance has changed to **Running**.

Select **Data** from the menu on the left.

Select **Bob temperature in JSON over Kafka** from the **Data source** drop-down.

Make sure that you see new values coming in every 10 seconds.

Select **Bob temperature (again) in JSON over Kafka** from the **Data source** drop-down.

Make sure that you see new values coming in every 10 seconds.

#### Stop everything.

Run the following command.

    docker-compose -f farro-demo.yml -p farro-demo down

#### Clean everything up.

Run the following command (**at your own risk**).

    docker system prune --volumes
