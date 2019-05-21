# Node monitoring

## Individual Node Monitoring Service

The Factoid Authority \(TFA\) and De Facto has set up individual node monitoring which can be used by everyone for free:

* A web interface showing current active nodes is available at [http://fct.tools/](http://fct.tools/).
* Factom node monitoring discord bot: [https://git.factoid.org/TFA/TFA-Bot](https://git.factoid.org/TFA/TFA-Bot)
* [Monitoring Factom nodes with Grafana](https://medium.com/p/monitoring-factom-nodes-with-grafana-an-introduction-a6ba7ceeb0e0?source=email-e1da6e70f47a--writer.postDistributed&sk=5f580df6eed020365f9e62253efb42c4)

## Local tools

`Factomd` comes with a few ways to monitor your node's health. The most obvious tool is the control panel found at localhost:8090. Information about the control panel can be found here [Factomd control panel](https://developers.factomprotocol.org/start/factomd-control-panel)

`Factomd` also used to come with more monitoring tools called Prometheus and Grafana. If you want to include them in your package, you can run Grafana and Prometheus docker images:

```text
docker run -d --name=grafana -p 3001:3001 grafana/grafana
docker run -d --name=prometheus -p 9090:9090 prom/prometheus
```

To see Grafana, open http://localhost:3001

### Setting up Grafana <a id="page_Setting-up-Grafana"></a>

1. First ensure you have Grafana open by visiting http://localhost:3001
2. The username is "admin" and password "admin". Be sure not to open this port to the world or anyone can log in!
3. You will be greeted by a page that has a button saying "Add data source". Click that
   * Name: Prometheus
   * Type: Prometheus
   * Ensure Default is checked
   * URL: http://prometheus:9090
4. Once all the fields are put in, click "Save and Test". You should be greeted by "Data source is working".
5. Now we have Prometheus as a datasource, let's get some graphs up. In the top left is the Grafana logo, click it, then dashboard, then import
   * Top Left &gt; Dashboard &gt; Import
6. A preconfigured dashboard can be found here: https://grafana.com/dashboards/4482
   * Input `4482` into the first input, then click Load
   * Make sure to select your prometheus source we added earlier from the dropdown menu next to Prometheus
   * Click import and your dashboard is now viewable.
7. Feel free to mess around and change things to your liking.

