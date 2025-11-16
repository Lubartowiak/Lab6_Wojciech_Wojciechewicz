# Lab6_Wojciech_Wojciechewicz

# 1. Utworzenie pliku deployment-nginx.yaml
   ```
   cat > deployment-nginx.yaml <<'EOF'
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-proxy
  labels:
    app: nginx-proxy
spec:
  replicas: 5
  selector:
    matchLabels:
      app: nginx-proxy
  template:
    metadata:
      labels:
        app: nginx-proxy
    spec:
      containers:
      - name: nginx
        image: nginx:1.19
        ports:
        - containerPort: 80
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 2
EOF
```
# 2. Utworzenie Deploymentu
```
kubectl apply -f deployment-nginx.yaml
```
# 3. Sprawdzenie statusu rollout
```
kubectl rollout status deployment/nginx-proxy
```
# 4. Weryfikacja liczby i stanu Podów
```
kubectl get pods -l app=nginx-proxy -o wide
```
