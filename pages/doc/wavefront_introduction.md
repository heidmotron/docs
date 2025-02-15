---
title: What is Tanzu Observability by Wavefront?
tags: [getting started]
sidebar: doc_sidebar
permalink: wavefront_introduction.html
summary: Learn about the architecture, interfaces, and how to get started.
---
Tanzu Observability by Wavefront is a high-performance streaming analytics platform that supports observability for metrics, counters, histograms, and traces/spans. The product is unique because it scales to very high data ingestion rates and query loads. You can collect data from many services and sources across your entire application stack, and can look at details for earlier data that were ingested earlier.

## Intro Videos

The first <a href="https://bcove.video/2AiJk2v" target="_blank">video<img src="/images/video_camera.png" alt="video camera icon"/></a> is a 90 second overview of **how you can use** explore data and create alerts.

<iframe src="https://bcove.video/2AiJk2v" width="700" height="400" allowfullscreen="true" alt="Wavefront intro how-to"></iframe>

<!---
<p><a href="https://bcove.video/2AiJk2v" target="_blank"><img src="/images/v_intro_howto.png" style="width: 700px;" alt="Wavefront intro how-to"/></a>
</p>
--->

In the second **conceptual** video, Wavefront co-founder Clement Pang explains:
* How to set up the data ingestion pipeline
* How dashboards, charts, and alerts allow you to monitor your environment
* How our histogram and tracing features can give you the full picture of what's going on.

<p><a href="https://youtu.be/90mw6Vcmlt4" target="_blank"><img src="/images/v_intro_clement.png" style="width: 700px;" alt="Wavefront proxies video"/></a>
</p>


## What Can I Do?

After you've sent your data to your Wavefront instance, you can view them in custom dashboards, alert on problem values, and perform anomaly detection and forecasting.

### Charts and Dashboards

<table style="width: 100%;">
<tbody>
<tr>
<td width="50%">Visualize the information in <a href="ui_examine_data.html"> <strong>dashboards and charts</strong></a>.
<ul>
<li>Use filters and functions to see exactly what you’re interested in. For example, combine multiple time series using aggregation functions such as sum() or avg().</li>
<li>Combine functions, and show or hide some of the information - or use dashboard variables to change the focus of a dashboard. For example, a variable might allow you to show the production or development environment.</li>
<li>Select one of several <strong>chart types</strong> (line plot, point plot, table, etc.)</li></ul></td>
<td width="50%"><img src="images/intro_query_v2new.png" alt="simple v2 chart"/></td>
</tr>
</tbody>
</table>

### Alerts

<table style="width: 100%;">
<tbody>
<tr><td width="50%">To detect problems, you can <a href="alerts_manage.html"> <strong>create alerts</strong></a> directly from charts and specify.
<p>For example, assume in your environment you need to know:</p>
<ul>
<li>When the CPU reaches a certain threshold. </li>
<li>Who should be notified and how (email, Pagerduty, etc). </li>
<li>What the alert severity is, and when the alert resolves.</li>
</ul>
After you've set up an alert with that information, we'll send alert notifications that include details and a chart image. See the example on the right. </td>
<td width="50%"><img src="/images/alert_notification_example.png" alt="alert notification example"/></td>
</tr>
</tbody>
</table>

### Queries

<table style="width: 100%;">
<tbody>
<tr><td width="50%">The <a href="label_reference%20page.html"><strong>Wavefront query language (WQL)</strong></a> allows you to extract exactly the information you need. With filters and functions you can customize your charts so the signal becomes visible in the noise. <br>
<br>Initially, many users like the ease-of-use of Chart Builder (shown on the right). Advanced users work with Query Editor.
</td>
<td width="50%"><img src="/images/chart_builder.png" alt="chart builder"/></td>
</tr>
</tbody>
</table>

### Distributed Tracing

<table style="width: 100%;">
<tbody>
<tr><td width="50%">Use <a href="tracing_basics.html"> <strong>Distributed Tracing</strong></a> to work with a service map, examine traces and spans, and drill down into problem areas. </td>
<td width="50%"><img src="/images/tracing_for_intro.png" alt="service map"/>  </td>
</tr>

</tbody>
</table>

## How Do You Integrate With...?

We support [over 200 integrations](label_integrations%20list.html) including cloud providers, DevOps tools, big data, and more.

To interact with the Wavefront service, you can use our rich Graphical User Interface, which includes many pre-built dashboards, charts, and alerts. You can also use SDKs available on our [Github page](https://github.com/wavefrontHQ), the Wavefront REST API, and CLIs.

In addition, tight integrations with Spring Boot, Kubernetes, and Tanzu Mission Control are available.

### Spring Boot

<table style="width: 100%;">
<tbody>
<tr><td width="50%"><strong><a href="wavefront_springboot.html">Wavefront for Spring Boot</a></strong> allows you to quickly configure your environment, so Spring Boot components send metrics, histograms, and traces/spans to the Wavefront service. After you’ve completed setup, you can examine the data in preconfigured or custom-built dashboards and charts.  </td>
<td width="50%"><img src="/images/spring_boot_getting_started.png" alt="spring boot getting started"/>  </td>
</tr>

</tbody>
</table>

### Kubernetes

<table style="width: 100%;">
<tbody>
<tr><td width="50%">Use our one-click install of the <strong><a href="kubernetes.html"> Wavefront Collector for Kubernetes</a></strong> to collect real-time metrics from all layers of a Kubernetes environment (clusters, nodes, pods, containers and the Kubernetes control plane). You can visualize the metrics in a rich set of predefined dashboards. </td>
<td width="50%"><a href="https://youtu.be/jbmUKPSIguQ" target="_blank"><img src="/images/v_kubernetes_lightboard.png" alt="Kubernetes and Wavefront with Clement Pang"/></a> </td>
</tr>
</tbody>
</table>

### Tanzu Mission Control

[VMware Tanzu Mission Control](https://docs.vmware.com/en/VMware-Tanzu-Mission-Control/index.html) is a centralized management platform for consistently operating and securing your Kubernetes infrastructure and modern applications across multiple teams and clouds. You can use Tanzu Mission Control to manage your entire Kubernetes environment, regardless of where your clusters reside.

It's easy to monitor any of the clusters:

<table style="width: 100%;">
<tbody>
<tr><td markdown="span" width="50%">**Step 1**: A user with Administrator privileges enables the integration from Tanzu Mission Control. </td>
<td width="50%"><img src="/images/tmc_integration_enabled.png" alt="Click to enable the Wavefront integration"/> </td>
</tr>
<tr><td markdown="span" width="50%">**Step 2**: Administrators for individual kubernetes clusters add the integration and start exploring the [metrics](tmc.html#kubernetes-source) in [predefined dashboards](tmc.html#dashboards). </td>
<td width="50%"><img src="/images/tmc_add_integration.png" alt="Select add Tanzu Observability by Wavefront. "/> </td>
</tr>
</tbody>
</table>

## How Do I Set Up a Data Ingestion Pipeline?

You can use Tanzu Observability by Wavefront with time-series (metric) data, and also with traces and spans, and with histograms from diverse sources.
* **Cloud:** Perform minimal setup to let the Wavefront service access the data in your cloud environment. The result is direct ingestion of cloud services data such as Amazon Web Services or Google Cloud Platform.
* **Integrations:** For other data sources, we support [over 200 integrations](label_integrations%20list.html). You modify a simple configuration file and you’re good to go.
* **Start Where You Are:** If your environment already has a metrics infrastructure, you can do some pre-processing on the data so they correspond to the Wavefront Data Format, and send them directly to the Wavefront proxy.
* **Direct Ingestion:** For some use cases, [direct ingestion](direct_ingestion.html) is the best approach. Consider the [proxy benefits](proxies.html#proxy-benefits) before you select direct ingestion.
* **Histograms:** For high-velocity metrics, [Wavefront histograms](proxies_histograms.html) might be the best solution.
* **App Monitoring with Distributed Tracing:** For traces, we support Jaeger and Zipkin or any applications that are instrumented with the OpenTracing library. You can also send custom traces using one of our SDKs. Our [Application Map](tracing_ui_overview.html) GUI supports easy exploration of trace data, RED metrics, etc.

### Video: Getting Data Into Wavefront

<p><a href="https://www.youtube.com/watch?v=lhrtPSqn8-c&index=2&list=PLmp0id7yKiEdaWcjNtGikcyqpNcPNbn_K"><img src="/images/v_data_into_wavefront.png" style="width: 700px;" alt="getting data into wavefront"/></a>
</p>

## What Are Supported Interfaces?

Different users interact with the product in different ways:

* Most users access the **graphical user interface** (GUI) from a browser. You log in to your Wavefront instance from a standard web browser, in many cases using an SSO solution.  The UI supports different time windows -- even an entire year.
* The Chart Builder and the Query Editor allow you to fine-tune your charts and alerts. Access function documentation from the UI or start with the [Query Language Reference](query_language_reference.html) and click any function on that page for details and examples.
* The [Wavefront REST API](wavefront_api.html) allows you to perform UI actions programmatically. The API is based on Swagger, so you can generate the client of your choice.
* For **Distributed Tracing**, we make a large sets of SDKs available in Github.

## What's the Architecture?

The Wavefront service runs the metrics collection engine. The service runs in the cloud and accepts data from the Wavefront proxy or through direct ingestion.

* With cloud services, the Wavefront service pulls the data from your cloud provider (after minimal setup). We support all major cloud providers.
* For on-prem telemetry you have several options:
  - Set up a **collector** agent such as Telegraf, collects data from you host or infrastructure and sends those data to the proxy.
  - Send data from your application code to the proxy using a **metrics library**. This works well both for metrics and for traces and spans.
* If you have a custom application, you can send your metrics to the proxy or directly to the service  -- as long as the data is in one of the supported data formats.
  For example, if your environment already includes a metrics collection infrastructure, you can do some pre-processing on the data and send them to the proxy.
* The proxy can also ingest metrics from your log files. See [Log Data Metrics Integration](integrations_log_data.html)


![Wavefront architecture](images/wavefront_architecture_new.png)
