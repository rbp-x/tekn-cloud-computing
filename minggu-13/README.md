# Laporan Praktikum Teknologi Cloud Computing - Minggu 13
#### Rahadiyan Bondan Permadi
##### 215411119

## Learn Kubertentes Basics


## Materi
 
# Di lab ini, kita akan bermain-main dengan container orchestration pada Docker. Kita akan menerapkan aplikasi sederhana ke satu host dan mempelajari cara kerjanya. Kemudian, kita mengonfigurasi Docker Swarm, dan belajar menerapkan aplikasi sederhana yang sama di beberapa host. Kemudian kita akan melihat cara menskalakan aplikasi dan memindahkan beban kerja ke berbagai host dengan mudah.

## Tujuan

1.  Mahasiswa mampu menerapkan dan memahami aplikasi sederhana ke satu host dan mempelajari cara kerjanya.
2.  Mahasiswa mampu mengkonfigurasikan Docker Swarm dan menerapkan beberapa aplikasi yang sama dalam beberapa host.
3.  Mahasiswa mampu menskalakan aplikasi dan memindahkan beban kerja ke berbagai host dengan mudah.


## Pembahasan

Langkah - langkah Praktikum

# MODUL 1

    $ minikube version
   
![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%201/1.%20Minikube%20Version%20-%20start.jpg)

    $ minikube start

![2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%201/2.%20kubectl%20version.jpg)

    $ kubectl version
    
![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%201/3.%20kubectl%20cluster-info.jpg)
    
    $ kubectl cluster-info
    
![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%201/4.%20kubectl%20get%20nodes.jpg)
    
    $ kubectl get nodes
    
![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%201/5.%20completing%20module.jpg)

# MODUL 2

   $ kubectl version
   $ kubectl get nodes
   
![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%202/1.%20nodes.jpg)

   $ kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1
   
![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%202/3.%20deploy%20app.jpg)  
   
   $ kubectl get deployments
   
![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%202/4.%20cek%20app%20deployed.jpg)   
   
   $ echo -e "\n\n\n\e[92mStarting Proxy. After starting it will not output a response. Please click the first Terminal Tab\n"; kubectl proxy
   $ curl http://localhost:8001/version

![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%202/5.%20create%20proxy.jpg)   
 
   $ export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}') echo Name of the Pod: $POD_NAME
   $ curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/

![6.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%202/6.%20POD%20Name%20dan%20Akses%20POD%20berjalan.jpg)

# MODUL 3

   $ kubectl get pods
   $ kubectl describe pods
   
![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%203/1.%20cek%20konfigurasi%20aplikasi.jpg)
![2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%203/2.%20cek%20konfigurasi%20aplikasi.jpg)

   $ echo -e "\n\n\n\e[92mStarting Proxy. After starting it will not output a response. Please click the first Terminal Tab\n"; kubectl proxy
   $ export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}') echo Name of the Pod: $POD_NAME
   
![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%203/3.%20panggil%20kembali%20POD%20.jpg)
      
   $ curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/

![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%203/4.%20melihat%20aplikasi%20berjalan.jpg)

   $ kubectl logs $POD_NAME
   
![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%203/5.%20melihat%20log%20kontainer.jpg)

   $ kubectl exec -ti $POD_NAME -- bash
   $ cat server.js
   $ curl localhost:8080
   
![6.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%203/6.%20ekseskuias%20perintah%20didalam%20kontainer.jpg)
![7.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%203/7.%20memulai%20di%20bash%20kontainer.jpg)
 
   $ exit

# MODUL 4

   $ kubectl get pods
   $ kubectl get services
   $ kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080
   
![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%204/1.%20create%20dan%20jalankan%20service.jpg)
   
   $ kubectl get services
   $ kubectl describe services/kubernetes-bootcamp
   
![2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%204/2.%20untuk%20menemukan%20port%20yang%20terbuka.jpg)
   
   $ export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}') echo NODE_PORT=$NODE_PORT
   $ curl $(minikube ip):$NODE_PORT
   
![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%204/3.%20create%20environtment%20%20.jpg)
   
   $ kubectl describe deployment
   
![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%204/4.%20describe%20deployment.jpg)
   
   $ kubectl get pods -l app=kubernetes-bootcamp
   $ kubectl get services -l app=kubernetes-bootcamp
   $ export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}') echo Name of the Pod: $POD_NAME
   $ kubectl label pods $POD_NAME version=v1

![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%204/5.jpg)

   $ kubectl describe pods $POD_NAME

![6.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%204/6.jpg)

   $ kubectl get pods -l version=v1
   
![7.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%204/7.jpg)

![8.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%204/8.jpg)

   
   $ kubectl delete service -l app=kubernetes-bootcamp
   $ kubectl get services
   $ curl $(minikube ip):$NODE_PORT
   
![9.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%204/9.jpg)
   
   $ kubectl exec -ti $POD_NAME -- curl localhost:8080

![10.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%204/10.jpg)

# MODUL 5

   $ kubectl get deployments

![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%205/1.jpg)
   
   $ kubectl get deployments
   $ kubectl scale deployments/kubernetes-bootcamp --replicas=4
   $ kubectl get deployments
   $ kubectl get pods -o wide
   $ kubectl describe deployments/kubernetes-bootcamp
   $ kubectl describe services/kubernetes-bootcamp
   
![2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%205/2.jpg)
   
   $ export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}') echo NODE_PORT=$NODE_PORT
   
![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%205/3.jpg) 

   $ curl $(minikube ip):$NODE_PORT
   $ kubectl scale deployments/kubernetes-bootcamp --replicas=2
   $ kubectl get deployments
   $ kubectl get pods -o wide
   
![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%205/4.jpg)

# MODUL 6

   $ kubectl get deployments
   $ kubectl get pods
   $ kubectl describe pods
   $ kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2
   $ kubectl get pods
   
![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%206/1.jpg)

   
   $ kubectl describe services/kubernetes-bootcamp
   $ export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}') echo NODE_PORT=$NODE_PORT
   $ curl $(minikube ip):$NODE_PORT
   
![2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%206/2.jpg)
   
   $ kubectl rollout status deployments/kubernetes-bootcamp
   $ kubectl describe pods
   
![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%206/3.jpg)

   $ kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=gcr.io/google-samples/kubernetes-bootcamp:v10
   $ kubectl get deployments
   $ kubectl get pods
   
![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%206/4.jpg)
   
   $ kubectl describe pods
   $ kubectl rollout undo deployments/kubernetes-bootcamp
   
![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%206/5.jpg)

   $ kubectl get pods
   $ kubectl describe pods

![6.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%206/6.jpg)

![7.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-13/pict/modul%206/7.jpg)

## Software yang Diperlukan

Linux, Kubernetes

```

