# Apache Spark

Lightning-Fast Cluster Computing - <http://spark.incubator.apache.org/>


## Online Documentation

You can find the latest Spark documentation, including a programming
guide, on the project webpage at <http://spark.incubator.apache.org/documentation.html>.
This README file only contains basic setup instructions.


## Building

Spark requires Scala 2.10. The project is built using Simple Build Tool (SBT),
which can be obtained from [here](http://www.scala-sbt.org). To build Spark and its example programs, run:

    sbt assembly

Once you've built Spark, the easiest way to start using it is the shell:

    ./spark-shell

Or, for the Python API, the Python shell (`./pyspark`).

Spark also comes with several sample programs in the `examples` directory.
To run one of them, use `./run-example <class> <params>`. For example:

    ./run-example org.apache.spark.examples.SparkLR local[2]

will run the Logistic Regression example locally on 2 CPUs.

Each of the example programs prints usage help if no params are given.

All of the Spark samples take a `<master>` parameter that is the cluster URL
to connect to. This can be a mesos:// or spark:// URL, or "local" to run
locally with one thread, or "local[N]" to run locally with N threads.

## Running tests

### With sbt (Much faster to run compared to maven)
Once you have built spark with `sbt assembly` mentioned in [Building](#Building) section. Test suits can be run as follows using sbt.

`sbt test`
 
### With maven.
1. Export these necessary environment variables as follows.

 `export SCALA_HOME=<scala distribution>`

 `export MAVEN_OPTS="-Xmx1512m -XX:MaxPermSize=512m"`

2. Build assembly by
`mvn package -DskipTests`

3. Run tests
`mvn test`

## A Note About Hadoop Versions

Spark uses the Hadoop core library to talk to HDFS and other Hadoop-supported
storage systems. Because the protocols have changed in different versions of
Hadoop, you must build Spark against the same version that your cluster runs.
You can change the version by setting the `SPARK_HADOOP_VERSION` environment
when building Spark.

For Apache Hadoop versions 1.x, Cloudera CDH MRv1, and other Hadoop
versions without YARN, use:

    # Apache Hadoop 1.2.1
    $ SPARK_HADOOP_VERSION=1.2.1 sbt assembly

    # Cloudera CDH 4.2.0 with MapReduce v1
    $ SPARK_HADOOP_VERSION=2.0.0-mr1-cdh4.2.0 sbt assembly

For Apache Hadoop 2.2.X, 2.1.X, 2.0.X, 0.23.x, Cloudera CDH MRv2, and other Hadoop versions
with YARN, also set `SPARK_YARN=true`:

    # Apache Hadoop 2.0.5-alpha
    $ SPARK_HADOOP_VERSION=2.0.5-alpha SPARK_YARN=true sbt assembly

    # Cloudera CDH 4.2.0 with MapReduce v2
    $ SPARK_HADOOP_VERSION=2.0.0-cdh4.2.0 SPARK_YARN=true sbt assembly

    # Apache Hadoop 2.2.X and newer
    $ SPARK_HADOOP_VERSION=2.2.0 SPARK_YARN=true sbt assembly

When developing a Spark application, specify the Hadoop version by adding the
"hadoop-client" artifact to your project's dependencies. For example, if you're
using Hadoop 1.2.1 and build your application using SBT, add this entry to
`libraryDependencies`:

    "org.apache.hadoop" % "hadoop-client" % "1.2.1"

If your project is built with Maven, add this to your POM file's `<dependencies>` section:

    <dependency>
      <groupId>org.apache.hadoop</groupId>
      <artifactId>hadoop-client</artifactId>
      <version>1.2.1</version>
    </dependency>


## Configuration

Please refer to the [Configuration guide](http://spark.incubator.apache.org/docs/latest/configuration.html)
in the online documentation for an overview on how to configure Spark.


## Apache Incubator Notice

Apache Spark is an effort undergoing incubation at The Apache Software
Foundation (ASF), sponsored by the Apache Incubator. Incubation is required of
all newly accepted projects until a further review indicates that the
infrastructure, communications, and decision making process have stabilized in
a manner consistent with other successful ASF projects. While incubation status
is not necessarily a reflection of the completeness or stability of the code,
it does indicate that the project has yet to be fully endorsed by the ASF.


## Contributing to Spark

Contributions via GitHub pull requests are gladly accepted from their original
author. Along with any pull requests, please state that the contribution is
your original work and that you license the work to the project under the
project's open source license. Whether or not you state this explicitly, by
submitting any copyrighted material via pull request, email, or other means
you agree to license the material under the project's open source license and
warrant that you have the legal authority to do so.

