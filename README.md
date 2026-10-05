# Apache Hudi + Spark + Flink Demo

This repository is a Maven multi-module project demonstrating how to use Apache Hudi with both Apache Spark and Apache Flink. It includes sample code for common Hudi operations such as insert, update, delete, overwrite, query, incremental reads, point-in-time reads, and Flink table-based writes.

## Project structure

```text
09-hudi-spark-flink/
├── pom.xml
├── hudi-spark/
│   ├── pom.xml
│   └── src/main/scala/com/itbys/hudi/spark/
│       ├── InsertDemo.scala
│       ├── UpdateDemo.scala
│       ├── DeleteDemo.scala
│       ├── InsertOverwriteDemo.scala
│       ├── QueryDemo.scala
│       ├── IncrementalQueryDemo.scala
│       ├── PointInTimeQueryDemo.scala
│       └── TestKafkaProducer.java
└── hudi-flink/
    ├── pom.xml
    └── src/main/java/com/itbys/hudi/flink/
        └── HudiDemo.java
```

## Modules

### hudi-spark

This module shows Spark-based Hudi examples. It uses:

- Spark 3.2.2
- Scala 2.12
- Hadoop 3.1.3
- Hudi 0.12.0

Example classes:

- `InsertDemo`: writes a new Hudi table using `DataGenerator`
- `UpdateDemo`: updates existing records in a Hudi table
- `DeleteDemo`: deletes records by key
- `InsertOverwriteDemo`: overwrites partitions or table data
- `QueryDemo`: reads a snapshot table through Hudi
- `IncrementalQueryDemo`: reads only new or changed records
- `PointInTimeQueryDemo`: reads table state as of a specific time
- `TestKafkaProducer.java`: simple Kafka producer for testing event ingestion

### hudi-flink

This module shows Flink SQL integration with Hudi using the Hudi connector. It creates a source table from `datagen` and writes to a Hudi table using the `hudi` connector.

- Flink 1.13.6
- Hudi 0.12.0
- Java 8

## Prerequisites

Before running the examples, make sure you have:

- JDK 8+
- Maven 3.6+
- Apache Hadoop / HDFS access
- Apache Spark runtime (for the Spark examples)
- Apache Flink runtime (for the Flink example)

The sample code uses HDFS paths such as `hdfs://hdp:8020/tmp/...`. These values are examples and should be adjusted to match your actual cluster or local environment.

## Build

This project is organized as a Maven parent aggregator and two child modules. The parent POM is not a runnable application by itself, so the usual approach is to build each module directly:

```bash
mvn -f hudi-spark/pom.xml clean package
mvn -f hudi-flink/pom.xml clean package
```

If you prefer to work from the repository root, build the module-specific POM files instead of running the parent aggregator build directly.

## Run examples

### Spark examples

Run a demo class from the `hudi-spark` module in your IDE or with `spark-submit`. These classes are plain Scala applications that build against the Spark/Hudi dependencies declared in the module POM.

If your environment uses a different Spark setup, update the `basePath` and other configuration values in the Scala demo classes before running them.

### Flink example

Run `com.itbys.hudi.flink.HudiDemo` from the `hudi-flink` module in your IDE or with a Flink job submission command. The example writes generated rows to a Hudi table using the Flink SQL connector.

## Important notes

- These demos are intended for learning and experimentation.
- Paths, cluster addresses, and storage settings are environment-specific.
- Hudi table format and connector settings should be validated against your cluster version and deployment mode.
- Some classes assume local HDFS-compatible file paths or a running HDFS service.

## License

This project is provided as a demo and sample code for educational and technical exploration.
