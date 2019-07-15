# Troubleshoot application failure
Check accessibility
```
curl http://web-service-ip:node-port
```
Check service name/status
```
k get svc web-service
k describe svc web-service | grep Endpoints
```
Check service to pod discovery
```
k get svc mysql-service -ojson  | jq -r '.spec.ports'
k get po mysql -ojson | jq -r '.spec.containers[0].ports'
```
```
k describe svc web-service | grep Selector
k get po webapp -ojson | jq -r '.metadata.labels.'
```
Check pod status and number of restarts
```
k get po
```
Check pod events
```
k describe po web
```
Check pod logs
```
k logs web
k logs web -f
k logs web -f --previous
```

# Troubleshoot control plane failure
# Troubleshoot worker node failure
# Troubleshoot networking
