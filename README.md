# demo_argocd_with_ingress

## argocd - login and change passoword

kubectl port-forward svc/argocd-server -n argocd 8080:443

argocd login localhost:8080
argocd account update-password


---

### init password

- account: admin
- password: 

```
argoPass=$(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)
echo $argoPass
```

### [optional] reset admin password
```
kubectl patch secret argocd-secret -p ' {"data": {"admin.password": null, "admin.passwordMtime": null}}' -n argocd
```
restart the server pod(delete it), and use the new pod name as admin's password.
