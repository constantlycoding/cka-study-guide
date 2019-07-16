# cka-study-guide
CKA study guide

https://github.com/cncf/curriculum

1.14.1

| Domain                                         | Weight(%) |
|:---------------------------------------------- |:---------:|
| [Scheduling][1]                                | 5         |
| [Logging/Monitoring][2]                        | 5         |
| [Application Lifecycle Management][3]          | 8         |
| [Cluster Maintenance][4]                       | 11        |
| [Security][5]                                  | 12        |
| [Storage][6]                                   | 7         |
| [Troubleshooting][7]                           | 10        |
| [Core Concepts][8]                             | 19        |
| [Networking][9]                                | 11        |
| [Installation, Configuration & Validation][10] | 12        |

# Autocomplete
```
source <(kubectl completion bash)
alias k=kubectl
complete -F __start_kubectl k
```

[1]: scheduling.md
[2]: logging-monitoring.md
[3]: application-lifecycle-management.md
[4]: cluster-maintenance.md
[5]: security.md
[6]: storage.md
[7]: troubleshooting.md
[8]: core-concepts.md
[9]: networking.md
[10]: installation-configuration-validation.md
