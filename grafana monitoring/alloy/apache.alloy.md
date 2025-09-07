
## apache.alloy config file created
 vi apache.alloy
```
local.file_match "local_files101" {
  path_targets = [{ "__path__" = "/home/ubuntu/access/access.log" }]
  sync_period  = "5s"
}

loki.source.file "local_files101" {
  targets    = local.file_match.local_files101.targets
  tail_from_end = false
  forward_to = [loki.process.add_labels101.receiver]
}

loki.process "add_labels101" {

stage.multiline {
    firstline = "^[0-9]{1,3}\\."  // IP at start of line
  }

  stage.regex {
    expression = "^(?P<client_ip>\\S+) \\S+ \\S+ \\[(?P<time>[^\\]]+)\\] \"(?P<method>[A-Z]+) (?P<path>[^ ]+) (?P<protocol>[^\"]+)\" (?P<status>\\d{3}) (?P<bytes_sent>\\d+                  |-) \"(?P<referrer>[^\"]*)\" \"(?P<user_agent>[^\"]*)\""
  }


// Only promote low-cardinality fields to labels
  stage.labels {
    values = {
      method = "",
      status = "",
       path  = "",
   client_ip = "",
    }
  }

  stage.static_labels {
    values = {
      job         = "apache_101",
       host       = "apache_server101",
      location    = "/home/ubuntu/access",
    }
  }
    forward_to = [loki.write.local_files101.receiver]
}

loki.write "local_files101" {
  endpoint {
    url = "http://54.87.33.189:3100/loki/api/v1/push"
  }
}
