# kube-tutorial

Kubernetesの設定ファイルを作ってみる

デプロイメントの定義ファイルを読み込ませる
```bash
kubectl apply -f ./apa000dep.yml
deployment.apps/apa000dep created
```

Podの一覧を取得する
```bash
kubectl get pods
NAME                         READY   STATUS              RESTARTS   AGE
apa000dep-8468f698b8-6tw5r   0/1     ContainerCreating   0          11s
apa000dep-8468f698b8-fl729   0/1     ContainerCreating   0          11s
apa000dep-8468f698b8-h86gp   0/1     ContainerCreating   0          11s
apa000dep-8468f698b8-xrt8k   0/1     ContainerCreating   0          11s
apa000dep-8468f698b8-xz2dc   0/1     ContainerCreating   0          11s
```

サービスの定義ファイルを読み込ませる
```bash
kubectl apply -f ./apa000ser.yml
service/apa000ser created
```

サービスの一覧を取得する
```bash
kubectl get services
NAME         TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
apa000ser    NodePort    10.106.43.126   <none>        8099:30080/TCP   16s
kubernetes   ClusterIP   10.96.0.1       <none>        443/TCP          6d19h
```

Nginxの初期画面が表示される
```bash
curl http://localhost:30080
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

デプロイメントの削除
```bash
kubectl delete -f ./apa000dep.yml
deployment.apps "apa000dep" deleted
```

デプロイメントがなくなっていることを確認
```bash
kubectl get deployment
No resources found in default namespace.
```

サービスを削除する
```bash
kubectl delete -f ./apa000ser.yml
service "apa000ser" deleted
```

サービスがなくなっていることを確認
```bash
kubectl get service
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   6d19h
```
