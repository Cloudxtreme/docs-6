Architecture and General Overview
==================================

@TODO Change image to reflect HEKA being changed to StatsD
![Jumpscale Architecture](https://cloud.githubusercontent.com/assets/526328/5579704/a8f9aec8-9047-11e4-9a45-e2c756f15d4f.jpg)

## JS Node 
* A machine running jumpscale framework.
* We've different types of JS nodes:
  * **CPU Node:** A machine running a hypervisor
  * **Firewall node:** A machine running a firewall
  * **Application node:** 

## OSIS Server
* An abstract layer that supports different backend databases; mainly, [MongoDB](https://www.mongodb.org) & [InfluxDB](https://www.influxdb.com)
*  [InfluxDB](https://www.influxdb.com) is used to store statistical and log data while [MongoDB](https://www.mongodb.org) is the main database
* All database operations are handled by OSIS and different components can connect to OSIS server using OSIS client.
* More info about [OSIS](../../OSIS/OSIS.md)

## Master StatsD Server
* Every JS Node has a local [StatsD](https://github.com/etsy/statsd) that pushes local stats and logs into the centralized master StatsD.
* Collects logs, aggregates stats and pushes them into [InfluxDB](http://www,influxdb.com)

## Agent controller
* It can interact with [OSIS](../../OSIS/OSIS.md)
* Controls the whole cloud / acts as a Job controller
* It can schedule tasks on a JS Nodes [i.e start a virtual machine on a CPU Node]
* Uses [Redis](http://www.redis.io) database as a task queue system.

## JumpScripts
* Python scripts that are meant to do certain tasks
* executed/updated by JSAgent on a JS node
* Execution of jumpscripts on the same machine or different machine(s) is handled by Agent controller.
* JSAgent can get Jumpscripts updates through webdis on the Agent Controller

## Portal
* A web application to control the cloud, see logs, errors, manage users and execute tasks.
* [Portal](../Portal/Home.md) has a special and powerful wiki syntax to create new pages very quickly.
* Portal supports Markdown as well.

## AtYourService

* Jumpscale comes with its own packaging system that enables you to create/install/update/ [services](../AtYourService/AtYourServiceIntro.md)