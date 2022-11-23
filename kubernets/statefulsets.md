# StatefulSets
***
## O que são?
***
* O StatefulSet funciona de maneira similar a um deployment, mas é voltado para aplicações que devem manter o seu estado, então diferente do Deployment em que os dados serão perdidos quando o pod for deletado, no StatefulSet os dados serão mantidos.
* Dentro do statefulset é possível definir um volume para cada pod, e esse volume será mantido mesmo que o pod seja deletado. Desse modo é necessário utilizar um volume persistente, como o **PersistentVolume** e um **PersistentVolumeClaim**.
* Os pods dentro do Statefulset possuem uma identidade única e mesmo que o pod seja deletado e criado novamente, ele manterá a mesma identidade. 
* EX de um StatefulSet:
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web-statefulset
spec:
    replicas: 1
    template:
      metadata:
        labels:
          app: nginx
        name: nginx
      spec:
        containers:
            - name: nginx
              image: nginx:1.7.9
              ports:
                - containerPort: 80
              envFrom:
                - configMapRef:
                    name: web-configmap
              volumeMounts:
                - name: www
                    mountPath: /usr/share/nginx/html
        volumes:
          - name: www
            persistentVolumeClaim:
              claimName: www-claim
    selector:
      matchLabels:
        app: nginx
    serviceName: nginx