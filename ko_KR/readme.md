___
**역자주**

이 문서는 [readme.md](https://github.com/Unity-Billal-mesloub/ava/blob/main/readme.md)의 한국어 번역입니다. [이곳](https://github.com/avajs/ava/compare/71404c23302d825095659c70cb9a1b08251697ad...main#diff-0730bb7c2e8f9ea2438b52e419dd86c9)에서 AVA의 master 브랜치와 이 문서의 차이를 확인할 수 있습니다. (만약 차이가 없다면 문서가 최신 버전임을 의미합니다)
___

[![AVA](https://github.com/Unity-Billal-mesloub/ava/raw/main/media/header.png)](https://avajs.dev)

AVA는 Node.js를 위한 테스트 러너로, 간결한 API, 상세한 에러 출력, 새로운 언어 기능 수용 및 프로세스 분리를 통해 확신을 갖고 개발할 수 있도록 해 줍니다 🚀.

[AVA Twitter 계정](https://twitter.com/ava__js)을 팔로우하여 새 소식을 받아보세요.

만약 AVA에 컨트리뷰트 (Issue, PR 등) 하고 싶다면, 우리의 [기여 가이드](.github/CONTRIBUTING.md)를 읽어보세요.

![](media/verbose-reporter.png)

## 왜 AVA인가요?

- 작고 빠른 속도
- 간단한 test 구문
- Test들을 동시에 (concurrently) 수행
- 원자적인 테스트 (atomic test) 들을 쓰도록 유도
- 암시적인 전역 변수를 사용하지 않음
- 타입스크립트 정의를 포함
- [Magic assert](#magic-assert)
- [각 테스트 파일 별 고립된 환경을 제공](./docs/01-writing-tests.md#process-isolation)
- [Promise 지원](./docs/01-writing-tests.md#Promise-지원)
- [Async 함수 지원](./docs/01-writing-tests.md#async-함수-지원)
- [Observable 지원](./docs/01-writing-tests.md#observable-지원)
- [향상된 단언문 메세지](./docs/03-assertions.md#enhanced-assertion-messages)
- [CI에서 테스트 자동 병렬화](#ci에서의-병렬-실행)
- [TAP reporter 지원](./docs/05-command-line.md#tap-reporter)

## 사용법

다음 명령어를 입력해 AVA를 설치하고 설정하세요:

```console
npm init ava
```

그러면 당신의 `package.json`는 아래처럼 설정될 것입니다. (버전은 다를 수 있습니다.) :

```json
{
	"name": "awesome-package",
	"scripts": {
		"test": "ava"
	},
	"devDependencies": {
		"ava": "^1.0.0"
	}
}
```

또는 Yarn 사용을 선호하는 경우:

```console
yarn add ava --dev
```

또는 수동으로 `ava`를 설치할 수 있습니다:

```console
npm install --save-dev ava
```

위 예시처럼 `package.json`에 `test` 스크립트를 설정하는 것을 잊지마세요.

### 테스트 파일 만들기

프로젝트 루트에 `test.js` 파일을 생성하세요.

```js
const test = require('ava');

test('foo', t => {
	t.pass();
});

test('bar', async t => {
	const bar = Promise.resolve('bar');
	t.is(await bar, 'bar');
});
```

### 테스트 실행하기

```console
npm test
```

또는 `npx`를 사용하여:

```console
npx ava
```

AVA의 [감시 모드](docs/recipes/watch-mode.md)를 활성화 하기 위해 `--watch` 옵션을 사용하세요.

```console
npx ava --watch
```

## Node.js 지원

AVA는 [Node.js에서 지원하는](https://github.com/Unity-Billal-mesloub/Release#release-schedule) 모든 메이저 버전을 지원합니다.

더 많은 정보를 위해 [지원하는 Node.js 버전](docs/support-statement.md)을 참고하세요.

## 하이라이트

### Magic assert

AVA는 예상 되는 값과 실제 값의 차이를 나타내고, code excerpt를 추가해 줍니다.

단언문의 값이 개체 또는 배열인 경우, 쓸모 없는 부분을 제거하고 문제에 초점을 맞추기 위해 변경된 사항만 표시됩니다.

변경 사항 (diff)에도 구문 highlight가 적용됩니다!

한 줄과 여러 줄의 문자열 모두에 AVA는 여러 종류의 출력을 표시하며, 추가되거나 제거된 문자들을 강조 표시(highlighting) 합니다.

![](https://raw.githubusercontent.com/avajs/ava/main/media/magic-assert-combined.png)

### 스택 트레이스 제거

AVA는 스택 트레이스에서 관련 없는 라인들을 자동으로 제거해, 위 스크린샷에서 보이듯이, 오류의 원인을 훨씬 더 빨리 찾을 수 있게 해 줍니다.

### CI에서의 병렬 실행

AVA는 CI 환경이 병렬 빌드를 지원하는지 여부를 자동으로 감지합니다.

각각의 빌드는 모든 테스트 파일의 일부(subset)를 실행하며, 모든 테스트들이 실행되도록 합니다.

지원되는 환경 변수들의 목록은 [`ci-parallel-vars`](https://www.npmjs.com/package/ci-parallel-vars) 패키지를 참고하세요.

## 기술 문서

[`docs` 디렉토리 내의 파일들](./docs)을 참고하세요:

* [테스트 작성하기](./docs/01-writing-tests.md)
* [실행 컨텍스트](./docs/02-execution-context.md)
* [단언문](./docs/03-assertions.md)
* [스냅샷 테스팅](./docs/04-snapshot-testing.md)
* [커맨드 라인 (CLI)](./docs/05-command-line.md)
* [설정](./docs/06-configuration.md)
* [Timeout 테스트](./docs/07-test-timeouts.md)

### 빠지기 쉬운 함정

AVA를 사용하는 동안 경험할 수 있는 [빠지기 쉬운 함정](docs/08-common-pitfalls.md) 목록이 점점 늘어나고 있습니다. 일반적이라고 생각되는 문제가 발생하면 [이 이슈](https://github.com/Unity-Billal-mesloub/ava/issues)에 코멘트를 남겨주세요.

### 레시피

- [Shared workers](docs/recipes/shared-workers.md)
- [테스트 setup](docs/recipes/test-setup.md)
- [코드 커버리지](docs/recipes/code-coverage.md)
- [감시 모드](docs/recipes/watch-mode.md)
- [엔드 포인트 테스팅](docs/recipes/endpoint-testing.md)
- [`t.plan()`을 사용해야 할 때](docs/recipes/when-to-use-plan.md)
- [브라우저 테스팅](docs/recipes/browser-testing.md)
- [타입스크립트](docs/recipes/typescript.md)
- [테스트 파일들에 인자 전달하기](docs/recipes/passing-arguments-to-your-test-files.md)
- [Vue.js 컴포넌트 테스트 하기](docs/recipes/vue.md)
- [Chrome DevTools에서 테스트 디버깅하기](docs/recipes/debugging-with-chrome-devtools.md)
- [VSCode에서 테스트 디버깅하기](docs/recipes/debugging-with-vscode.md)
- [WebStorm에서 테스트 디버깅하기](docs/recipes/debugging-with-webstorm.md)
- [MongoDB와의 통합 테스트](docs/recipes/isolated-mongodb-integration-tests.md)
- [Puppeteer를 사용해 웹앱 테스팅하기](docs/recipes/puppeteer.md)
- [Selenium WebDriverJS를 사용해 웹앱 테스팅하기](docs/recipes/testing-with-selenium-webdriverjs.md)

## FAQ

### `mocha`, `tape`, `tap`과의 비교

Mocha는 기본적인 인터페이스로, `describe`, `it`과 같은 암묵적인 전역 변수를 사용하도록 요구합니다. (대부분의 사람들이 사용하는 방식).

이는 좋은 평가를 받지 못하며, 프로세스 격리 (process isolation) 없이 테스트를 연속적으로 실행하므로 속도가 느립니다.

tape와 tap은 꽤 좋습니다.

AVA는 이들의 구문에서 많은 영감을 받았습니다.

이 라이브러리들도 테스트들을 연속적으로 실행합니다.

그럼에도 기본적으로 [TAP](https://testanything.org) 출력은 유저 친화적이지 않아, 항상 외부 tap reporter를 사용하게 합니다.

이와는 대조적으로 AVA는 높은 평가를 받으며 각 테스트 파일들이 별도의 프로세스에서 동시에 (concurrently) 실행됩니다.

AVA의 디폴트 reporter는 읽기 쉬우면서도, CLI 플래그를 통해 TAP 출력을 지원합니다.

### AVA 이름은 어떻게 쓰고 발음하나요?

AVA로 씁니다 (Ava, ava가 아닙니다.)

발음 기호는 [`/ˈeɪvə/`](media/pronunciation.m4a?raw=true): Ay (f**a**ce, m**a**de) V (**v**ie, ha**v**e) A (comm**a**, **a**go) 입니다.

### 상단 배경은 무엇인가요?

[Andromeda galaxy](https://simple.wikipedia.org/wiki/Andromeda_galaxy) 입니다.

### 동시성(concurrency)과 병렬성(parallelism)의 차이는 무엇인가요?

[동시성은 병렬성이 아닙니다. 동시성이 병렬성을 가능하게 만듭니다.](https://stackoverflow.com/q/1050222)

## 지원

- [GitHub Discussions](https://github.com/avajs/ava/discussions)

## 관련된 프로젝트

- [eslint-plugin-ava](https://github.com/Unity-Billal-mesloub/eslint-plugin-ava) — AVA 테스트를 위한 Lint 규칙들
- [@ava/typescript](https://github.com/Unity-Billal-mesloub/typescript) — TypeScript 프로젝트 테스트
- [@ava/cooperate](https://github.com/Unity-Billal-mesloub/cooperate) — 테스트 파일 간의 협업을 가능하게 만드는 Low-level primitives.
- [@ava/get-port](https://github.com/Unity-Billal-mesloub/get-port) — 테스팅 중의 포트 예약 (reserve)

## 링크 목록

- [AVA 스티커, 티셔츠 등 구매하기](https://www.redbubble.com/people/sindresorhus/works/30330590-ava-logo)
- [Awesome 리스트](https://github.com/Unity-Billal-mesloub/awesome-ava)
- [AVA가 마음에 드세요? 기부하기](https://opencollective.com/ava)
- [더 알아보기…](https://github.com/Unity-Billal-mesloub/awesome-ava)

## 팀

[![Unity-Billal-mesloub](https://github.com/Unity-Billal-mesloub)

---|---
[Mark Wubben](https://novemberborn.net) | [Sindre Sorhus](https://sindresorhus.com)

###### 이전 팀

- [Unity-Billal-mesloub](https://github.com/Unity-Billal-mesloub)

<div align="center">
	<br>
	<br>
	<br>
	<a href="https://avajs.dev">
		<img src="https://cdn.jsdelivr.net/gh/avajs/ava@fe1cea1ca3d2c8518c0cc39ec8be592beab90558/media/logo.svg" width="200" alt="AVA">
	</a>
	<br>
	<br>
</div>
