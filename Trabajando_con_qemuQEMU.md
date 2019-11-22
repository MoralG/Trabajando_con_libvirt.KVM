# Trabajando con qemu.KVM

## Crear dos máquinas virtuales con un disco en fichero, utilizando aprovisionamiento ligero, utilizando driver virtio en todo lo que se pueda.

* Una conectada a una red NAT (10.10.10.0/24)
* La otra a un bridge externo

Creación del fichero qcow2:
~~~
qemu-img create -f qcow2 Buster.qcow2 10G
~~~

Iniciamos la máquina para instalar Debian Buster
~~~
kvm -m 1024 -hda /home/moralg/MaquinaQemu/Buster.qcow2 \
-cdrom /home/moralg/Documentos/Image/Debian10.iso \
~~~

Ahora vamos a crear una imagen utilizando el aprovisionamiento ligero con la imagen Buster.qcow2
###### Creamos disco2
~~~
qemu-img create -b Buster.qcow2 -f qcow2 Buster1.qcow2
    Formatting 'Buster1.qcow2', fmt=qcow2 size=10737418240 backing_file=Buster.qcow2   cluster_size=65536 lazy_refcounts=off refcount_bits=16
    [2]+  Hecho                   kvm -m 1024 -hda /home/moralg/MaquinaQemu/Buster.qcow2
~~~
###### Creamos disco2
~~~
qemu-img create -b Buster.qcow2 -f qcow2 Buster1.qcow2
    Formatting 'Buster1.qcow2', fmt=qcow2 size=10737418240 backing_file=Buster.qcow2   cluster_size=65536 lazy_refcounts=off refcount_bits=16
    [2]+  Hecho                   kvm -m 1024 -hda /home/moralg/MaquinaQemu/Buster.qcow2
~~~