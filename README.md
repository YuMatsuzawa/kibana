# Fork note

This fork investigate how to serve Kibana as static assets without out-of-the-box Kibana Server introduced in Kibana 4.x.

Current working branch is [4.1.5-static](https://github.com/YuMatsuzawa/kibana/tree/4.1.5-static), which is set to default in this fork. None of other branches are being worked on.

Much of the works are based on [kibana-community/kibana4-static](https://github.com/kibana-community/kibana4-static).

## Background

* Currently working on version **4.1.5** to be compatible with [Amazon ES](http://docs.aws.amazon.com/ja_jp/elasticsearch-service/latest/developerguide/what-is-amazon-elasticsearch-service.html) which is currently version 1.5.2 (2016/04)
    * Cannot use versions below 4.1.3 for this purpose, since there was [a bug](https://github.com/elastic/kibana/issues/3718) which screwed up request URL when target ES is mounted on subdirectory of your domain

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
