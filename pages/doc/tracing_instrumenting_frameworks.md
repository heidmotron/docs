---
title: Instrumenting Your App for Tracing
keywords: data, distributed tracing, OpenTelemetry
tags: [tracing]
sidebar: doc_sidebar
permalink: tracing_instrumenting_frameworks.html
summary: Set up your application to send metrics, histograms, and trace data to Wavefront.
---

You instrument your application so that trace data from different parts of the stack are sent to Wavefront. Instrumentation enables you to trace a request from end to end across multiple distributed services, guided by key metrics from your application. After instrumentation, you can use our [tracing UI](tracing_basics.html#visualize-distributed-tracing-data-in-wavefront) to visualize a request as a trace that consists of a hierarchy of spans. This visualization helps you pinpoint where the request is spending most of its time and discover problems.

You instrument each microservice in your application with one or more [Wavefront observability SDKs](wavefront_sdks.html). This page:
* Helps you choose the SDK(s) or corresponding integration
* Directs you to the setup steps for each SDK or integration

## Step 1. Prepare to Send Data to Wavefront

Choose one of the following ways to send metrics, histograms, and trace data from your application to the Wavefront service:
* **Direct Ingestion**. To get up and running quickly, use direct ingestion to send data directly to the Wavefront service.
* **Wavefront proxy**. For any production environment, we recommend a Wavefront proxy to forward data from your application to the Wavefront service. [Using a proxy](direct_ingestion.html#proxy-or-direct-ingestion) provides resilience to internet outages, control over data queuing and filtering, and more.

Watch [this video](https://youtu.be/Lrm8UuxrsqA) for some background on proxy vs. direct ingestion.

### To Prepare for Direct Ingestion

1. Identify the URL of your Wavefront instance. This is the URL you connect to when you log in to Wavefront, typically something like `https://mywavefront.wavefront.com`.
2. [Obtain an API token](wavefront_api.html#generating-an-api-token).


### To Prepare for Using a Wavefront Proxy

1. On the host that will run the proxy, [install the proxy](proxies_installing.html#install-a-proxy).
    {{site.data.alerts.note}}
      <ul>
      <li>If you want to use span logs, you need proxy version 5.0 or later.</li>
      <li>If you are using a Sender SDK to send data to Wavefront, you need proxy version 9.0 or later.</li>
      </ul>
    {{site.data.alerts.end}}
2. On the proxy host, open the proxy configuration file `wavefront.conf` for editing. The [path to the file](proxies_configuring.html#paths) depends on the host OS.
3. In the `wavefront.conf` file, uncomment or define an HTTP listener port to send your metrics, histograms, and tracing spans.
    {{site.data.alerts.note}}
      <p>For proxy version before proxy 9.0, in the <code>wavefront.conf</code> file, find and uncomment each listener port you want to enable. The following example enables the default/recommended listener ports for metrics, histogram distributions, and trace data:</p>
          <pre>
pushListenerPorts=2878
...
histogramDistListenerPorts=2878
...
traceListenerPorts=30000
          </pre>
    {{site.data.alerts.end}}
    

4. Consider setting up [trace sampling](trace_data_sampling.html) by [configuring the proxy with a sampling strategy](trace_data_sampling.html#setting-up-explicit-sampling-through-the-proxy).
5. Save the `wavefront.conf` file.
6. [Start the proxy](proxies_installing.html#start-and-stop-a-proxy).


## Step 2. Get Data Flowing into Wavefront

Wavefront provides SDKs that implement the [OpenTracing](https://opentracing.io) specification in many languages. You can use a Wavefront OpenTracing SDK to collect custom trace data that you define for your service, for example, to augment an auto-instrumented framework or to replace a 3rd party OpenTracing-compliant library.

{% include tip.html content="Wavefront can only retrieve up to 1000 spans for a given trace, and you only see up to 1000 spans when you [drill down into spans](tracing_traces_browser.html#drill-down-into-spans-and-view-metrics-and-span-logs) via the Traces Browser. Therefore, as a best practice and for optimal performance, configure your application to have less than 1000 spans in a trace." %}

{{site.data.alerts.note}}
<p>You can use OpenTracing or OpenTelemetry (OpenTracing and OpenCensus have merged to form OpenTelemetry) to send traces to Wavefront. </p>
  <ul>
    <li>
      To learn about the specification that works for you, see <a href="https://help.wavefront.com/hc/en-us/articles/360058140212-OpenTracing-or-OpenTelemetry-Which-specification-to-select-for-instrumenting-applications-for-tracing-">OpenTracing or OpenTelemetry</a>.
    </li>
    <li>
      If your application uses OpenTelemetry, send trace data to Wavefront using the Jaeger or Zipkin integration. See <a href="opentelemetry.html#sending-trace-data-to-wavefront">OpenTelemetry</a>.
    </li>
  </ul>
{{site.data.alerts.end}}

{% include important.html content="Spans that have the `$` character in the application or service name are rejected by Wavefront." %}

### Instrument Your Application with OpenTracing SDKs

Choose the Wavefront OpenTracing SDK for your microservice's programming language, and click the link to go to its `README` file on GitHub:

{% include note.html content="If you can not find the SDK you were looking for, see all the [SDKs provided by Wavefront](wavefront_sdks.html#what-do-you-want-to-collect)." %}

<div class="row">
 <div class="col-md-3 col-sm-6">
     <div class="panel panel-default text-center">
         <div class="panel-body">
            <a href="https://github.com/wavefrontHQ/wavefront-opentracing-sdk-java">
            <img src="/images/icons_svg_java.png" alt="Java logo">
            </a>
         </div>
     </div>
 </div>
 <div class="col-md-3 col-sm-6">
     <div class="panel panel-default text-center">
         <div class="panel-body">
            <a href="https://github.com/wavefrontHQ/wavefront-opentracing-sdk-python">
            <img src="/images/icons_svg_phython.png" alt="Python">
            </a>
         </div>
     </div>
 </div>
 <div class="col-md-3 col-sm-6">
     <div class="panel panel-default text-center">
         <div class="panel-body">
            <a href="https://github.com/wavefrontHQ/wavefront-opentracing-sdk-go">
            <img src="/images/icons_svg_go.png" alt="Go">
            </a>
         </div>
     </div>
 </div>
 <div class="col-md-3 col-sm-6">
        <div class="panel panel-default text-center">
            <div class="panel-body">
               <a href="https://github.com/wavefrontHQ/wavefront-opentracing-sdk-csharp">
               <img src="/images/icons_svg_.net.png" alt="Net">
               </a>
            </div>
        </div>
    </div>
  </div>

### Instrument Your OpenTracing Java Application Without Writing Code

If you need application observability, but don't want to instrument code for your Java microservices, use the [Wavefront Java Tracing Agent](https://github.com/wavefrontHQ/wavefront-opentracing-bundle-java). For more information, see [this blog post on the Wavefront Java Tracing Agent](https://tanzu.vmware.com/content/vmware-tanzu-observability-blog/wavefront-introduces-java-tracing-agent-delivering-out-of-the-box-application-observability).

<div class="row">
   <div class="col-md-3 col-sm-6">
       <div class="panel panel-default text-center">
           <div class="panel-body">
              <a href="https://github.com/wavefrontHQ/wavefront-opentracing-bundle-java">
              <img src="/images/icons_svg_java_tracing_agent.png" alt="Java tracing agent">
              </a>
           </div>
       </div>
   </div>
 </div>

### Send Trace Data to Wavefront via Applications Integrated with Jaeger or Zipkin

If you have already instrumented your application with Jaeger or Zipkin follow these steps:
  1. Collect traces and send them to Wavefront using the following integrations.

      <div class="row">
       <div class="col-md-3 col-sm-6">
           <div class="panel panel-default text-center">
               <div class="panel-body">
                  <a href="jaeger.html">
                  <img src="/images/icons_svg_jaeger.png" alt="Jaeger" class="center">
                  </a>
               </div>
           </div>
       </div>
       <div class="col-md-3 col-sm-6">
           <div class="panel panel-default text-center">
               <div class="panel-body">
                  <a href="zipkin.html">
                  <img src="/images/icons_svg_zipkin.png" alt="Zipkin" class="center">
                  </a>
               </div>
           </div>
       </div>
     </div>


 2. Optionally, add custom tags, applications names, or use an alternative for the Jaeger or Zipkin integration. See [Using Jaeger or Zipkin with Wavefront](tracing_integrations.html) for details.

After your recompiled application starts running, start [exploring your custom trace data on the Traces Browser](tracing_traces_browser.html) and [exploring the RED metrics and histograms that are automatically derived on the Service Dashboard](tracing_service_dashboard.html) from your trace data.

### Instrument Your Application with Wavefront Sender SDKs

For maximum flexibility, you can use the Wavefront Sender SDKs. See [SDKs for Sending Raw Data to Wavefront](wavefront_sdks.html#sdks-for-sending-raw-data-to-wavefront) for background.

<div class="row">
 <div class="col-md-2 col-sm-6">
     <div class="panel panel-default text-center">
         <div class="panel-body">
            <a href="https://github.com/wavefrontHQ/wavefront-sdk-java">
            <img src="/images/icons_svg_java.png" alt="Java logo">
            </a>
         </div>
     </div>
 </div>
 <div class="col-md-2 col-sm-6">
     <div class="panel panel-default text-center">
         <div class="panel-body">
            <a href="https://github.com/wavefrontHQ/wavefront-sdk-python">
            <img src="/images/icons_svg_phython.png" alt="Python">
            </a>
         </div>
     </div>
 </div>
 <div class="col-md-2 col-sm-6">
     <div class="panel panel-default text-center">
         <div class="panel-body">
            <a href="https://github.com/wavefrontHQ/wavefront-sdk-go">
            <img src="/images/icons_svg_go.png" alt="Go">
            </a>
         </div>
     </div>
 </div>
 <div class="col-md-2 col-sm-6">
     <div class="panel panel-default text-center">
         <div class="panel-body">
            <a href="https://github.com/wavefrontHQ/wavefront-sdk-csharp">
            <img src="/images/icons_svg_.net.png" alt="Net">
            </a>
         </div>
     </div>
 </div>
 <div class="col-md-2 col-sm-6">
     <div class="panel panel-default text-center">
         <div class="panel-body">
            <a href="https://github.com/wavefrontHQ/wavefront-sdk-cpp">
            <img src="/images/icons_cplus.png" alt="C++">
            </a>
         </div>
     </div>
 </div>
</div>

When you use a Sender SDK, you won’t see span-level RED metrics by default. This section explains how to send span-level RED metrics using a custom tracing port.

1. [Prepare to send data via the Wavefront proxy](#to-prepare-for-using-a-wavefront-proxy).
    {% include note.html content="You need proxy version 9.0 or later."%}
1. Configure your application to send data via the Wavefront Proxy. See the SDK’s README file for details.
1. Specify the port or a comma-separated list of ports that you want to send the trace data using the `customTracingListenerPorts` configuration in your [`<wavefront_config_path>`](proxies_configuring.html#paths)`/wavefront.conf` file.
  ```xml
  ## port for sending custom spans using the sender sdk
  ## you can use a port that you prefer. in this example port 30001 is used
  customTracingListenerPorts=30001
  ```
1. When you configure the `wavefront sender` on your application as explained in the SDK’s README file, define the port so that span level RED metrics will be gathered from your application.

## Next Steps

Examine traces, spans, and RED metric sent by your application.
* See [Application Status](tracing_ui_overview.html) to get an overview of your applications.
* See [Service Dashboard](tracing_service_dashboard.html) to see the RED metrics of an application.
* See [Traces Browser](tracing_traces_browser.html) to examine the traces of your application.
