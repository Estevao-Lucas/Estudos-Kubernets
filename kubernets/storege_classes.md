# Storage Classes
***
## O que são?
***
* Os storage classes são uma forma de provisionar armazenamento para os pods, da mesma forma que os volumes fazem.
* Com os storage classes é possível **criar volumes (PV) e discos de forma dinamica**, ou seja, sem a necessidade de criar um volume manualmente e conforme a necessidade.
* Cada StorageClass contém os campos **provisioner**, **parameters** e **reclaimPolicy**, que são usados ​​quando um PersistentVolume pertencente à classe precisa ser provisionado dinamicamente.
* O provisioner é o nome do plugin que será usado para provisionar o volume.
* Os parâmetros são passados ​​ao provisioner quando um volume é provisionado.
* O reclaimPolicy é o tipo de política de reivindicação que será usada para o volume provisionado.
* EX: **GCEPersistentDisk** é um provisioner que cria volumes do tipo **GCE PD**.
* Existem 3 tipos de storage classes:
  * **Default**: é o storage class padrão, caso não seja especificado nenhum storage class.
  * **Retained**: é o storage class que não é deletado quando o PV é deletado.
  * **Dynamic**: é o storage class que é provisionado dinamicamente.
* Exemplo de um storage class GCE:
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: slow
provisioner: kubernetes.io/gce-pd
parameters:
  type: pd-standard
  fstype: ext4
  replication-type: none
```
* Ex PVC consumindo um storage class:
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-1
spec:
  accessModes: 
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
  storageClassName: slow
  # O storageClassName é definido nesse campo, então ele faz referencia a um Sc existente.
```