# cka-study-guide
CKA study guide

https://github.com/cncf/curriculum

1.14.1

| Domain                                   | Weight(%) |
|:---------------------------------------- |:---------:|
| [Scheduling][1]                          | 5         |
| [Logging/Monitoring][2]                  | 5         |
| [Application Lifecycle Management][3]    | 8         |
| Cluster Maintenance                      | 11        |
| Security                                 | 12        |
| [Storage][6]                             | 7         |
| [Troubleshooting][7]                     | 10        |
| [Core Concepts][8]                       | 19        |
| Networking                               | 11        |
| Installation, Configuration & Validation | 12        |

# Autocomplete
```
source <(kubectl completion bash)
alias k=kubectl
complete -F __start_kubectl k
```

[1]: scheduling.md
[2]: logging-monitoring.md
[3]: application-lifecycle-management.md
[6]: storage.md
[7]: troubleshooting.md
[8]: core-concepts.md
