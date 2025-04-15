---
title: "verificar la instalación de kubectl"
description: "Cómo verificar kubectl."
headless: true
_build:
  list: never
  render: never
  publishResources: false
---

Para que kubectl encuentre y acceda a un clúster de Kubernetes, necesita un
[archivo kubeconfig](/docs/concepts/configuration/organize-cluster-access-kubeconfig/), que se crea automáticamente cuando creas un clúster usando
[kube-up.sh](https://github.com/kubernetes/kubernetes/blob/master/cluster/kube-up.sh)
o implementar con éxito un clúster de Minikube.
De forma predeterminada, la configuración de kubectl se encuentra en `~/.kube/config`.

Verifique que kubectl esté configurado correctamente obteniendo el estado del clúster:

```shell
kubectl cluster-info
```
Si ve una respuesta de URL, kubectl está configurado correctamente para acceder a su clúster.

Si ve un mensaje similar al siguiente, kubectl no está configurado correctamente o no puede conectarse a un clúster de Kubernetes.
```
The connection to the server <server-name:port> was refused - did you specify the right host or port?
```

Por ejemplo, si tiene la intención de ejecutar un clúster de Kubernetes en su computadora portátil (localmente), primero necesitará instalar una herramienta como [Minikube](https://minikube.sigs.k8s.io/docs/start/) y luego volver a ejecutar los comandos indicados anteriormente.

Si `kubectl cluster-info` devuelve la respuesta de la URL pero no puede acceder a su clúster, para verificar si está configurado correctamente, use:

```shell
kubectl cluster-info dump
```

### Solución de problemas del error 'No se encontró un proveedor de autenticación' error message {#no-auth-provider-found}

A partir de Kubernetes 1.26, kubectl eliminó la autenticación integrada para los servicios administrados de Kubernetes de ciertos proveedores de nube provedores de nube. Estos proveedores han lanzado complementos específicos para de kubectl. Para obtener instrucciones, revisa la documentación de cada proveedor:

* Azure AKS: [kubelogin plugin](https://azure.github.io/kubelogin/)
* Google Kubernetes Engine: [gke-gcloud-auth-plugin](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl#install_plugin)

(También podrían existir otras razones por las que aparece este mensaje de error, no necesariamente relacionadas con este cambio)



