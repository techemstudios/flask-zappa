# flask-zappa - Flask SERVERLESS
Simple Flask Zappa app example. This shall be the base for an
assignment -- providing a simple API implementation from which a
student shall add more functionality.

## Purpose
This repo illustrates a simplified approach for deploying a flask_restful (Python Flask) app on AWS API GW and Lambda. This just deploys the API portion of the api (/spam-api).

## Pre-reqs and Config?
NEED TO DO THE SPECIAL AWS AMI TRICK IF ON CLOUD 9.
Not really, assume you have an AWS account and just do this:
* `cd spam-api`
* `virtualenv spam-api-env`
* `source spam-api-env/bin/activate`
* `pip install flask flask_restful zappa`
* `zappa init`

## Deploy
* `zappa deploy {env}`
