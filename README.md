# k8s-lab
labs for kubernetes

## Deploying Wordpress on ICP

NOTE: HostPath persistence is not suitable for production deployments! HostPath
mounts storage directly from the host machine to be used by a container.

- Follow this [tutorial](https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/)
- Before deploying the `mysql-deployment.yaml` you need to follow these steps
	- Open a terminal and run `mkdir /home/skytap/mysql`
	- Create a `PersistentVolume` in the ICP UI. Go to Platform > Storage
	- Name = mysql-pv, Capacity = 20, Reclaim policy = Recycle, Storage Type = HostPath
	- Go to Parameters tab, Key = `path`, Value = `/home/skytap/mysql`
- Before deploying the `wordpress-deployment.yaml` you need to follow these steps
	- Open a terminal and run `mkdir /home/skytap/wordpress`
	- Create a `PersistentVolume` in the ICP UI. Go to Platform > Storage
	- Name = wordpress-pv, Capacity = 20, Reclaim policy = Recycle, Storage Type = HostPath
	- Go to Parameters tab, Key = `path`, Value = `/home/skytap/wordpress`
	- Change the `apiVersion` for the `Deployment` in `wordpress-deployment.yaml` to `apps/v1beta2`
		this is because we are using a version of Kubernetes < 1.9
- To view the Wordpress UI get the port of the `LoadBalancer` resource that was created:
  - `$ kubectl get services wordpress` and record the port number
	- Open a browser and go to `http://10.0.0.1:port_number`
