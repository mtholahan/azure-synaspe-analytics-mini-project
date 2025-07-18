1. Why should one use Azure Key Vault when working in the Azure environment? What are the alternatives to using Azure Key Vault? What are the pros and cons of using Azure Key Vault?

   

   Azure Key Vault provides centralized secret management for sensitive information like API keys, passwords, and connections strings. It boasts role-based access through Azure AD; it also can rotate keys without editing pipelines. Alternatives include storing secrets in app config files, environment variables, or Azure App Configuration — though these lack centralized security controls.. 

   We have these pros:

   - Secure and compliant
   - Ease of integration with ADF, Synapse, Logic Apps
   - Key rotation

   Some cons:

   - Extra configuration step (need to link Key Vault + grant perms)
   - Slight performance hit
   - Cost

   

2. How do you achieve the loop functionality within an Azure Data Factory pipeline? Why would you need to use this functionality in a data pipeline?

   The **ForEach activity**, a control flow component, enables looping through a collection of items. This control activity enables iterating over objects — for example, loading 50 tables or 10 files with one reusable logic block.

   

3. What are expressions in Azure Data Factory? How are they helpful when designing a data pipeline (please explain with an example)?

   An expression allows us to write dynamic logic. We use a @ syntax to evaluate functions at runtime. Expressions are often used in dynamic filenames, folder paths, and conditional filters.

   ```
   @concat('sales_', formatDateTime(utcnow(), 'yyyyMMdd'), '.csv')
   ```

    resolves to **sales_20250717.csv**

   Expressions allow pipelines to adapt dynamically at runtime — writing logic once that works across varying data scenarios.

   

4. What are the pros and cons of parametrizing a dataset in Azure Data Factory pipeline’s activity?

   ## Pros:

   - Reusability: one dataset supports many variations (e.g., paths, filenames)
   - Cleaner, configurable pipelines
   - Easy integration with metadata-driven frameworks

   ## Cons:

   - More complexity when debugging

   - Harder to preview data in the UI

   - Must carefully manage scope of parameters (linked service vs. dataset vs. pipeline)

     This is especially useful in metadata-driven pipelines where the same dataset structure applies across different files or folders.

   

5. What are the different supported file formats and compression codecs in Azure Data Factory? When will you use a Parquet file over an ORC file? Why would you choose an AVRO file format over a Parquet file format?

ADF supports a wide range of formats for ingestion and output depending on the use case.

## Supported File Formats:

- Delimited Text (CSV/TSV)

- JSON
- Parquet
- Avro
- ORC
- XML

## Supported Compression Codecs:

- gzip

- bz2
- deflate
- zip
- snappy
- lz4
- zstd (some newer scenarios)



## When to Use What?

### Parquet vs. ORC:

- Both are columnar formats, ideal for big data.

- Parquet: preferred in Azure/Synapse ecosystem (broader support).


- ORC: used more in Hive/Hadoop-heavy environments.

### Avro vs. Parquet:

| Feature          | Avro                    | Parquet                   |
| ---------------- | ----------------------- | ------------------------- |
| Format           | Row based               | Columnar                  |
| Best for         | Streaming               | Analysis                  |
| Schema Evolution | Strong                  | Moderate                  |
| Interop          | Great with Kafka, Spark | Better in Synapse, Athena |

Use Avro when you need schema evolution or real-time streaming.
Use Parquet for efficient querying in Synapse, ADF, or Power BI.
