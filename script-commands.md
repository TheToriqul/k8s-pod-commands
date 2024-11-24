# Kubernetes Pod Commands Reference Guide

- [Section 1: Pod Creation](#section-1-pod-creation)
- [Section 2: Pod Management](#section-2-pod-management)
- [Section 3: Container Operations](#section-3-container-operations)
- [Section 4: Monitoring](#section-4-monitoring)
- [Section 5: Cleanup](#section-5-cleanup)

> **Author**: Md Toriqul Islam  
> **Description**: Reference guide for Kubernetes pod management commands  
> **Learning Focus**: Pod lifecycle management and container operations  
> **Note**: This is a reference guide. Commands should be understood before execution.

## Section 1: Pod Creation

### Imperative Creation
```bash
# Create a pod with nginx image
kubectl run my-nginx --image=nginx:latest --restart=Never --port=80

# Create pod with specific resource requests
kubectl run my-nginx --image=nginx:latest --requests=cpu=100m,memory=128Mi
```

### Declarative Creation
```bash
# Apply pod configuration from YAML
kubectl apply -f my-pod.yaml

# Create pod and export its configuration
kubectl run my-nginx --image=nginx:latest --dry-run=client -o yaml > pod.yaml
```

## Section 2: Pod Management

### Status Operations
```bash
# Get pod status
kubectl get pod my-nginx

# Get detailed pod information
kubectl describe pod my-nginx

# Get pod logs
kubectl logs my-nginx
```

### Configuration Management
```bash
# Edit pod configuration
kubectl edit pod my-nginx

# Get pod manifest in YAML
kubectl get pod my-nginx -o yaml
```

## Section 3: Container Operations

### Executive Commands
```bash
# Execute shell in pod
kubectl exec -it my-nginx -- /bin/sh

# Run specific command in pod
kubectl exec my-nginx -- nginx -v

# Check nginx configuration
kubectl exec my-nginx -- nginx -t
```

### Port Management
```bash
# Port forward pod
kubectl port-forward my-nginx 8080:80

# Check container ports
kubectl get pod my-nginx -o jsonpath='{.spec.containers[*].ports[*]}'
```

## Section 4: Monitoring

### Resource Monitoring
```bash
# Watch pod status
kubectl get pod my-nginx -w

# Get pod metrics
kubectl top pod my-nginx

# Get pod events
kubectl get events --field-selector involvedObject.name=my-nginx
```

### Health Checks
```bash
# Check pod readiness
kubectl get pod my-nginx -o jsonpath='{.status.conditions[*].status}'

# View pod restart count
kubectl get pod my-nginx -o jsonpath='{.status.containerStatuses[*].restartCount}'
```

## Section 5: Cleanup

### Pod Deletion
```bash
# Delete specific pod
kubectl delete pod my-nginx

# Delete pod using YAML file
kubectl delete -f my-pod.yaml

# Force delete pod
kubectl delete pod my-nginx --grace-period=0 --force
```

## Learning Notes

1. Always verify pod status after creation
2. Use appropriate resource requests
3. Implement proper cleanup practices
4. Maintain security best practices
5. Document configuration changes

---

> 💡 **Best Practice**: Always use resource limits and requests for production pods

> ⚠️ **Warning**: Force deletion should be used as a last resort

> 📝 **Note**: Keep pod configurations version controlled

## Additional Resources

- [Kubernetes Official Documentation](https://kubernetes.io/docs/)
- [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
- [Nginx Documentation](https://nginx.org/en/docs/)