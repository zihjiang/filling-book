# env

flink提交任务时指定的参数, [详情](https://ci.apache.org/projects/flink/flink-docs-release-1.13/zh/docs/deployment/config/)

| name                                   | type | required | default value |
| -------------------------------------- | ---- | -------- | ------------- |
| job.name                               |      | no       | filling       |
| execution.buffer.timeout               |      | no       |               |
| execution.parallelism                  |      | no       | 1             |
| execution.max-parallelism              |      | no       | -1            |
| execution.checkpoint.interval          |      | no       | -1            |
| execution.checkpoint.mode              |      | no       |               |
| execution.checkpoint.timeout           |      | no       |               |
| execution.checkpoint.data-uri          |      | no       |               |
| execution.max-concurrent-checkpoints   |      | no       |               |
| execution.checkpoint.cleanup-mode      |      | no       |               |
| execution.checkpoint.min-pause         |      | no       |               |
| execution.checkpoint.fail-on-error     |      | no       |               |
| execution.restart.strategy             |      | no       |               |
| execution.restart.attempts             |      | no       |               |
| execution.restart.delayBetweenAttempts |      | no       |               |
| execution.restart.failureInterval      |      | no       |               |
| execution.restart.failureRate          |      | no       |               |
| execution.restart.delayInterval        |      | no       |               |
| execution.query.state.max-retention    |      | no       |               |
| execution.query.state.min-retention    |      | no       |               |
| execution.state.backend                |      | no       |               |

