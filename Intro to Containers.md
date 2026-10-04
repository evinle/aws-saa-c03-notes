- Less overhead, less resource usages
- Sits on top of OS
- ![[Pasted image 20261004184811.png]]
- ![[Pasted image 20261004184824.png]]
- Running copy of a Docker Image
- Stack of layers
- Image created using Dockerfile

## Anatomy
- Base image - FROM centos:7
- Images contain readonly layers
	- Changed layered onto the image using diffs
- ![[Pasted image 20261004185229.png]]
- Containers are just Images with a Read/Write layer
	- Sometimes that can be the only difference between them
	- ![[Pasted image 20261004185824.png]]

## Container Registry
![[Pasted image 20261004190016.png]]

## Key Concepts
- Dockerfiles are used to build images
- Portable - self-contained
- Lighweight - parent OS used, fs layers are shared
- Container only runs the application & environment it needs
- As much isolation as VMs
- Ports are exposed to host 
- Application stacks can have multiple containers