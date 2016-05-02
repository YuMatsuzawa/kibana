# Fork note

This fork investigate how to serve Kibana 4.1.5 as static assets without out-of-the-box Kibana Server introduced in Kibana 4.x.

Working branch is [4.1.5-static](https://github.com/YuMatsuzawa/kibana/tree/4.1.5-static), which is set to default in this fork. None of the master and other fork-time branches are being worked on.

Much of the works are based on [kibana-comunity/kibana4-static](https://github.com/kibana-community/kibana4-static).

## Background

* Using version 4.1.5 so as to be compatible with [Amazon ES](http://docs.aws.amazon.com/ja_jp/elasticsearch-service/latest/developerguide/what-is-amazon-elasticsearch-service.html) which is currently version 1.5.2 (2016/04)
* Cannot use versions below 4.1.3, since there was [a bug](https://github.com/elastic/kibana/issues/3718) which screwed up request URL when target ES is mount on subdirectory of your domain

## How to build

* Prepare required version of Node (according to `package.json`, version must be within `~0.10 || ~0.12`)
* `$ npm install`
* `$ bower install`
* `$ grunt build`
* Deliverables are placed in `build/dist/kibana/`

## How to serve

* Static assets are found in `build/dist/kibana/src/public/`, copy and serve them from whatever web server you like
* There must be `/config` endpoint, which should respond with required config information as JSON. Simply editing `config` file in this branch should suffice, but you might want to create your own controller to dynamically produce config, which is also OK
    * Replace `elasticsearch` field in the config with your ES endpoint. This will be the endpoint where static Kibana request to
* If your static Kibana is served from `http://<your host>/whatever_path/kibana/` path, then your config endpoint must be `http://<your host>/whatever_path/kibana/config`, since Kibana will search their config based on its current path

# Kibana 4.1.5

[![Build Status](https://travis-ci.org/elastic/kibana.svg?branch=master)](https://travis-ci.org/elastic/kibana?branch=master)

Kibana is an open source ([Apache Licensed](https://github.com/elastic/kibana/blob/master/LICENSE.md)), browser based analytics and search dashboard for Elasticsearch. Kibana is a snap to setup and start using. Kibana strives to be easy to get started with, while also being flexible and powerful, just like Elasticsearch.

## Requirements

- Elasticsearch version 1.4.4 or later
- Kibana binary package

## Installation

* Download: [http://www.elastic.co/downloads/kibana](http://www.elastic.co/downloads/kibana)
* Run `bin/kibana` on unix, or `bin\kibana.bat` on Windows.
* Visit [http://localhost:5601](http://localhost:5601)

## Quick Start

You're up and running! Fantastic! Kibana is now running on port 5601, so point your browser at http://YOURDOMAIN.com:5601.

The first screen you arrive at will ask you to configure an **index pattern**. An index pattern describes to Kibana how to access your data. We make the guess that you're working with log data, and we hope (because it's awesome) that you're working with Logstash. By default, we fill in `logstash-*` as your index pattern, thus the only thing you need to do is select which field contains the timestamp you'd like to use. Kibana reads your Elasticsearch mapping to find your time fields - select one from the list and hit *Create*.

**Tip:** there's an optimization in the way of the *Use event times to create index names* option. Since Logstash creates an index every day, Kibana uses that fact to only search indices that could possibly contain data in your selected time range.

Congratulations, you have an index pattern! You should now be looking at a paginated list of the fields in your index or indices, as well as some informative data about them. Kibana has automatically set this new index pattern as your default index pattern. If you'd like to know more about index patterns, pop into to the [Settings](#settings) section of the documentation.

**Did you know:** Both *indices* and *indexes* are acceptable plural forms of the word *index*. Knowledge is power.

Now that you've configured an index pattern, you're ready to hop over to the [Discover](#discover) screen and try out a few searches. Click on **Discover** in the navigation bar at the top of the screen.

## Documentation

Visit [Elastic.co](http://www.elastic.co/guide/en/kibana/current/index.html) for the full Kibana documentation.

## Snapshot Builds

For the daring, snapshot builds are available. These builds are created after each commit to the master branch, and therefore are not something you should run in production.

| platform |  |  |
| --- | --- | --- |
| OSX | [tar](http://download.elastic.co/kibana/kibana/kibana-4.1.5-darwin-x64.tar.gz) | [zip](http://download.elastic.co/kibana/kibana/kibana-4.1.5-darwin-x64.zip) |
| Linux x64 | [tar](http://download.elastic.co/kibana/kibana/kibana-4.1.5-linux-x64.tar.gz) | [zip](http://download.elastic.co/kibana/kibana/kibana-4.1.5-linux-x64.zip) |
| Linux x86 | [tar](http://download.elastic.co/kibana/kibana/kibana-4.1.5-linux-x86.tar.gz) | [zip](http://download.elastic.co/kibana/kibana/kibana-4.1.5-linux-x86.zip) |
| Windows | [tar](http://download.elastic.co/kibana/kibana/kibana-4.1.5-windows.tar.gz) | [zip](http://download.elastic.co/kibana/kibana/kibana-4.1.5-windows.zip) |
