# Copilot instructions for kafka-connect-elasticsearch

## Repository basics
- This is a Java/Maven project for the Kafka Connect Elasticsearch sink connector.
- Main production code is under `src/main/java/io/confluent/connect/elasticsearch`.
- Unit tests are under `src/test/java/io/confluent/connect/elasticsearch`.
- Integration tests are under `src/test/java/io/confluent/connect/elasticsearch/integration`.

## Build and test
- Use Java 8 compatibility when validating changes.
- Preferred full validation command: `mvn clean verify`.
- CI also builds distributables with:
  - `mvn clean install -Pstandalone -DskipTests`
  - `mvn clean install -DskipTests`
- CI test matrix sets `ELASTICSEARCH_VERSION`; if needed locally, set this env var before `mvn clean verify`.

## Change guidance
- Keep changes minimal and focused on the requested task.
- Follow existing style:
  - 2-space indentation
  - explicit imports (no wildcard imports)
- When changing behavior, add or update tests in the matching package (`*Test` for unit tests, `*IT` for integration tests).
- Prefer updating existing classes/tests over introducing new abstractions unless clearly necessary.

## Useful code entry points
- Connector/task lifecycle: `ElasticsearchSinkConnector`, `ElasticsearchSinkTask`
- Client and indexing behavior: `ElasticsearchClient`, `DataConverter`, `Mapping`
- Configuration: `ElasticsearchSinkConnectorConfig`, `ElasticsearchSinkTaskConfig`
- Offset tracking and retries: `OffsetTracker`, `AsyncOffsetTracker`, `SyncOffsetTracker`, `RetryUtil`

## Pull request expectations
- Keep PR titles brief and descriptive (used for changelog generation).
- Include a clear summary of what changed and how it was tested.
- For minor fixes, `MINOR:` in the title is encouraged by project guidelines.
