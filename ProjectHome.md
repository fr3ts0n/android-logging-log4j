&lt;wiki:gadget url="https://android-logging-log4j.googlecode.com/svn/trunk/adsense-gadget-top.xml" width="728" height="90" /&gt;

# Logging with Log4J in Android #

<a href='http://mindpipe.blogspot.com/2011/11/android-log4j-exception-properties.html'>Why logging with log4j in Android is problematic</a>



# Features #

<p>Provides</p>

  * logging in Android using [log4j](http://logging.apache.org/log4j/)
  * support for logging with [slf4j](http://www.slf4j.org/) in Android using log4j
  * a **LogCatAppender** for log4j, which logs to [LogCat](http://developer.android.com/guide/developing/tools/logcat.html)
  * a log4j **configuration facade** class for convenient Log4J configuration
  * no modified _log4j.jar_ is needed

## Maven support ##

<p>For users using <a href='http://code.google.com/p/maven-android-plugin/'>Maven for Android</a></p>

```
<dependency>
  <groupId>de.mindpipe.android</groupId>
  <artifactId>android-logging-log4j</artifactId>
  <version>1.0.3</version>
</dependency>
```

&lt;wiki:gadget url="https://android-logging-log4j.googlecode.com/svn/trunk/adsense-gadget-middle.xml" width="728" height="90" /&gt;

# Quickstart example using log4j in Android #

## Log4J configuration ##

```
import java.io.File;
import org.apache.log4j.Level;
import android.os.Environment;
import de.mindpipe.android.logging.log4j.LogConfigurator;
/**
 * Call {@link #configure()}} from your application's activity.
 */
public class ConfigureLog4J {
    public static void configure() {
        final LogConfigurator logConfigurator = new LogConfigurator();
		
        logConfigurator.setFileName(Environment.getExternalStorageDirectory() + File.separator + "myapp.log");
        logConfigurator.setRootLevel(Level.DEBUG);
        // Set log level of a specific logger
        logConfigurator.setLevel("org.apache", Level.ERROR);
        logConfigurator.configure();
    }
}
```

<p>Above code configures the log4j system with some default settings e.g.<br>
<br>
<ul><li>file appender and LogCat appender<br>
</li><li>rotating logs and corresponding backup files and file sizes<br>
</li><li>default log output pattern</li></ul>

See <a href='http://android-logging-log4j.googlecode.com/svn/trunk/src/main/java/de/mindpipe/android/logging/log4j/LogConfigurator.java'>LogConfigurator</a> for concrete default values and what else can be configured.<br>
</p>

<p>See full <a href='http://android-logging-log4j.googlecode.com/svn/trunk/src/test/java/de/mindpipe/android/logging/log4j/example/ExampleLog4J.java'>log4j example</a>.</p>

<p><b>NOTE:</b> In order to log to a file on the external storage, the following permission needs to be placed in <i>AndroidManifest.xml</i>.<p>

<pre><code>&lt;uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /&gt;<br>
</code></pre>

<h2>Using log4j directly</h2>
<p>Using log4j directly causes smaller application sizes than using it through an abstraction layer e.g. with slf4j. In case of not using slf4j, you can save potentially about 36Kb.</p>

<h3>Prerequisites</h3>
<p>Add the following libraries to the classpath.</p>

<ul><li><i>android-logging-log4j.jar</i>
</li><li><i>log4j.jar</i> (version 1.2.x)</li></ul>

<pre><code>import org.apache.log4j.Logger;<br>
<br>
public class ExampleLog4J {<br>
    private final Logger log = Logger.getLogger(ExampleLog4J.class);<br>
<br>
    public void myMethod() {<br>
        log.info("This message should be seen in log file and logcat");<br>
    }<br>
}<br>
</code></pre>




<h2>Using log4j over slf4j</h2>
<ul><li>in general logging in java should be implemented by using a logging abstraction API such as <a href='http://www.slf4j.org'>slf4j</a>
<ul><li>a log4j implementation using slf4j is available<br>
</li><li>see the <a href='http://slf4j.org/manual.html'>slf4j documentation</a> for details<br>
</li><li>use <i>android-logging-log4j</i> to configure your log4j system and/or use the LogCatAppender for convenient logging in your development environment</li></ul></li></ul>


<h3>Prerequisites</h3>
<p>Add the following libraries to the classpath.</p>

<ul><li><i>android-logging-log4j.jar</i>
</li><li><i>log4j.jar</i> (version 1.2.x)<br>
</li><li><i>slf4j-api.jar</i>
</li><li><i>slf4j-log4j12.jar</i></li></ul>

<pre><code>import org.slf4j.Logger;<br>
import org.slf4j.LoggerFactory;<br>
<br>
public class ExampleLog4JOverSLF4J {<br>
    private final Logger log = LoggerFactory.getLogger(ExampleLog4JOverSLF4J.class);<br>
	<br>
    public void myMethod() {<br>
        log.info("This message should be seen in log file and logcat");<br>
    }<br>
}<br>
<br>
</code></pre>

<p>See full <a href='http://android-logging-log4j.googlecode.com/svn/trunk/src/test/java/de/mindpipe/android/logging/log4j/example/ExampleLog4JOverSLF4J.java'>log4j over slf4j example</a></p>


<h1>Motivation</h1>
<ul><li>log4j.properties does not work on Android<br>
</li><li>log4j.xml does not work on Android (at least for me)<br>
</li><li>log4j provides good features e.g. rotating log files and appenders<br>
</li><li>no log appender for log4j available to log to LogCat</li></ul>


<wiki:gadget url="https://android-logging-log4j.googlecode.com/svn/trunk/adsense-gadget-bottom.xml" width="728" height="90" />