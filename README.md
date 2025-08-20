## Part 2 – Decoupled Architecture for Batch Ingestion  

**Note:** Make sure to check out the [Version 1 repository](https://github.com/hamzabel99/Data_Ingestion_V1) first, as it’s essential to understand the foundation before diving into Version 2.

![Pipeline Architecture](Arcdhitecture%20Ingestion%20V2.png)

In the first version, the architecture was fully functional but tightly coupled: every uploaded file could trigger a Glue job directly.  

In this second version, the architecture is restructured to decouple ingestion from processing. Instead of running a Glue job for each single file (and nobody really wants a Spark job billed just to process one file), files are now collected and processed in batch.  

This design is more cost-efficient, scalable, and aligned with real-world ingestion patterns.  

This batch job is managed through the WorkflowMetadata table: for each prefix, we’ll have a Step Function, along with a batchSize column that we can control to decide how many files are required before the pipeline kicks off.
