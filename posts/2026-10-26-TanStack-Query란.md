---
title: "TanStack Query란?"
date: 2026-10-26
tags: []
velog_url: https://velog.io/@s26011-cloud/TanStack-Query%EB%9E%80
---

# 개요
TanStack Query는 서버로부터 데이터 가져오기, 데이터 캐싱, 캐시 제어 등 데이터를 쉽고 효율적으로 관리할 수 있는 라이브러리이다.


대표적인 기능은 다음과 같습니다.
- 데이터 가져오기 및 캐싱
- 동일 요청의 중복 제거
- 신선한 데이터 유지
- 무한 스크롤, 페이지네이션 등의 성능 최적화
- 네트워크 재연결, 요청 실패 등의 자동 갱신
---
## 데이터 캐싱
TanStack Query를 활용해 데이터를 가져올 때는 항상 쿼리 키(queryKey)를 지정하기 된다. 이 쿼리 키는 캐시된 데이터와 비교해 새로운 데이터를 가져올지, 캐시된 데이터를 사용할지 결정하는 기준이 된다.
```
import { useQuery } from '@tanstack/react-query'

export default function DelayedData() {
  const { data, isLoading } = useQuery({
    queryKey: ['delay'],                 // 캐시 이름표
    queryFn: async () => (await fetch('https://api.heropy.dev/v0/delay?t=1000')).json(),
    staleTime: 1000 * 10,                // 10초 동안은 캐시 그대로 사용
  })

  if (isLoading) return <div>로딩 중...</div>
  return <div>{JSON.stringify(data)}</div>
}
```
---
## 데이터의 신선도
TanStack Query는 캐시한 데이터를 신선(Fresh)하거나 상한(Stale) 상태로 구분해 관리한다. 캐시된 데이터가 신선하다면 서버에 요청하지 않고 그대로 사용한다. 반면 데이터가 상하면 다시 가져올 수 있는 상태가 되고, 서버에 요청해 새로운 데이터를 가져온다.
```
const { data, isStale } = useQuery({
  queryKey: ['delay'],
  queryFn: async () => (await fetch('https://api.heropy.dev/v0/delay?t=1000')).json(),
  staleTime: 1000 * 10, // 10초 동안은 "신선(fresh)", 지나면 "오래됨(stale)"
})

return <div>{isStale ? '오래된 데이터' : '신선한 데이터'}</div>
```
