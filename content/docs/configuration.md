---
title: Configuration - Finatra
date: "2013-07-01"
---
    <div class="page-header">
     <h1>Flags</h1>
   </div>
   <p class="lead">Finatra uses <a href="http://twitter.github.io/twitter-server/Features.html#flags">Flags</a> for configuration, passed as arguments:</p>
   <pre class="prettyprint">java -jar target/finatra_app.jar -com.twitter.finatra.config.port=&#39;:7070&#39;</pre>

   <p class="lead">Here&#39;s a full list of Flags available: (this is <code>-usage</code> output)</p>
  <pre class="prettyprint">global flags:
  -com.twitter.finatra.config.adminPort=&#39;:9990&#39;: Admin/Stats Port
  -com.twitter.finatra.config.appName=&#39;finatra&#39;: Name of server
  -com.twitter.finatra.config.assetPath=&#39;/public&#39;: path to assets
  -com.twitter.finatra.config.certificatePath=&#39;&#39;: path to SSL certificate
  -com.twitter.finatra.config.docRoot=&#39;src/main/resources&#39;: path to docroot
  -com.twitter.finatra.config.env=&#39;development&#39;: Environment
  -com.twitter.finatra.config.keyPath=&#39;&#39;: path to SSL key
  -com.twitter.finatra.config.logLevel=&#39;INFO&#39;: log level
  -com.twitter.finatra.config.logNode=&#39;finatra&#39;: Logging node
  -com.twitter.finatra.config.logPath=&#39;logs/finatra.log&#39;: path to log
  -com.twitter.finatra.config.maxRequestSize=&#39;5&#39;: maximum request size (in megabytes)
  -com.twitter.finatra.config.pidEnabled=&#39;false&#39;: whether to write pid file
  -com.twitter.finatra.config.pidPath=&#39;finatra.pid&#39;: path to pid file
  -com.twitter.finatra.config.port=&#39;:7070&#39;: Http Port
  -com.twitter.finatra.config.sslPort=&#39;:7443&#39;: Port for SSL
  -com.twitter.finatra.config.templatePath=&#39;/&#39;: path to templates
</pre>

<p class="lead">To turn features off, like the admin server, just pass an empty string instead of a port number:</p>
<pre class="prettyprint">java -jar target/finatra_app.jar -com.twitter.finatra.config.adminPort=''</pre>

<p class="lead">You can define your own flags inside <code><a href="https://github.com/capotej/finatra/blob/master/src/main/scala/com/twitter/finatra/FinatraServer.scala">FinatraServer</a></code>  for any application specific configuration:</p>
<pre class="prettyprint">class MyServer extends FinatraServer {
  val thingFlag = flag(&#34;thingEnabled&#34;, true, &#34;Is the thing enabled&#34;)

  if (thingFlag()) {
    println(&#34;thing is enabled&#34;)
  }
}
</pre>

<p class="lead">Now if we run <code>-usage</code>, we&#39;ll see:</p>

<pre class="prettyprint">com.twitter.finatra_example.App:
  -help=&#39;false&#39;: Show this help
  -thingEnabled=&#39;true&#39;: Is the thing enabled

global flags:
  -com.twitter.finatra.config.adminPort=&#39;:9990&#39;: Admin/Stats Port
  -com.twitter.finatra.config.assetPath=&#39;/public&#39;: path to assets
  -com.twitter.finatra.config.certificatePath=&#39;&#39;: path to SSL certificate
  -com.twitter.finatra.config.docRoot=&#39;src/main/resources&#39;: path to docroot
  -com.twitter.finatra.config.env=&#39;development&#39;: Environment
  -com.twitter.finatra.config.keyPath=&#39;&#39;: path to SSL key
  ...
</pre>

<p class="lead">It&#39;s also possible to set flags via java <a href="http://docs.oracle.com/javase/tutorial/essential/environment/sysprop.html">System Properties</a>:</p>
<pre class="prettyprint">System.setProperty(&#34;com.twitter.finatra.config.pidEnabled&#34;, &#34;false&#34;)
</pre>
