# Namespace, ResourceQuota, LimitRange

<br>

## :question: 사용해야 하는 이유?

`Kubernetes Cluster`에는 전체 사용할 수 있는 자원이 있고, `Cluster`안에는 각각의 `Namespace`가 있다. 그리고 `Namespace` 안에는 `Pod`들이 있다.`Pod`는 필요한 자원을 `Cluster`자원을 공유해서 사용한다. 만약 한 `Pod`가 `Cluster`에 남은 자원을 모두 사용해버리면 다른 `Pod`에 입장에서 쓸 자원이 없고, 자원이 필요할 때 문제가 발생한다.

#### :boom: ResouceQuota

이러한 문제를 해결하기 위해 `ResourceQuota`가 있고, `Namespace`에 설정하면 `Namespace`의 자원 한계를 설정할 수 있다.

#### :boom: LimitRange

한 `Pod`가 자원 사용량을 너무 크게 해버리면 다른 `Pod`들이 해당 `Namespace`에 들어올수 없게 된다. 이 부분을 관리하기 위해서 `LimitRange`를 적용한다. 이렇게 되면 `Namespace`에 들어오는 `Pod`의 크기를 제한할 수 있다. 즉, 한 `Pod` 자원 사용량이 `LimitRange`보다 작아야 `Namespace`에 들어올 수 있다.

#### :sparkles: 다양하게 사용되는 ResouceQuota, LimitRange

`ResourceQuota`와 `LimitRange`는 `Namespace`뿐만 아니라 `Cluster`에도 자원에 대한 제한을 걸 수 있다.

<br>

## :book: Namespace

- 한 `Namespace`에서 같은 타입의 오브젝트(`Pod`, `Service` 등등)들은 중복된 이름을 가질 수 없다.

- `Namespace`의 대표적인 특징은 각각의 `Namespace`들의 자원이 분리가 되기 때문에 관리가 된다.

- `Pod`와 `Service`를 연결하려면 같은 `Namespace` 있어야 한다. `Pod`와 `Service`가 다른 `Namespace`에 있으면 연결되지 않는다.

- `Namespace`를 삭제하면, 안에 있는 자원들도 모두 삭제된다.

<br>

## :book: ResourceQuota

- `Cluster`, `Namespace`의 자원 한계를 설정하는 오브젝트이다.

```
requests.memory : Namespace에 들어갈 Pod들의 전체 Request 자원의 크기를 설정한다.

limits.memory : 메모리 limit를 설정한다.
```

- 한가지 주의할 점, `ResourceQuota`가 정의된 `Namespace`에서 `Pod`를 만들때, 반드시 `requests.memory`, `limits.memory`를 명시해야 한다.

<br>

## :book: LimitRange

- 각각의 `Pod`마다 `Namespace`에 들어올 수 있는지 자원을 체크해준다.

```
min : Pod에서 설정되는 메모리의 값이 min을 넘어야 한다.
max : Pod에서 설정되는 메모리 값이 max를 초과할 수 없다.
maxLimitRequestRatio: request값과 limit값의 비율이 최대 maxLimitRequestRatio를 넘으면 안된다는 뜻이다.
```

```
ex)
min: 1G
max: 4G
maxLimitRequestRatio: 3

pod1
  limits.memory: 5G

pod2
  requests.memory: 4G
  limits.memory: 1G
```

- pod1은 max를 초과하기 때문에 들어올 수 없다.

- pod2는 min, max값을 통과하지만 maxLimitRequestRatio가 3보다 큰 4이기 때문에 들어올 수 없다. (4 / 1 = 4)

<br>

## :bookmark: 참고

- [인프런 - 대세는 쿠버네티스 ^o^](https://www.inflearn.com/course/%EC%BF%A0%EB%B2%84%EB%84%A4%ED%8B%B0%EC%8A%A4-%EA%B8%B0%EC%B4%88)
