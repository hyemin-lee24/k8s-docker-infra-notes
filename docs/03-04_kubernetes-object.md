# 3.4 쿠버네티스 오브젝트

### 데몬셋

데몬셋은 디플로이먼트의 `replicas` 값이 노드 수만큼 정해져 있는 형태로 볼 수 있다. 노드 하나당 파드 한 개만 생성된다.

이는 노드의 단일 접속 지점으로, 노드 외부와 통신하기 때문에 파드가 1개 이상 필요하지 않다.

노드를 관리하는 파드라면 데몬셋으로 구성하는 것이 효율적이다.

---

### 컨피그맵

설정을 목적으로 사용하는 오브젝트이다.

---

### PV와 PVC

파드에서 생성한 내용을 기록하고 보관하거나, 모든 파드가 동일한 설정 값을 유지하고 관리하기 위해 공유된 볼륨으로 공통된 설정을 가져올 수 있도록 설계할 필요가 있다.

이러한 목적을 위해 다양한 형태의 볼륨이 제공된다:

- 임시: `emptyDir`
- 로컬: `emptyDir`
- 원격: `persistentVolumeClaim`, `cephfs`, `cinder`, `csi`, `fc(fibre channel)`, `flexVolume`, `flocker`, `glusterfs`, `iscsi`, `nfs`, `portworxVolume`, `quobyte`, `rbd`, `scaleIO`, `storageos`, `vsphereVolume`
- 특수 목적: `downwardAPI`, `configMap`, `secret`, `azureFile`, `projected`
- 클라우드: `awsElasticBlockStore`, `azureDisk`, `gcePersistentDisk`

쿠버네티스는 필요할 때 `PVC`(PersistentVolumeClaim, 지속적으로 사용 가능한 볼륨 요청)를 통해 볼륨을 사용한다.

PVC를 사용하려면, 먼저 `PV`(PersistentVolume, 지속적으로 사용 가능한 볼륨)로 볼륨을 선언해야 한다.

`PV`는 볼륨을 사용할 수 있게 준비하는 단계이며, `PVC`는 준비된 볼륨에서 일정 공간을 할당받는 작업이다.

---

### 스테이트풀셋

파드가 만들어지는 **이름과 순서**를 예측할 필요가 있을 때 사용한다.

스테이트풀셋은 `volumeClaimTemplates` 기능을 사용해 PVC를 자동으로 생성할 수 있고, 각 파드가 순서대로 생성되기 때문에 고정된 이름, 볼륨, 설정 등을 가질 수 있다.

효율성이 좋은 구조는 아니므로, 요구 사항에 맞게 적절히 사용하는 것이 중요하다.