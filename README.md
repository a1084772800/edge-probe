# edge-probe

External dead-man's probe: checks a public endpoint every ~5 minutes from
GitHub-hosted runners and posts an alert (edge-triggered, hourly re-alert,
recovery notice) via a chat webhook when it becomes unreachable.

The point: the alert path lives entirely **outside** the monitored machine,
so "the machine is down" can never silence its own alarm.

State machine = this workflow's own run history (`failure` streak), no
external storage. Secrets: `FEISHU_APP_ID`, `FEISHU_APP_SECRET`,
`ALERT_CHAT_ID`.

Note: GitHub disables scheduled workflows after 60 days without commits;
the `keepalive` job makes an empty commit monthly to prevent that.
