# ESLint와 Prettier 의 캐시전략
eslint 에는 `--cache-strategy` 으로 캐시전략을 지정할 수 있다.

```shell
--cache-strategy metadata 
--cache-strategy content
```

* `metadata` : 기본값
* `content` : 파일 내용

일반적으로 metadata 가 더 빠르다. 

### 내가 겪은 문제점
local 에서 컴포넌트의 경로를 수정해서 lint를 돌려서 성공을 확인했다.
그상태에서 PR을 올려 git CI를 돌렸지만, CI lint 단계에서 실패.
결론적으론 수정 전 경로의 컴포넌트에 접근해 import 하고있었던 파일에서 에러가 났던 것.

local에서는 성공했던 lint가 와 CI에서는 터졌을까?

local에서는 내가 수정한 파일을 기준으로만 Lint를 검사한다.
당연히 수정 전 컴포넌트를 접근했던 파일은 현재기준으로 수정하지 않았으므로 캐싱되고 있었고, 
lint scan 대상에 패스된 것.

그러나 git CI상에선 모든 파일의 metadata가 매번 달라지므로, (매번 새로운 파일로 인식하는 것 같다.) lint가 깨진 것이다.

이를 수정하기 위해선 캐시전략중 `content` 로 설정해야 한다.



> **참고자료**
> * https://prettier.io/docs/en/cli.html#--cache-strategy
> * https://github.com/stylelint/stylelint/issues/6170
