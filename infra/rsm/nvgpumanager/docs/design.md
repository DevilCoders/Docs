# Design
Heavily influenced by kubernetes/deviceplugin conception

## Design papers
* [Original design paper](https://wiki.yandex-team.ru/rtcnetdev/GPU-Manager-design/#10.perekljuchenieustrojjstvavfio-pci-nvidia)


## Design assumptions
* **local path ACL security** GRPC service is available only localy via unix socket, no extra ACL required.
* **stateless service** Service does not store device state, service may be restarted at any time.
* **PCI busID as ID** Use PCI Bus ID as primary object ID for reference. This allow us to control all types of resources (nvml-gpu, vfio-pci, vGpu)

## Primary API objects
### PciDeviceSpec
Represent generic pci device specification

### NvGpuDevice
nvidia device which is owned by nvidia kernel driver. such devices can be used by host system, or attached to kernel, NVML inteface is available.
### VFioGpuDevice
nvidia device which is owned by vfio-pci kernel driver.
such devices can be attached to VM
IMPORTANT: device not be used by host system, NVML api is not available.

## Integration
### Integration with nvidia libraries
nvgpu-manager need to known  which  nvidia-kernel-driver tools and CUDA library is installed on host.
For that reason we need meta package which depends on certain nvidia driver version and creates
symlinks in convinient places

* `/opt/nvgpu-manager/nvidia-driver` nvidia kernel driver root for example `/usr/lib/nvidia-418`
* `/opt/nvgpu-manager/cuda` Cuda library root 
    
