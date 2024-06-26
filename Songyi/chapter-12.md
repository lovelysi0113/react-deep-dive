# 12장: 모든 웹 개발자가 관심을 가져야 할 핵심 웹 지표

## 12.1 웹사이트와 성능

- 사용자가 웹서비스에 접속했을 때 기대하는 사항
    1. 웹사이트를 방문한 목적을 손쉽게 달성할 수 있어야 한다
    2. 첫번째 목적을 달성하는 데 걸리는 시간이 짧아야 한다
    3. 웹사이트에서 개인정보가 누출되는 등의 사고 없이 보안이 철저해야 한다
- 웹사이트 개발자라면 자신이 만들고자 하는 프로덕트를 어떤 기술로 어떻게 만들 것이닞에 대해 신경 쓰는 것만큼 웹사이트의 성능에도 주의를 기울여야 한다
- 웹사이트 성능 또한 개발자의 책임이며, 웹사이트의 성능은 조직이 이루고자 하는 목표와 직결된다고 해도 무방하다

## 12.2 핵심 웹 지표란?

- 핵심 웹 지표(Core Web Vital)
    - 웹사이트에서 뛰어난 사용자 경험을 제공하는데 필수적인 지표
- 구글에서 핵심 웹 지표로 꼽는 지표
    - LCP(Largest Contentful Paint): 최대 콘텐츠풀 페인트
    - FID(First Input Delay): 최초 입력 지연
    - CLS(Cumulative Layout Shift): 누적 레이아웃 이동
- 핵심 웹 지표는 사용자가 웹사이트를 이용하는 과정에서 느끼는 불편함을 최소화하고 사용자 경험을 향상시키는 데 중요한 역할을 한다

## 12.3 최대 콘텐츠풀 페인트(LCP)

- 페이지가 처음으로 로드를 시작한 시점부터 뷰포트 내부에서 가장 큰 이미지 또는 텍스트로 렌더링하는 데 걸리는 시간
    - 뷰포트: 사용자에게 현재 노출되는 화면
    - 큰 이미지와 텍스트
        - `<img>`
        - `<svg>` 내부의 `<image>`
        - poster 속성을 사용하는 `<video>`
        - `url()`을 통해 불러온 배경 이미지가 있는 요소
        - 텍스트와 같이 인라인 텍스트 요소를 포함하고 있는 블록 레벨 요소
- 각 엘리먼트가 등장한 시점부터 텍스트 또는 이미지가 완전히 로딩되는 시점
- 시용자 기기가 노출하는 뷰포트 내부에서 가장 큰 영역을 차지하는 요소가 렌더링되는 데 얼마나 걸리는지 측정하는 지표
- 뷰포트에 메인 콘텐츠가 화면에 완전히 전달되는 속도를 기준으로 한다면 사용자는 페이지가 로딩이 완료됐다고 체감하는 시간과 매우 비슷하게 측정할 수 있다
- 기준 점수
    - LCP가 2.5초 이하인 웹사이트는 사용자가 페이지를 빠르게 인식하고 사용할 수 있게 된다
    - LCP가 4초 이상인 웹사이트는 사용자가 페이지를 느리게 인식하고 사용할 수 있게 된다
- 개선 방안
    - LCP 예상 영역에 이미지가 아닌 문자열을 넣는다
    - 이미지를 불러올 때 `<img>` 또는 `<video>`의 poster를 사용한다
    - 이미지를 무손식 형식으로 압축한다
    - `loading = lazy`를 주의한다
    - 최대 콘텐츠풀 리소스는 직접 호스팅한다

## 12.4 최초 입력 지연(FID)

- 웹사이트의 반응성을 측정하는 지표
- 사용자가 얼마나 빠르게 웹페이지와의 상호작용에 대한 응답을 받을 수 있는지 측정하는 지표
- 최초의 입력 하나에 대해서만 그 응답 지연이 얼마나 걸리는지 판단한다
    - 사용자의 입력
        - Response: 사용자의 입력에 대한 반응 속도
        - Animation: 애니메이션의 각 프레임이 렌더링되는 시간
        - Idle: 브라우저가 사용자 입력을 처리하는 시간
        - Load: 콘텐츠를 전달하고 인터렉션을 처리하는 시간
    - FID는 R에 해당하는 응답에 초점을 맞추고 있다
- 화면이 최초에 그려지고 난 뒤, 사용자가 웹페이지에서 클릭 등 상호작용을 수행했을 때 메인 스레드가 이 이벤트에 대한 반응을 할 수 있을 때까지 걸리는 시간
- 최초 이벤트 발생으로부터 해당 이벤트의 핸들러가 실행되는 순간까지 사이의 기간만 측정
- 기준 점수
    - FID가 100밀리초 이하인 웹사이트는 사용자가 페이지와의 상호작용에 대한 응답을 빠르게 받을 수 있다
    - FID가 300밀리초 이상인 웹사이트는 사용자가 페이지와의 상호작용에 대한 응답을 느리게 받을 수 있다
- 개선 방안
    - 실행에 오래 걸리는 긴 작업을 분리한다
        - 긴 작업: 실행을 완료하는 데 오래 걸리는 작업
        - 실행이 오래 걸릴 것 같은 작업 뿐만 아니라 웹페이지 최초 로딩에 필요하지 않은 내용을 나중에 불러오는 작업도 분리하여 처리한다
    - 웹페이지에서 당장 사용하지 않는 코드는 사용자가 필요로 하는 순간에 불러오거나 우선순위를 낮춰서 불러온다
    - 타사 스크립트는 `<script>`의 async나 defer 속성을 사용한다

## 12.5 누적 레이아웃 이동(CLS)

- 페이지의 생명주기 동안 발생하는 모든 예기치 않은 이동에 대한 지표를 계산
- 사용자가 페이지를 이용하는 동안 페이지의 레이아웃이 얼마나 불안정한지 측정하는 지표
    - `useEffect`가 많을수록 클라이언트에서 처리해야 하는 작업이 많아진다
    - 최초 렌더링 이후에 실행되는 `useEffect`가 많을수록, 그리고 이 `useEffect`가 렌더링에 영향을 미칠수록 CLS에서 좋지 않은 점수를 받을 가능성이 높아진다
- 뷰포트 내부의 요소에 대해서만 측정하며, 뷰포트 밖의 요소에 대해서는 측정하지 않는다
    - 사용자 액션으로 인해 발생한 레이아웃 이동은 점수에 포함되지 않는다
- 점수 계산
    - 영향분율: 레이아웃 이동이 발생한 요소의 전체 높이와 뷰포트 높이의 비율
    - 거리분율: 레이아웃 이동이 발생한 요소가 뷰포트 대비 얼마나 이동했는가
    - 영향분율과 거리분율을 곱하여 최종 점수를 계산한다
- 기준 점수
    - CLS가 0.1 이하인 웹사이트는 사용자가 페이지를 불안정하게 인식하지 않는다
    - CLS가 0.25 이상인 웹사이트는 사용자가 페이지를 불안정하게 인식한다
- 개선 방안
    - `useEffect`의 내부에서 요소에 영향을 미치는 작업, 특히 뷰포트 내부에서 노출될 확률이 높은 작업을 최소화한다
    - 폰트 로딩을 최적화한다
    - 적절한 이미지 크기를 설정한다
