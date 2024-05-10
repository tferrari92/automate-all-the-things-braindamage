### We've added this labels so they are recongnized by the Kubernetes plugin 
```yaml
labels:
    backstage.io/kubernetes-id: my-app-frontend
```

### We've accomodated the directory structure to more appropiately fit the new 
my-app helm charts now exists within [/helm-charts/systems/ dir](/helm-charts/systems/) because now we have the possibility of other syetems existing.
So my-app is a sytem whinch includes my-app frontend  and my-app-backend but we could also have your-app system which might include any number of services.