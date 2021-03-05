<p align="left">
<a href="https://join.slack.com/t/redatahq/shared_invite/zt-md9kg05x-Aao1mvx0huTKrDZ1tA8v9w"><img alt="Slack" src="https://img.shields.io/badge/chat-slack-blue.svg"></a>
</p>


# Redata

*Do you know this feeling? -
Something in your data broke, you patiently added monitoring to detect that in the future... only so, that the next time different not expected thing went wrong :)*

Redata is monitoring system for data teams. Automatically computing health checks on all your tables, visualizing them over time, and alerting on them.

# Key features

## Metrics layer

Redata computes health metrics for your data, containing information like this:

* time since last record was added
* number of records added in last (hour/day/week/month)
* schema changes that recently happened
* number of missing values in columns over time
* min/max/avg of values and lenghts of strings in colums
* other user defined metrics

## UI with alerts & tables
Redata UI enables you to view all your tables, their health and alerts of unexpected situations.
You can also adjust checks generated by Redata here.

<img src="./docs/static/redata_ui.png" width="80%"></img>

## Automatic dashboards

Having metrics in one common format makes it possible to create table health dashboards automatically
Here are some examples of how Grafana dashboards look like:

<img src="./docs/static/table_dashboard2.png" width="80%"></img>

## Smart alerts

Redata compares metrics computed in the past to current metrics and alerts if anomalies are found. This means that situations like this:
 * sudden drops or increases in the volume of new records added to your tables
 * longer than expected break between data arrivals
 * significantly different maximal/minimal/avg numbers in any of table columns
 * and more

Would be detected, and you will be alerted. Redata supports Slack (with others tools possible to integerate for you via Grafana) so you can also set up alerts to your favorite support channel.


# Benefits over doing monitoring yourself
What are benefits of using Redata instead of implementing data monitoring yourself? Here is a our list :)

 * **UI showing health of your tables** - See your tables and their health easily
 * **Automatic and up to date health dashboards** - It's normally quite cumbersome to setup proper monitoring for all tables and keeping it up to date is hard - redata can do that for you, detecting new tables and columns and automatically creating dashboards/panels for them.
 
 * **Smart alerts** - Once tables are detected redata automatically tracks their health and looks for anomalies there. Alerts are designed specifically for data quality checks and separete from Grafana alerts (no limits on what to alert on, etc.)
 
 * **Visualizing new, previously impossible things** - Things like schema changes, cannot be queried from DB, redata compares snapshots of your schemas and alert if this change
 
 * **Big set of predefined and effectively computed metrics** - Redata comes with large set of predefined metrics, computed out of box for your tables. We also optimize queries computing them, so that it's effective and fast.

# Getting started (local machine setup)

```
git clone https://github.com/redata-team/redata.git
cd redata

docker-compose up
```

Now visit http://localhost:5000, add your database and starting monitoring your data. Default password/user for Redata/Grafana app is redata :)


# Deploying on production

Redata uses `docker` and `docker-compose` for deployment, this makes it easy to deploy in the cloud, or in your on premise enviroment. 

Look at sample setup instructions for specfic cloud providers:

 - [AWS EC2 deployment](deployment/aws_ec2_awslinux/deployment.md),
 - [AWS Fargate via Pulumi](deployment/pulumi_aws_fargate/README.md),
 - [GCP Compute Engine deployment](deployment/gcp_compute_engine_debian/deployment.md)

# Community

Join [Slack](https://join.slack.com/t/redatahq/shared_invite/zt-md9kg05x-Aao1mvx0huTKrDZ1tA8v9w) for general questions about using redata, problems, and discussions with people making it :)


# Integrations

Here are integrations we support or work on now. Let us know if you'd really like to pritize something or your DB is not included on the list.

<table>
	<thead>
		<tr>
			<th colspan="2">Integration</th>
			<th>Status</th>
		</tr>
	</thead>
	<tbody>
		<tr><td><img height="40" src="https://wiki.postgresql.org/images/3/30/PostgreSQL_logo.3colors.120x120.png" /></td><td style="width: 200px;"><a href="https://www.postgresql.org/">PostgreSQL</a></td><td>Supported</td></tr>
		<tr><td><img height="40" src="https://www.mysql.com/common/logos/powered-by-mysql-167x86.png" /></td><td style="width: 200px;"><a href="https://www.mysql.com/">MySQL</a></td><td>Supported</td></tr>
		<tr><td><img height="40" src="./docs/static/Exasol_clean_navy.png" /></td><td style="width: 200px;"><a href="https://www.exasol.com/">Exasol</a></td><td>Supported</td></tr>
		<tr><td><img height="40" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSVBiUjawSeBBj7T2v64nKYk7SWuLQ3g1vugg&usqp=CAU" /></td><td style="width: 200px;"><a href="https://cloud.google.com/bigquery">BigQuery</a></td><td>Supported</td></tr>
		<tr><td><img height="40" src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/de/AirflowLogo.png/320px-AirflowLogo.png" /></td><td style="width: 200px;"><a href="https://airflow.apache.org/">Apache Airflow</a></td><td>Supported, view all your checks in Airflow </td></tr>
		<tr><td><img height="40" src="https://upload.wikimedia.org/wikipedia/en/thumb/a/a1/Grafana_logo.svg/125px-Grafana_logo.svg.png" /></td><td style="width: 200px;"><a href="https://grafana.com/">Grafana</a></td><td>Supported, view metrics here</td></tr>
		<tr><td><img height="40" src="https://assets.brandfolder.com/pl546j-7le8zk-btwjnu/v/2925183/view@2x.png?v=1610642000" /></td><td style="width: 200px;"><a href="https://slack.com/">Slack</a></td><td>Supported, get alerts on Slack</td></tr>
		<tr><td><img height="40" src="https://www.sqlalchemy.org/img/sqla_logo.png" /></td><td style="width: 200px;">Other SQL DBs</td><td>Experimental support via using SQLAlchemy</td></tr>
		<tr><td><img height="40" src="https://www.blazeclan.com/wp-content/uploads/2013/08/Amazon-Redshift-%E2%80%93-11-Key-Points-to-Remember.png" /></td><td style="width: 200px;">AWS Redshift</td><td>In development</td></tr>
		<tr><td><img height="40" src="https://braze-marketing-assets.s3.amazonaws.com/images/partner_logos/amazon-s3.png" />   </td><td style="width: 200px;">AWS S3</td><td>In development</td></tr>
  		<tr><td><img height="40" src="https://static.wikia.nocookie.net/logopedia/images/7/7f/Microsoft_Office_Excel_%282018%E2%80%93present%29.svg/revision/latest/scale-to-width-down/52?cb=20190927105356" />   </td><td style="width: 200px;">Excel</td><td>Planned</td></tr>
		<tr><td><img height="40" src="https://www.snowflake.com/wp-content/themes/snowflake/img/snowflake-logo-blue@2x.png" /> </td><td style="width: 200px;">Snowflake</td><td>Planned</td></tr>
	</tbody>
</table>


# License
Redata is licensed under the MIT license. See the [LICENSE](LICENSE) file for licensing information.


# Contributing

We love all contributions, bigger and smaller.

Checkout our list of [good first issues](https://github.com/redata-team/redata/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22) and see if you like anything from there. Also feel welcome to join our [Slack](https://join.slack.com/t/redatahq/shared_invite/zt-md9kg05x-Aao1mvx0huTKrDZ1tA8v9w) and suggest ideas, or setup no pressure session with Redata [here](https://calendly.com/mateuszklimek/30min). 

More details on how to tests your changes under: [CONTRIBUTING](https://github.com/redata-team/redata/blob/master/CONTRIBUTING.md)

If you got this far and like what we are building, support us! Star https://github.com/redata-team/redata on Github :)
