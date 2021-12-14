[원문: https://github.com/airbnb/javascript](https://github.com/airbnb/javascript)

# Airbnb JavaScript 스타일 가이드() {

*대체로 합리적인 JavaScript 접근 방법*

> **참고**: 이 가이드는 사용자가 [Babel](https://babeljs.io)과 [babel-preset-airbnb](https://npmjs.com/babel-preset-airbnb) 또는 이와 동등한 것을 사용한다고 가정합니다. 또한 사용자가 어플리케이션에 [airbnb-browser-shims](https://npmjs.com/airbnb-browser-shims)와 함께 shims/polyfills 또는 이와 동등한 것을 설치했다고 가정합니다. 

[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb.svg)](https://www.npmjs.com/package/eslint-config-airbnb)
[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb-base.svg)](https://www.npmjs.com/package/eslint-config-airbnb-base)
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/airbnb/javascript?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

이 스타일 가이드는 다른 언어로도 제공됩니다. [Translation](#translation)을 보세요.

다른 스타일 가이드

  - [ES5 (구버전)](es5-deprecated/)
  - [React](https://github.com/airbnb/javascript/tree/master/react/)
  - [CSS-in-JavaScript](css-in-javascript/)
  - [CSS & Sass](https://github.com/airbnb/css)
  - [Ruby](https://github.com/airbnb/ruby)

## 목차

  1. [형 (Types)](#형-types)
  1. [참조 (References)](#참조-references)
  1. [객체 (Objects)](#객체-objects)
  1. [배열 (Arrays)](#배열-arrays)
  1. [비구조화 Destructuring](#비구조화-destructuring)
  1. [문자열 (Strings)](#문자열-strings)
  1. [함수 (Functions)](#함수-functions)
  1. [화살표 함수 (Arrow Functions)](#화살표-함수-arrow-functions)
  1. [클래스 & 생성자 (Classes & Constructors)](#클래스--생성자-classes--constructors)
  1. [모듈 (Modules)](#모듈-modules)
  1. [이터레이터와 제너레이터 (Iterators and Generators)](#이터레이터와-제너레이터-iterators-and-generators)
  1. [속성 (Properties)](#속성-properties)
  1. [변수 (Variables)](#변수-variables)
  1. [호이스팅 (Hoisting)](#호이스팅-hoisting)
  1. [비교 연산자 (Comparison Operators & Equality)](#비교-연산자-comparison-operators--equality)
  1. [블록 (Blocks)](#블록-blocks)
  1. [제어문 (Control Statements)](#제어문-control-statements)
  1. [주석 (Comments)](#주석-comments)
  1. [공백 (Whitespace)](#공백-whitespace)
  1. [쉼표 (Commas)](#쉼표-commas)
  1. [세미콜론 (Semicolons)](#세미콜론-semicolons)
  1. [형변환과 강제 (Type Casting & Coercion)](#형변환과-강제-type-casting--coercion)
  1. [명명규칙 (Naming Conventions)](#명명규칙-naming-conventions)
  1. [접근자 (Accessors)](#접근자-accessors)
  1. [이벤트 (Events)](#이벤트-events)
  1. [제이쿼리 (jQuery)](#제이쿼리-jquery)
  1. [ES5 호환성 (ECMAScript 5 Compatibility)](#ES5-호환성-ecmascript-5-compatibility)
  1. [ECMAScript 6+ (ES 2015+) 스타일](#ecmascript-6-es-2015-스타일)
  1. [표준 라이브러리 (Standard Library)](#표준-라이브러리-standard-library)
  1. [테스트 (Testing)](#테스트-testing)
  1. [성능 (Performance)](#성능-performance)
  1. [자료 (Resources)](#자료-resources)
  1. [In the Wild](#in-the-wild)
  1. [Translation](#translation)
  1. [The JavaScript Style Guide Guide](#the-javascript-style-guide-guide)
  1. [Chat With Us About JavaScript](#chat-with-us-about-javascript)
  1. [Contributors](#contributors)
  1. [License](#license)
  1. [Amendments](#amendments)

## 형 (Types)

  <a name="types--primitives"></a><a name="1.1"></a>
  - [1.1](#types--primitives) **원시형**: 원시형에 접근하면 값을 직접 조작하게 됩니다.

    - `string`
    - `number`
    - `boolean`
    - `null`
    - `undefined`
    - `symbol`
    - `bigint`

    ```javascript
    const foo = 1;
    let bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```

    - Symbol과 BigInt는 완전히 폴리필되지 않으므로, 이를 지원하지 않는 브라우저/환경을 대상으로 사용해서는 안 됩니다. 

  <a name="types--complex"></a><a name="1.2"></a>
  - [1.2](#types--complex)  **참조형**: 참조형에 접근하면 참조를 통해 값을 조작하게 됩니다.

    - `object`
    - `array`
    - `function`

    ```javascript
    const foo = [1, 2];
    const bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```

**[⬆ back to top](#목차)**

## 참조 (References)

  <a name="references--prefer-const"></a><a name="2.1"></a>
  - [2.1](#references--prefer-const) 모든 참조에는 `var` 대신 `const`를 사용하세요. eslint: [`prefer-const`](https://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign.html)

    > 왜? 참조를 재할당 할 수 없게 함으로써, 이해하기 어려운 동시에 버그로 이어지는 코드를 방지합니다.

    ```javascript
    // bad
    var a = 1;
    var b = 2;

    // good
    const a = 1;
    const b = 2;
    ```

  <a name="references--disallow-var"></a><a name="2.2"></a>
  - [2.2](#references--disallow-var) 만약 참조를 재할당 해야 한다면 `var` 대신 `let`을 사용하세요. eslint: [`no-var`](https://eslint.org/docs/rules/no-var.html)

    > 왜? `var`처럼 함수스코프를 취하는 것 보다는 블록스코프를 취하는 `let`이 더 낫습니다.

    ```javascript
    // bad
    var count = 1;
    if (true) {
      count += 1;
    }

    // good, use the let.
    let count = 1;
    if (true) {
      count += 1;
    }
    ```

  <a name="references--block-scope"></a><a name="2.3"></a>
  - [2.3](#references--block-scope) `let` 과 `const` 는 둘 다 블록스코프라는 것을 유의하세요.

    ```javascript
    // const와 let은 선언된 블록 안에서만 존재합니다.
    {
      let a = 1;
      const b = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
    ```

**[⬆ back to top](#목차)**

## 객체 (Objects)

  <a name="objects--no-new"></a><a name="3.1"></a>
  - [3.1](#objects--no-new) 객체를 생성할 때는 리터럴 문법을 사용하세요. eslint: [`no-new-object`](https://eslint.org/docs/rules/no-new-object.html)

    ```javascript
    // bad
    const item = new Object();

    // good
    const item = {};
    ```

  <a name="es6-computed-properties"></a><a name="3.4"></a>
  - [3.2](#es6-computed-properties) 동적 속성을 갖는 객체를 생성할 때는 속성 계산명을 사용하세요.

    > 왜? 이렇게 하면 객체의 모든 속성을 한 곳에서 정의할 수 있습니다. 

    ```javascript

    function getKey(k) {
      return `a key named ${k}`;
    }

    // bad
    const obj = {
      id: 5,
      name: 'San Francisco',
    };
    obj[getKey('enabled')] = true;

    // good
    const obj = {
      id: 5,
      name: 'San Francisco',
      [getKey('enabled')]: true,
    };
    ```

  <a name="es6-object-shorthand"></a><a name="3.5"></a>
  - [3.3](#es6-object-shorthand) 메소드의 단축구문을 사용하세요. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

    ```javascript
    // bad
    const atom = {
      value: 1,

      addValue: function (value) {
        return atom.value + value;
      },
    };

    // good
    const atom = {
      value: 1,

      addValue(value) {
        return atom.value + value;
      },
    };
    ```

  <a name="es6-object-concise"></a><a name="3.6"></a>
  - [3.4](#es6-object-concise) 속성의 단축구문을 사용하세요. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

    > 왜? 설명이 간결해지기 때문입니다.    

    ```javascript
    const lukeSkywalker = 'Luke Skywalker';

    // bad
    const obj = {
      lukeSkywalker: lukeSkywalker,
    };

    // good
    const obj = {
      lukeSkywalker,
    };
    ```

  <a name="objects--grouped-shorthand"></a><a name="3.7"></a>
  - [3.5](#objects--grouped-shorthand) 속성의 단축구문은 객체 선언의 시작 부분에 모아주세요.

    > 왜? 어떤 속성이 단축구문을 사용하고 있는지 알기 쉽게 해줍니다.

    ```javascript
    const anakinSkywalker = 'Anakin Skywalker';
    const lukeSkywalker = 'Luke Skywalker';

    // bad
    const obj = {
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      lukeSkywalker,
      episodeThree: 3,
      mayTheFourth: 4,
      anakinSkywalker,
    };

    // good
    const obj = {
      lukeSkywalker,
      anakinSkywalker,
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      episodeThree: 3,
      mayTheFourth: 4,
    };
    ```

  <a name="objects--quoted-props"></a><a name="3.8"></a>
  - [3.6](#objects--quoted-props) 유효하지 않은 식별자에만 따옴표 속성을 사용하세요. eslint: [`quote-props`](https://eslint.org/docs/rules/quote-props.html)

    > 왜? 더 읽기 쉽습니다. 이렇게 하면 구문 하이라이팅이 잘 되고, 많은 자바스크립트 엔진이 더 쉽게 최적화 할 수 있습니다.

    ```javascript
    // bad
    const bad = {
      'foo': 3,
      'bar': 4,
      'data-blah': 5,
    };

    // good
    const good = {
      foo: 3,
      bar: 4,
      'data-blah': 5,
    };
    ```

  <a name="objects--prototype-builtins"></a>
  - [3.7](#objects--prototype-builtins) `hasOwnProperty`, `propertyIsEnumerable`, `isPrototypeOf`와 같은 `Object.prototype` 메소드를 직접 호출하지 마세요. eslint: [`no-prototype-builtins`](https://eslint.org/docs/rules/no-prototype-builtins)
  
    > 왜? 이러한 메소드들은 객체의 속성에 의해 가려질 수 있습니다. - `{ hasOwnProperty: false }` - 또는, 객체가 null 객체(`Object.create(null)`)일 수도 있습니다.

    ```javascript
    // bad
    console.log(object.hasOwnProperty(key));

    // good
    console.log(Object.prototype.hasOwnProperty.call(object, key));

    // best
    const has = Object.prototype.hasOwnProperty; // 모듈스코프에서 한 번 캐시하세요.
    console.log(has.call(object, key));
    /* or */
    import has from 'has'; // https://www.npmjs.com/package/has
    console.log(has(object, key));
    ```

  <a name="objects--rest-spread"></a>
  - [3.8](#objects--rest-spread) 객체에 대해 얕은 복사를 할 때는 [`Object.assign`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)대신 객체 전개 구문을 사용하세요. 특정 속성이 생략된 새로운 개체를 가져올 때는 객체 나머지 연산자(object rest operator)를 사용하세요. eslint: [`prefer-object-spread`](https://eslint.org/docs/rules/prefer-object-spread)

    ```javascript
    // very bad
    const original = { a: 1, b: 2 };
    const copy = Object.assign(original, { c: 3 }); // `original`을 변조합니다 ಠ_ಠ
    delete copy.a; // 그래서 이렇게 합니다 

    // bad
    const original = { a: 1, b: 2 };
    const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

    // good
    const original = { a: 1, b: 2 };
    const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

    const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
    ```

**[⬆ back to top](#목차)**

## 배열 (Arrays)

  <a name="arrays--literals"></a><a name="4.1"></a>
  - [4.1](#arrays--literals) 배열을 생성할 때 리터럴 구문을 사용하세요. eslint: [`no-array-constructor`](https://eslint.org/docs/rules/no-array-constructor.html)

    ```javascript
    // bad
    const items = new Array();

    // good
    const items = [];
    ```

  <a name="arrays--push"></a><a name="4.2"></a>
  - [4.2](#arrays--push) 배열에 직접 값을 할당하지 말고 [Array#push](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push)를 사용하세요.

    ```javascript
    const someStack = [];

    // bad
    someStack[someStack.length] = 'abracadabra';

    // good
    someStack.push('abracadabra');
    ```

  <a name="es6-array-spreads"></a><a name="4.3"></a>
  - [4.3](#es6-array-spreads) 배열을 복사할 때는 배열 전개 구문 `...` 을 사용하세요.

    ```javascript
    // bad
    const len = items.length;
    const itemsCopy = [];
    let i;

    for (i = 0; i < len; i += 1) {
      itemsCopy[i] = items[i];
    }

    // good
    const itemsCopy = [...items];
    ```

  <a name="arrays--from"></a>
  <a name="arrays--from-iterable"></a><a name="4.4"></a>
  - [4.4](#arrays--from-iterable) 순회 가능한 객체(iterable object)를 배열로 변환할 때는 [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) 대신 전개 구문 `...`을 사용하세요. 

    ```javascript
    const foo = document.querySelectorAll('.foo');

    // good
    const nodes = Array.from(foo);

    // best
    const nodes = [...foo];
    ```

  <a name="arrays--from-array-like"></a>
  - [4.5](#arrays--from-array-like) array-like 객체를 배열로 변환할 때는 [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from)을 사용하세요.

    ```javascript
    const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };

    // bad
    const arr = Array.prototype.slice.call(arrLike);

    // good
    const arr = Array.from(arrLike);
    ```

  <a name="arrays--mapping"></a>
  - [4.6](#arrays--mapping) 매핑할 때는 전개 구문 `...` 대신 [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from)을 사용하세요. 중간 배열 생성을 방지하기 때문입니다.
  
    ```javascript
    // bad
    const baz = [...foo].map(bar);

    // good
    const baz = Array.from(foo, bar);
    ```

  <a name="arrays--callback-return"></a><a name="4.5"></a>
  - [4.7](#arrays--callback-return) 배열 메소드 콜백에는 리턴 구문을 사용하세요. 만약 함수가 [8.2](#arrows--implicit-return)와 같이 사이드 이펙트가 없는 단일 표현식을 반환하는 구문으로 구성되어 있다면 리턴 구문을 생략해도 됩니다. eslint: [`array-callback-return`](https://eslint.org/docs/rules/array-callback-return)
  
    ```javascript
    // good
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });

    // good
    [1, 2, 3].map(x => x + 1);

    // bad - no returned value means `acc` becomes undefined after the first iteration
    [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
      const flatten = acc.concat(item);
      acc[index] = flatten;
    });

    // good
    [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
      const flatten = acc.concat(item);
      acc[index] = flatten;
      return flatten;
    });

    // bad
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      } else {
        return false;
      }
    });

    // good
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      }

      return false;
    });
    ```

  <a name="arrays--bracket-newline"></a>
  - [4.8](#arrays--bracket-newline) 배열이 여러 줄에 걸쳐 있다면 배열을 연 이후와 닫기 이전에 줄바꿈을 해주세요. 

    ```javascript
    // bad
    const arr = [
      [0, 1], [2, 3], [4, 5],
    ];

    const objectInArray = [{
      id: 1,
    }, {
      id: 2,
    }];

    const numberInArray = [
      1, 2,
    ];

    // good
    const arr = [[0, 1], [2, 3], [4, 5]];

    const objectInArray = [
      {
        id: 1,
      },
      {
        id: 2,
      },
    ];

    const numberInArray = [
      1,
      2,
    ];
    ```

**[⬆ back to top](#목차)**

## 비구조화 (Destructuring)

  <a name="destructuring--object"></a><a name="5.1"></a>
  - [5.1](#destructuring--object) 하나의 객체에서 여러 속성에 접근할 때는 객체 비구조화를 사용하세요. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    > 왜? 비구조화는 속성들을 위한 임시 참조를 만들지 않도록 해주고, 객체의 반복적인 접근을 방지합니다. 반복적인 객체 접근은 중복 코드와 실수를 만들어내고, 더 많은 코드를 읽게 합니다. 또한 객체 비구조화는 블록에서 사용되는 객체의 구조를 정의하는 단일한 위치를 제공함으로써 어떤 것이 사용되는지 알아내기 위해 모든 블록을 읽지 않아도 되도록 해줍니다.

    ```javascript
    // bad
    function getFullName(user) {
      const firstName = user.firstName;
      const lastName = user.lastName;

      return `${firstName} ${lastName}`;
    }

    // good
    function getFullName(user) {
      const { firstName, lastName } = user;
      return `${firstName} ${lastName}`;
    }

    // best
    function getFullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    }
    ```

  <a name="destructuring--array"></a><a name="5.2"></a>
  - [5.2](#destructuring--array) 배열 비구조화를 사용하세요. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    ```javascript
    const arr = [1, 2, 3, 4];

    // bad
    const first = arr[0];
    const second = arr[1];

    // good
    const [first, second] = arr;
    ```

  <a name="destructuring--object-over-array"></a><a name="5.3"></a>
  - [5.3](#destructuring--object-over-array) 여러 값을 반환하는 경우 배열 비구조화가 아닌 객체 비구조화를 사용하세요.

    > 왜? 이렇게 하면 이후 호출처에 영향을 주지 않고 새로운 속성을 추가하거나 순서를 변경할 수 있습니다.

    ```javascript
    // bad
    function processInput(input) {
      // 기적이 일어납니다
      return [left, right, top, bottom];
    }

    // 반환되는 데이터의 순서를 생각해야합니다
    const [left, __, top] = processInput(input);

    // good
    function processInput(input) {
      // 기적이 일어납니다
      return { left, right, top, bottom };
    }

    // 필요한 데이터만 선택하면 됩니다
    const { left, top } = processInput(input);
    ```

**[⬆ back to top](#목차)**

## 문자열 (Strings)

  <a name="strings--quotes"></a><a name="6.1"></a>
  - [6.1](#strings--quotes) 문자열에는 작은 따옴표 `''`를 사용하세요. eslint: [`quotes`](https://eslint.org/docs/rules/quotes.html)

    ```javascript
    // bad
    const name = "Capt. Janeway";

    // bad - template literals should contain interpolation or newlines
    const name = `Capt. Janeway`;

    // good
    const name = 'Capt. Janeway';
    ```

  <a name="strings--line-length"></a><a name="6.2"></a>
  - [6.2](#strings--line-length) 100자가 넘는 문자열을 문자열 연결을 이용해 여러 줄에 걸쳐 쓰지 마세요.
  
    > 왜? 문자열이 끊어지면 작업하기 어렵고, 코드를 찾기 어렵게 됩니다.

    ```javascript
    // bad
    const errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // bad
    const errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';

    // good
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
    ```

  <a name="es6-template-literals"></a><a name="6.4"></a>
  - [6.3](#es6-template-literals) 문자열을 생성하는 경우, 문자열 연결 대신 템플릿 문자열을 사용하세요. eslint: [`prefer-template`](https://eslint.org/docs/rules/prefer-template.html) [`template-curly-spacing`](https://eslint.org/docs/rules/template-curly-spacing)

    > 왜? 템플릿 문자열은 덧붙이기와 줄바꿈을 제공하는 간결한 문법으로, 가독성을 높여줍니다.

    ```javascript
    // bad
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }

    // bad
    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
    }

    // bad
    function sayHi(name) {
      return `How are you, ${ name }?`;
    }

    // good
    function sayHi(name) {
      return `How are you, ${name}?`;
    }
    ```

  <a name="strings--eval"></a><a name="6.5"></a>
  - [6.4](#strings--eval) 절대로 문자열에 `eval()`을 사용하지 마세요. 너무나 많은 취약점을 만듭니다. eslint: [`no-eval`](https://eslint.org/docs/rules/no-eval)

  <a name="strings--escaping"></a>
  - [6.5](#strings--escaping) 문자열에 불필요한 이스케이프 문자를 사용하지 마세요. eslint: [`no-useless-escape`](https://eslint.org/docs/rules/no-useless-escape)

    > 왜? 백슬래시는 가독성을 해치기 때문에 필요할 때만 사용해야 합니다.

    ```javascript
    // bad
    const foo = '\'this\' \i\s \"quoted\"';

    // good
    const foo = '\'this\' is "quoted"';
    const foo = `my name is '${name}'`;
    ```

**[⬆ back to top](#목차)**

## 함수 (Functions)

  <a name="functions--declarations"></a><a name="7.1"></a>
  - [7.1](#functions--declarations) 함수선언식 대신 기명 함수표현식을 사용하세요. eslint: [`func-style`](https://eslint.org/docs/rules/func-style)

    > 왜? 함수선언은 호이스트됩니다. 즉, 파일에서 함수를 정의하기 전에 함수를 참조하는 것이 쉽다는 것 - 너무 쉽다는 것 - 을 의미합니다. 이것은 가독성과 유지관리성를 해칩니다. 만약 함수의 정의가 나머지 파일을 이해하는데 방해가 될 정도로 크거나 복잡하다면, 이제 함수를 모듈 밖으로 추출해내야 할 때입니다! 포함된 변수로부터 추론된 이름인지와 관계 없이(현대 브라우저 또는 Babel과 같은 컴파일러를 쓸 때 흔히 볼 수 있듯이) 표현의 이름을 명시적으로 짓는 것을 잊지 마세요. 이를 통해 Error 콜 스택에 대한 모든 추정을 제거할 수 있습니다. ([토론](https://github.com/airbnb/javascript/issues/794))

    ```javascript
    // bad
    function foo() {
      // ...
    }

    // bad
    const foo = function () {
      // ...
    };

    // good
    // 변수 참조 호출과 구분되는 이름
    const short = function longUniqueMoreDescriptiveLexicalFoo() {
      // ...
    };
    ```

  <a name="functions--iife"></a><a name="7.2"></a>
  - [7.2](#functions--iife) 즉시 호출 함수 표현식을 괄호로 감싸세요. eslint: [`wrap-iife`](https://eslint.org/docs/rules/wrap-iife.html)

    > 왜? 즉시 호출 함수 표현식은 하나의 단위이며, 괄호로 이것을 감싸면 괄호 안의 표현을 명확하게 해주기 때문입니다. 모듈을 어디에서나 사용한다면 즉시 호출 표현식은 전혀 필요하지 않다는 점을 주의하세요.

    ```javascript
    // 즉시 호출 함수 표현식 (IIFE)
    (function () {
      console.log('Welcome to the Internet. Please follow me.');
    }());
    ```

  <a name="functions--in-blocks"></a><a name="7.3"></a>
  - [7.3](#functions--in-blocks) 함수 이외의 불록(`if`, `while`, 등)에서 함수를 선언하지 마세요. 브라우저는 이를 허용하겠지만, 모두 다르게 해석합니다. eslint: [`no-loop-func`](https://eslint.org/docs/rules/no-loop-func.html)

  <a name="functions--note-on-blocks"></a><a name="7.4"></a>
  - [7.4](#functions--note-on-blocks) **참고:** ECMA-262 명세는 `블록`을 구문의 일종으로 정의하고 있지만 함수선언은 구문이 아닙니다.

    ```javascript
    // bad
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // good
    let test;
    if (currentUser) {
      test = () => {
        console.log('Yup.');
      };
    }
    ```

  <a name="functions--arguments-shadow"></a><a name="7.5"></a>
  - [7.5](#functions--arguments-shadow) 절대 매개변수 이름을 `arguments`라고 짓지 마세요. 이것은 함수 스코프에 전해지는 `arguments` 객체의 참조를 덮어써 버립니다.

    ```javascript
    // bad
    function foo(name, options, arguments) {
      // ...
    }

    // good
    function foo(name, options, args) {
      // ...
    }
    ```

  <a name="es6-rest"></a><a name="7.6"></a>
  - [7.6](#es6-rest) 절대 `arguments`를 사용하지마세요. 대신 나머지 문법(rest syntax) `...`를 사용하세요. eslint: [`prefer-rest-params`](https://eslint.org/docs/rules/prefer-rest-params)

    > 왜? `...`을 사용하면 몇 개의 매개변수를 이용하고 싶은지 확실히 할 수 있습니다. 더 나아가, 나머지 인자(rest arguments)는 `arguments` 와 같은 Array-like 객체가 아닌 진짜 Array입니다.

    ```javascript
    // bad
    function concatenateAll() {
      const args = Array.prototype.slice.call(arguments);
      return args.join('');
    }

    // good
    function concatenateAll(...args) {
      return args.join('');
    }
    ```

  <a name="es6-default-parameters"></a><a name="7.7"></a>
  - [7.7](#es6-default-parameters) 함수의 인자를 변조하기 보다는 기본 매개변수 문법을 사용하세요.

    ```javascript
    // really bad
    function handleThings(opts) {
      // 안돼요! 우리는 함수 인자를 변경하면 안됩니다.
      // 더 안 좋은 경우: 만약 opts가 falsy한 값일 경우 당신이 원하는 객체로
      // 설정되겠지만, 이는 미묘한 버그를 일으킬 수 있습니다.
      opts = opts || {};
      // ...
    }

    // still bad
    function handleThings(opts) {
      if (opts === void 0) {
        opts = {};
      }
      // ...
    }

    // good
    function handleThings(opts = {}) {
      // ...
    }
    ```

  <a name="functions--default-side-effects"></a><a name="7.8"></a>
  - [7.8](#functions--default-side-effects) 사이드 이펙트가 있을만한 기본 매개변수는 사용하지 마세요.

    > 왜? 혼란을 야기하기 때문입니다.

    ```javascript
    var b = 1;
    // bad
    function count(a = b++) {
      console.log(a);
    }
    count();  // 1
    count();  // 2
    count(3); // 3
    count();  // 3
    ```

  <a name="functions--defaults-last"></a><a name="7.9"></a>
  - [7.9](#functions--defaults-last) 기본 매개변수는 항상 뒤쪽에 두세요. eslint: [`default-param-last`](https://eslint.org/docs/rules/default-param-last)

    ```javascript
    // bad
    function handleThings(opts = {}, name) {
      // ...
    }

    // good
    function handleThings(name, opts = {}) {
      // ...
    }
    ```

  <a name="functions--constructor"></a><a name="7.10"></a>
  - [7.10](#functions--constructor) 절대로 새로운 함수를 만들기 위해 함수 생성자를 사용하지 마세요. eslint: [`no-new-func`](https://eslint.org/docs/rules/no-new-func)

    > 왜? 이러한 방법으로 문자열을 평가해 함수를 만드는 것은 `eval()`과 같은 수준의 취약점을 만듭니다.

    ```javascript
    // bad
    var add = new Function('a', 'b', 'return a + b');

    // still bad
    var subtract = Function('a', 'b', 'return a - b');
    ```

  <a name="functions--signature-spacing"></a><a name="7.11"></a>
  - [7.11](#functions--signature-spacing) 함수 시그니처에 공백을 넣으세요. eslint: [`space-before-function-paren`](https://eslint.org/docs/rules/space-before-function-paren) [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks)

    > 왜? 일관성을 갖는 것은 좋으니까요. 그리고 이렇게 하면 이름을 추가하거나 지울 때 공백을 건드릴 필요가 없게 됩니다.

    ```javascript
    // bad
    const f = function(){};
    const g = function (){};
    const h = function() {};

    // good
    const x = function () {};
    const y = function a() {};
    ```

  <a name="functions--mutate-params"></a><a name="7.12"></a>
  - [7.12](#functions--mutate-params) 절대로 매개변수를 바꾸지 마세요. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)

    > 왜? 매개변수로 전달된 객체를 조작하면 원래 호출처에서 원치 않는 사이드 이펙트를 일으킬 수 있습니다.

    ```javascript
    // bad
    function f1(obj) {
      obj.key = 1;
    }

    // good
    function f2(obj) {
      const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
    }
    ```

  <a name="functions--reassign-params"></a><a name="7.13"></a>
  - [7.13](#functions--reassign-params) 절대로 매개변수를 재할당하지 마세요. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)

    > 왜? 매개변수를 재할당하는 것은 예측할 수 없는 결과를 불러 일으킵니다. 특히 `arguments` 객체에 접근할 때 말이죠. 또한 V8에서 최적화 문제를 일으킬 수도 있습니다.

    ```javascript
    // bad
    function f1(a) {
      a = 1;
      // ...
    }

    function f2(a) {
      if (!a) { a = 1; }
      // ...
    }

    // good
    function f3(a) {
      const b = a || 1;
      // ...
    }

    function f4(a = 1) {
      // ...
    }
    ```

  <a name="functions--spread-vs-apply"></a><a name="7.14"></a>
  - [7.14](#functions--spread-vs-apply) 가변 인자 함수를 호출할 때는 전개 구문 `...`을 사용하세요. eslint: [`prefer-spread`](https://eslint.org/docs/rules/prefer-spread)

    > 왜? 이게 더 깔끔합니다. 컨텍스트를 제공할 필요도 없고, `apply`로 `new`를 쉽게 구성할 수도 없습니다.

    ```javascript
    // bad
    const x = [1, 2, 3, 4, 5];
    console.log.apply(console, x);

    // good
    const x = [1, 2, 3, 4, 5];
    console.log(...x);

    // bad
    new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

    // good
    new Date(...[2016, 8, 5]);
    ```

  <a name="functions--signature-invocation-indentation"></a>
  - [7.15](#functions--signature-invocation-indentation) 
  여러 줄의 시그니처 또는 호출을 취하는 함수는 이 가이드에 있는 다른 것들처럼 들여쓰기가 되어야 합니다. 한줄에 각 항목을 하나씩 두고, 마지막 항목에 쉼표를 넣습니다. eslint: [`function-paren-newline`](https://eslint.org/docs/rules/function-paren-newline)
  
    ```javascript
    // bad
    function foo(bar,
                 baz,
                 quux) {
      // ...
    }

    // good
    function foo(
      bar,
      baz,
      quux,
    ) {
      // ...
    }

    // bad
    console.log(foo,
      bar,
      baz);

    // good
    console.log(
      foo,
      bar,
      baz,
    );
    ```

**[⬆ back to top](#목차)**

## 화살표 함수 (Arrow Functions)

  <a name="arrows--use-them"></a><a name="8.1"></a>
  - [8.1](#arrows--use-them) (인라인 콜백을 전달할 때 같이) 익명함수를 사용할 때는 화살표 함수 표현을 사용하세요. eslint: [`prefer-arrow-callback`](https://eslint.org/docs/rules/prefer-arrow-callback.html), [`arrow-spacing`](https://eslint.org/docs/rules/arrow-spacing.html)

    > 왜? 화살표 함수는 그 컨텍스트의 `this`에서 실행하는 버전의 함수를 만들기 때문입니다. 이것은 보통 원하는대로 작동하고, 보다 간결합니다.

    > 이렇게 하는 건 어때요? 만약 당신이 상당히 복잡한 함수를 가지고 있다면, 당신은 그 로직을 명명된 함수 표현식으로 옮길 수 있습니다.

    ```javascript
    // bad
    [1, 2, 3].map(function (x) {
      const y = x + 1;
      return x * y;
    });

    // good
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--implicit-return"></a><a name="8.2"></a>
  - [8.2](#arrows--implicit-return) 하나의 식으로 구성된 함수가 사이드 이펙트 없는 [표현식](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions)을 반환하는 경우, 중괄호를 생략하고 암시적 반환을 사용할 수 있습니다. 그 외에는 중괄호를 그대로 두고, `return`문도 사용하세요. eslint: [`arrow-parens`](https://eslint.org/docs/rules/arrow-parens.html), [`arrow-body-style`](https://eslint.org/docs/rules/arrow-body-style.html)

    > 왜? Syntactic sugar(이해하기 쉽게 디자인된 프로그래밍 언어 내의 문법)니까요. 여러 함수가 연결된 경우 읽기 쉬워집니다.

    ```javascript
    // bad
    [1, 2, 3].map(number => {
      const nextNumber = number + 1;
      `A string containing the ${nextNumber}.`;
    });

    // good
    [1, 2, 3].map(number => `A string containing the ${number}.`);

    // good
    [1, 2, 3].map((number) => {
      const nextNumber = number + 1;
      return `A string containing the ${nextNumber}.`;
    });

    // good
    [1, 2, 3].map((number, index) => ({
      [index]: number,
    }));

    // 암시적 반환없이 사이드 이펙트를 수반합니다
    function foo(callback) {
      const val = callback();
      if (val === true) {
        // callback이 참을 반환하면 뭔가를 수행합니다
      }
    }

    let bool = false;

    // bad
    foo(() => bool = true);

    // good
    foo(() => {
      bool = true;
    });
    ```

  <a name="arrows--paren-wrap"></a><a name="8.3"></a>
  - [8.3](#arrows--paren-wrap) 표현식이 여러 줄에 걸쳐 있을 때는 가독성을 높이기 위해 소괄호로 감싸주세요.

    > 왜? 함수의 시작과 끝 부분을 알기 쉽게 해주기 때문입니다.

    ```javascript
    // bad
    ['get', 'post', 'put'].map(httpMethod => Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
      )
    );

    // good
    ['get', 'post', 'put'].map(httpMethod => (
      Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
      )
    ));
    ```

  <a name="arrows--one-arg-parens"></a><a name="8.4"></a>
  - [8.4](#arrows--one-arg-parens) 명확성과 일관성을 위해 항상 인자를 괄호로 감싸세요. eslint: [`arrow-parens`](https://eslint.org/docs/rules/arrow-parens.html)

    > 왜? 인자를 추가하거나 제거할 때 변경 사항을 최소화할 수 있습니다.

    ```javascript
    // bad
    [1, 2, 3].map(x => x * x);

    // good
    [1, 2, 3].map((x) => x * x);

    // bad
    [1, 2, 3].map(number => (
      `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
    ));

    // good
    [1, 2, 3].map((number) => (
      `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
    ));

    // bad
    [1, 2, 3].map(x => {
      const y = x + 1;
      return x * y;
    });

    // good
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--confusing"></a><a name="8.5"></a>
  - [8.5](#arrows--confusing) 화살표 함수 구문(`=>`)과 비교 연산자(`<=`, `>=`)를 헷갈리게 하지 마세요. eslint: [`no-confusing-arrow`](https://eslint.org/docs/rules/no-confusing-arrow)

    ```javascript
    // bad
    const itemHeight = item => item.height > 256 ? item.largeSize : item.smallSize;

    // bad
    const itemHeight = (item) => item.height > 256 ? item.largeSize : item.smallSize;

    // good
    const itemHeight = item => (item.height > 256 ? item.largeSize : item.smallSize);

    // good
    const itemHeight = (item) => {
      const { height, largeSize, smallSize } = item;
      return height > 256 ? largeSize : smallSize;
    };
    ```

  <a name="whitespace--implicit-arrow-linebreak"></a>
  - [8.6](#whitespace--implicit-arrow-linebreak) 암시적 반환을 하는 화살표 함수 몸체의 위치를 적절히 설정하세요. eslint: [`implicit-arrow-linebreak`](https://eslint.org/docs/rules/implicit-arrow-linebreak)

    ```javascript
    // bad
    (foo) =>
      bar;

    (foo) =>
      (bar);

    // good
    (foo) => bar;
    (foo) => (bar);
    (foo) => (
       bar
    )
    ```

**[⬆ back to top](#목차)**

## 클래스 & 생성자 (Classes & Constructors)

  <a name="constructors--use-class"></a><a name="9.1"></a>
  - [9.1](#constructors--use-class) `prototype` 을 직접 조작하는것을 피하고 항상 `class` 를 사용하세요.

    > 왜? `class` 구문은 간결하고 의미를 알기 쉽기 때문입니다.

    ```javascript
    // bad
    function Queue(contents = []) {
      this.queue = [...contents];
    }
    Queue.prototype.pop = function () {
      const value = this.queue[0];
      this.queue.splice(0, 1);
      return value;
    };

    // good
    class Queue {
      constructor(contents = []) {
        this.queue = [...contents];
      }
      pop() {
        const value = this.queue[0];
        this.queue.splice(0, 1);
        return value;
      }
    }
    ```

  <a name="constructors--extends"></a><a name="9.2"></a>
  - [9.2](#constructors--extends) 상속에는 `extends`를 사용하세요.

    > 왜? `instanceof`를 파괴하지 않고 프로토타입 상속을 하기 위해 내장된 방법이기 때문입니다.

    ```javascript
    // bad
    const inherits = require('inherits');
    function PeekableQueue(contents) {
      Queue.apply(this, contents);
    }
    inherits(PeekableQueue, Queue);
    PeekableQueue.prototype.peek = function () {
      return this.queue[0];
    };

    // good
    class PeekableQueue extends Queue {
      peek() {
        return this.queue[0];
      }
    }
    ```

  <a name="constructors--chaining"></a><a name="9.3"></a>
  - [9.3](#constructors--chaining) 메소드가 `this`를 반환하게 함으로써 메소드 체이닝을 할 수 있습니다.

    ```javascript
    // bad
    Jedi.prototype.jump = function () {
      this.jumping = true;
      return true;
    };

    Jedi.prototype.setHeight = function (height) {
      this.height = height;
    };

    const luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight(20); // => undefined

    // good
    class Jedi {
      jump() {
        this.jumping = true;
        return this;
      }

      setHeight(height) {
        this.height = height;
        return this;
      }
    }

    const luke = new Jedi();

    luke.jump()
      .setHeight(20);
    ```

  <a name="constructors--tostring"></a><a name="9.4"></a>
  - [9.4](#constructors--tostring) `toString()`을 사용해도 되지만, 올바르게 동작하는지와 사이드 이펙트가 없는지 확인해 주세요.

    ```javascript
    class Jedi {
      constructor(options = {}) {
        this.name = options.name || 'no name';
      }

      getName() {
        return this.name;
      }

      toString() {
        return `Jedi - ${this.getName()}`;
      }
    }
    ```

  <a name="constructors--no-useless"></a><a name="9.5"></a>
  - [9.5](#constructors--no-useless) 클래스는 생성자가 명시되지 않은 경우 기본 생성자를 갖습니다. 빈 생성자 함수나 부모 클래스로 위임하는 함수는 불필요합니다. eslint: [`no-useless-constructor`](https://eslint.org/docs/rules/no-useless-constructor)

    ```javascript
    // bad
    class Jedi {
      constructor() {}

      getName() {
        return this.name;
      }
    }

    // bad
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
      }
    }

    // good
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
        this.name = 'Rey';
      }
    }
    ```

  <a name="classes--no-duplicate-members"></a>
  - [9.6](#classes--no-duplicate-members) 중복되는 클래스 멤버를 만들지 마세요. eslint: [`no-dupe-class-members`](https://eslint.org/docs/rules/no-dupe-class-members)

    > 왜? 중복된 클래스 멤버를 선언하면 암묵적으로 마지막 멤버가 적용됩니다. 중복은 확실히 버그입니다.

    ```javascript
    // bad
    class Foo {
      bar() { return 1; }
      bar() { return 2; }
    }

    // good
    class Foo {
      bar() { return 1; }
    }

    // good
    class Foo {
      bar() { return 2; }
    }
    ```

  <a name="classes--methods-use-this"></a>
  - [9.7](#classes--methods-use-this) 클래스 메소드는 외부 라이브러리나 프레임워크가 구체적으로 비정적 메소드를 요구하지 않는 이상 `this`를 사용하거나 해당 메소드를 정적 메소드로 만들어야 합니다. 인스턴스 메서드는 수신자의 속성에 따라 다르게 동작함을 나타내야 합니다. eslint: [`class-methods-use-this`](https://eslint.org/docs/rules/class-methods-use-this)

    ```javascript
    // bad
    class Foo {
      bar() {
        console.log('bar');
      }
    }

    // good - this를 사용했습니다
    class Foo {
      bar() {
        console.log(this.bar);
      }
    }

    // good - constructor가 면제됩니다
    class Foo {
      constructor() {
        // ...
      }
    }

    // good - 정적 메소드는 this를 사용하지 않는다고 예상할 수 있습니다
    class Foo {
      static bar() {
        console.log('bar');
      }
    }
    ```    

**[⬆ back to top](#목차)**

## 모듈 (Modules)

  <a name="modules--use-them"></a><a name="10.1"></a>
  - [10.1](#modules--use-them) 항상 모듈(`import`/`export`)을 비표준 모듈 체계 대신 사용하세요. 언제든 선호하는 모듈 시스템으로 트랜스파일할 수 있습니다.

    > 왜? 모듈은 미래입니다. 지금 이 미래를 사용해 봅시다.

    ```javascript
    // bad
    const AirbnbStyleGuide = require('./AirbnbStyleGuide');
    module.exports = AirbnbStyleGuide.es6;

    // ok
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    export default AirbnbStyleGuide.es6;

    // best
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-wildcard"></a><a name="10.2"></a>
  - [10.2](#modules--no-wildcard) 와일드카드 import는 사용하지 마세요.

    > 왜? single default export임을 확실히 할 수 있습니다.

    ```javascript
    // bad
    import * as AirbnbStyleGuide from './AirbnbStyleGuide';

    // good
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    ```

  <a name="modules--no-export-from-import"></a><a name="10.3"></a>
  - [10.3](#modules--no-export-from-import) import문으로부터 직접 export하지 마세요.

    > 왜? 한줄이 간결하기는 하지만, 명확한 import와 명확한 export를 통해 일관성을 가질 수 있기 때문입니다.

    ```javascript
    // bad
    // filename es6.js
    export { es6 as default } from './AirbnbStyleGuide';

    // good
    // filename es6.js
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-duplicate-imports"></a>
  - [10.4](#modules--no-duplicate-imports) 같은 경로는 한 곳에서 import하세요.
 eslint: [`no-duplicate-imports`](https://eslint.org/docs/rules/no-duplicate-imports)

    > 왜? 같은 경로에서 import하는 여러 줄의 코드는 유지보수를 어렵게 만듭니다.

    ```javascript
    // bad
    import foo from 'foo';
    // … 또 다른 imports … //
    import { named1, named2 } from 'foo';

    // good
    import foo, { named1, named2 } from 'foo';

    // good
    import foo, {
      named1,
      named2,
    } from 'foo';
    ```

  <a name="modules--no-mutable-exports"></a>
  - [10.5](#modules--no-mutable-exports) 가변 바인딩을 export하지 마세요.
 eslint: [`import/no-mutable-exports`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-mutable-exports.md)

    > 왜? 변조는 일반적으로 피해야 하지만, 가변 바인딩을 export할 때는 특히 그렇습니다. 이 기술이 어떤 특별한 상황에 필요할 수도 있지만, 일반적으로는 상수 참조만 export되어야 합니다.

    ```javascript
    // bad
    let foo = 3;
    export { foo };

    // good
    const foo = 3;
    export { foo };
    ```

  <a name="modules--prefer-default-export"></a>
  - [10.6](#modules--prefer-default-export) 한가지만 export하는 모듈에서는 이름 붙여진 export보다는 default export를 사용하세요.
 eslint: [`import/prefer-default-export`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/prefer-default-export.md)

    > 왜? 하나만 export하는 파일의 가독성과 유지보수성이 더 좋기 때문입니다.

    ```javascript
    // bad
    export function foo() {}

    // good
    export default function foo() {}
    ```

   <a name="modules--imports-first"></a>
  - [10.7](#modules--imports-first) 모든 `import`구문을 다른 구문들 위에 두세요.
 eslint: [`import/first`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/first.md)

    > 왜? `import`구문은 호이스트되기 때문에 이것을 가장 위에 두면 예상치 못한 결과를 막을 수 있습니다.

    ```javascript
    // bad
    import foo from 'foo';
    foo.init();

    import bar from 'bar';

    // good
    import foo from 'foo';
    import bar from 'bar';

    foo.init();
    ```

  <a name="modules--multiline-imports-over-newlines"></a>
  - [10.8](#modules--multiline-imports-over-newlines) 여러 줄에 걸친 import는 여러 줄의 배열이나 객체 리터럴처럼 들여쓰기하세요. eslint: [`object-curly-newline`](https://eslint.org/docs/rules/object-curly-newline)

    > 왜? 스타일 가이드에 있는 다른 모든 중괄호 블록들 처럼 중괄호는 같은 들여쓰기 규칙을 따릅니다. 콤마가 그렇듯이 말이죠.

    ```javascript
    // bad
    import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';

    // good
    import {
      longNameA,
      longNameB,
      longNameC,
      longNameD,
      longNameE,
    } from 'path';
    ```

  <a name="modules--no-webpack-loader-syntax"></a>
  - [10.9](#modules--no-webpack-loader-syntax) 모듈 import 구문에서 Webpack loader 구문을 사용하지 마세요.
 eslint: [`import/no-webpack-loader-syntax`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-webpack-loader-syntax.md)

    > 왜? import에서 Webpack 구문을 사용하면 이 코드가 모듈 번들러에 연결되기 때문입니다. loader 구문은 `webpack.config.js`에서 사용하세요.

    ```javascript
    // bad
    import fooSass from 'css!sass!foo.scss';
    import barCss from 'style!css!bar.css';

    // good
    import fooSass from 'foo.scss';
    import barCss from 'bar.css';
    ```

  <a name="modules--import-extensions"></a>
  - [10.10](#modules--import-extensions) 자바스크립트 파일 확장자를 명시하지 마세요.
 eslint: [`import/extensions`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/extensions.md)

    > 왜? 확장자를 명시하면 모든 소비자에서 import하는 모듈의 세부적 구현을 부적절하게 하드코딩하고, 리팩토링을 막게 됩니다.

    ```javascript
    // bad
    import foo from './foo.js';
    import bar from './bar.jsx';
    import baz from './baz/index.jsx';

    // good
    import foo from './foo';
    import bar from './bar';
    import baz from './baz';

**[⬆ back to top](#목차)**

## 이터레이터와 제너레이터 (Iterators and Generators)

  <a name="iterators--nope"></a><a name="11.1"></a>
  - [11.1](#iterators--nope) 이터레이터를 사용하지 마세요. `for-in`이나 `for-of`같은 루프 대신 자바스크립트의 고급함수를 사용하세요. eslint: [`no-iterator`](https://eslint.org/docs/rules/no-iterator.html) [`no-restricted-syntax`](https://eslint.org/docs/rules/no-restricted-syntax)

    > 왜? 고급함수는 불변 규칙을 적용합니다. 사이드 이펙트에 대해 추측하는 것보다 값을 반환하는 순수 함수를 다루는 것이 더 간단합니다.

    > 배열을 이터레이트할 때 `map()` / `every()` / `filter()` / `find()` / `findIndex()` / `reduce()` / `some()` / ... 를 사용하세요. 배열을 생성할 때는 `Object.keys()` / `Object.values()` / `Object.entries()`를 사용해서 모든 객체를 이터레이트 할 수 있습니다. 

    ```javascript
    const numbers = [1, 2, 3, 4, 5];

    // bad
    let sum = 0;
    for (let num of numbers) {
      sum += num;
    }
    sum === 15;

    // good
    let sum = 0;
    numbers.forEach((num) => {
      sum += num;
    });
    sum === 15;

    // best (use the functional force)
    const sum = numbers.reduce((total, num) => total + num, 0);
    sum === 15;

    // bad
    const increasedByOne = [];
    for (let i = 0; i < numbers.length; i++) {
      increasedByOne.push(numbers[i] + 1);
    }

    // good
    const increasedByOne = [];
    numbers.forEach((num) => {
      increasedByOne.push(num + 1);
    });

    // best (keeping it functional)
    const increasedByOne = numbers.map(num => num + 1);
    ```

  <a name="generators--nope"></a><a name="11.2"></a>
  - [11.2](#generators--nope) 지금은 제너레이터를 사용하지 마세요.

    > 왜? ES5로 잘 트랜스파일되지 않기 때문입니다.

  <a name="generators--spacing"></a>
  - [11.3](#generators--spacing) 만약 반드시 제너레이터를 사용해야 하거나 [우리의 조언](#generators--nope)을 무시하는 경우, 함수 시그니처의 공백이 적절한지 확인하세요. eslint: [`generator-star-spacing`](https://eslint.org/docs/rules/generator-star-spacing)

    > 왜? `function`과 `*`는 같은 개념의 키워드입니다. - `*`은 `function`, `function*`의 제어자가 아니며, 이들은 `function`과 다른 고유한 구조입니다.

    ```javascript
    // bad
    function * foo() {
      // ...
    }

    // bad
    const bar = function * () {
      // ...
    };

    // bad
    const baz = function *() {
      // ...
    };

    // bad
    const quux = function*() {
      // ...
    };

    // bad
    function*foo() {
      // ...
    }

    // bad
    function *foo() {
      // ...
    }

    // very bad
    function
    *
    foo() {
      // ...
    }

    // very bad
    const wat = function
    *
    () {
      // ...
    };

    // good
    function* foo() {
      // ...
    }

    // good
    const foo = function* () {
      // ...
    };
    ```

**[⬆ back to top](#목차)**

## 속성 (Properties)

  <a name="properties--dot"></a><a name="12.1"></a>
  - [12.1](#properties--dot) 속성에 접근할 때는 마침표를 사용하세요. eslint: [`dot-notation`](https://eslint.org/docs/rules/dot-notation.html)

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    // bad
    const isJedi = luke['jedi'];

    // good
    const isJedi = luke.jedi;
    ```

  <a name="properties--bracket"></a><a name="12.2"></a>
  - [12.2](#properties--bracket) 변수를 사용해 속성에 접근할 때는 대괄호 `[]`를 사용하세요.

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    function getProp(prop) {
      return luke[prop];
    }

    const isJedi = getProp('jedi');
    ```

  <a name="es2016-properties--exponentiation-operator"></a>
  - [12.3](#es2016-properties--exponentiation-operator) 제곱 계산을 할 때는 제곱 연산자 `**`을 사용하세요. eslint: [`no-restricted-properties`](https://eslint.org/docs/rules/no-restricted-properties).

    ```javascript
    // bad
    const binary = Math.pow(2, 10);

    // good
    const binary = 2 ** 10;
    ```

**[⬆ back to top](#목차)**

## 변수 (Variables)

  <a name="variables--const"></a><a name="13.1"></a>
  - [13.1](#variables--const) 변수를 선언할 때는 항상 `const`나 `let`을 사용하세요. 이렇게 하지 않으면 전역 변수로 선언됩니다. 우리는 전역 네임스페이스를 오염시키지 않기를 바랍니다. Captain Planet이 우리에게 경고했어요. eslint: [`no-undef`](https://eslint.org/docs/rules/no-undef) [`prefer-const`](https://eslint.org/docs/rules/prefer-const)

    ```javascript
    // bad
    superPower = new SuperPower();

    // good
    const superPower = new SuperPower();
    ```

  <a name="variables--one-const"></a><a name="13.2"></a>
  - [13.2](#variables--one-const) 하나의 변수 선언/할당에는 하나의 `const` 또는 `let`을 사용하세요. eslint: [`one-var`](https://eslint.org/docs/rules/one-var.html)

    > 왜? 이렇게 하면 쉽게 새로운 변수를 추가할 수 있고, `,`를 `;`로 바꿔버리는 것에 대해 걱정할 필요가 없습니다. 또한 한번에 모든 선언을 건너뛰는 대신 디버거를 사용해 각 선언을 단계별로 살펴볼 수 있습니다.

    ```javascript
    // bad
    const items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

    // bad
    // (위 코드와 비교해 실수를 짚어보세요)
    const items = getItems(),
        goSportsTeam = true;
        dragonball = 'z';

    // good
    const items = getItems();
    const goSportsTeam = true;
    const dragonball = 'z';
    ```

  <a name="variables--const-let-group"></a><a name="13.3"></a>
  - [13.3](#variables--const-let-group) `const`를 그룹화한 다음에 `let`을 그룹화 하세요.

    > 왜? 이전에 할당한 변수에 대해 새 변수를 추가하는 경우 유용하기 때문입니다.

    ```javascript
    // bad
    let i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // bad
    let i;
    const items = getItems();
    let dragonball;
    const goSportsTeam = true;
    let len;

    // good
    const goSportsTeam = true;
    const items = getItems();
    let dragonball;
    let i;
    let length;
    ```

  <a name="variables--define-where-used"></a><a name="13.4"></a>
  - [13.4](#variables--define-where-used) 필요한 곳에서 변수를 할당하되, 합당한 곳에 두세요.

    > 왜? `let`과 `const`는 블록스코프이기 때문입니다. 함수스코프가 아닙니다.

    ```javascript
    // bad - unnecessary function call
    function checkName(hasName) {
      const name = getName();

      if (hasName === 'test') {
        return false;
      }

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }

    // good
    function checkName(hasName) {
      if (hasName === 'test') {
        return false;
      }

      const name = getName();

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }
    ```

  <a name="variables--no-chain-assignment"></a><a name="13.5"></a>
  - [13.5](#variables--no-chain-assignment) 변수 할당 체이닝을 하지 마세요. eslint: [`no-multi-assign`](https://eslint.org/docs/rules/no-multi-assign)

    > 왜? 변수 할당 체이닝은 암시적인 전역 변수를 만들기 때문입니다.

    ```javascript
    // bad
    (function example() {
      // 자바스크립트는 이것을
      // let a = ( b = ( c = 1 ) );
      // 로 해석합니다.
      // let 키워드는 변수 a에만 적용됩니다.
      // 변수 b와 c는 전역 변수가 됩니다.
      let a = b = c = 1;
    }());

    console.log(a); // throws ReferenceError
    console.log(b); // 1
    console.log(c); // 1

    // good
    (function example() {
      let a = 1;
      let b = a;
      let c = a;
    }());

    console.log(a); // throws ReferenceError
    console.log(b); // throws ReferenceError
    console.log(c); // throws ReferenceError

    // `const`에도 동일하게 적용됩니다
    ```

  <a name="variables--unary-increment-decrement"></a><a name="13.6"></a>
  - [13.6](#variables--unary-increment-decrement) 단항 증감 연산자(`++`, `--`)를 사용하지 마세요. eslint [`no-plusplus`](https://eslint.org/docs/rules/no-plusplus)

    > 왜? eslint 문서에 따르면, 단항 증감 구문은 자동으로 세미콜론을 삽입하며, 어플리케이션에서 값을 증감할 때 오류를 일으킬 수 있습니다. 또한 `num += 1`과 같은 구문을 통해 값을 변경하는 것이 `num++`이나 `num ++`와 같은 구문을 사용하는 것보다 더 의미있는 일이라고 생각합니다. 단항 증감 구문을 사용하지 않으면 프로그램에서 예기치 않은 동작을 일으키는 전위 증감 연산을 막을 수 있습니다.

    ```javascript
    // bad

    const array = [1, 2, 3];
    let num = 1;
    num++;
    --num;

    let sum = 0;
    let truthyCount = 0;
    for (let i = 0; i < array.length; i++) {
      let value = array[i];
      sum += value;
      if (value) {
        truthyCount++;
      }
    }

    // good

    const array = [1, 2, 3];
    let num = 1;
    num += 1;
    num -= 1;

    const sum = array.reduce((a, b) => a + b, 0);
    const truthyCount = array.filter(Boolean).length;
    ```

  <a name="variables--linebreak"></a>
  - [13.7](#variables--linebreak) 값을 할당할 때 `=`의 앞 또는 뒤에서 줄바꿈을 하지 마세요. 만약 할당이 [`max-len`](https://eslint.org/docs/rules/max-len.html)을 넘기는 경우, 값을 괄호로 둘러싸세요. eslint [`operator-linebreak`](https://eslint.org/docs/rules/operator-linebreak.html).

    > 왜? `=` 주위에서 줄바꿈을 하는 것은 할당 값을 모호하게 합니다.

    ```javascript
    // bad
    const foo =
      superLongLongLongLongLongLongLongLongFunctionName();

    // bad
    const foo
      = 'superLongLongLongLongLongLongLongLongString';

    // good
    const foo = (
      superLongLongLongLongLongLongLongLongFunctionName()
    );

    // good
    const foo = 'superLongLongLongLongLongLongLongLongString';
    ```

<a name="variables--no-unused-vars"></a>
- [13.8](#variables--no-unused-vars) 사용하지 않는 변수를 남겨두지 마세요. eslint: [`no-unused-vars`](https://eslint.org/docs/rules/no-unused-vars)

    > 왜? 선언되었지만 사용되지 않는 변수는 완벽하지 않은 리팩토링으로 인한 에러일 수 있습니다. 그런 변수는 코드의 자리를 차지하며, 읽는 사람이 혼란에 빠지도록 만듭니다.

    ```javascript
    // bad

    var some_unused_var = 42;

    // 쓰기 전용 변수는 사용한 것으로 간주되지 않습니다.
    var y = 10;
    y = 5;

    // 자신의 변경을 읽는 것은 사용한 것으로 간주되지 않습니다.
    var z = 0;
    z = z + 1;

    // 사용되지 않은 함수 인자.
    function getX(x, y) {
        return x;
    }

    // good

    function getXPlusY(x, y) {
      return x + y;
    }

    var x = 1;
    var y = a + 2;

    alert(getXPlusY(x, y));

    // 'type'은 사용되지 않을 경우 무시됩니다. 나머지 속성의 형제이기 때문입니다.
    // 이것은 특정 키를 생략하는 객체를 추출하는 형식입니다.
    var { type, ...coords } = data;
    // 'coords'는 이제 'data' 객체에서 'type' 속성이 빠진 'data' 객체입니다.
    ```

**[⬆ back to top](#목차)**

## 호이스팅 (Hoisting)

  <a name="hoisting--about"></a><a name="14.1"></a>
  - [14.1](#hoisting--about) `var` 선언은 할당없이 가장 가까운 함수 스코프의 꼭대기에 호이스트됩니다. `const`와 `let` 선언은 [Temporal Dead Zones (TDZ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_Dead_Zone)라고 불리는 새로운 개념의 혜택을 받습니다. [왜 typeof는 더 이상 안전하지 않은가](https://web.archive.org/web/20200121061528/http://es-discourse.com/t/why-typeof-is-no-longer-safe/15)에 대해서 알고있는 것이 중요합니다.

    ```javascript
    // (전역 변수 notDefined가 존재하지 않는다고 판정한 경우)
    // 동작하지 않습니다
    function example() {
      console.log(notDefined); // => throws a ReferenceError
    }

    // 그 변수를 참조하는 코드의 뒤에서 그 변수를 선언한 경우
    // 변수가 호이스트된 상태에서 동작합니다.
    // 주의：`true` 라는 값 자체는 호이스트되지 않습니다.
    function example() {
      console.log(declaredButNotAssigned); // => undefined
      var declaredButNotAssigned = true;
    }

    // 인터프리터는 변수선언을 스코프의 선두에 호이스트합니다
    // 위의 예는 다음과 같이 다시 쓸수 있습니다:
    function example() {
      let declaredButNotAssigned;
      console.log(declaredButNotAssigned); // => undefined
      declaredButNotAssigned = true;
    }

    // const와 let을 이용한 경우
    function example() {
      console.log(declaredButNotAssigned); // => throws a ReferenceError
      console.log(typeof declaredButNotAssigned); // => throws a ReferenceError
      const declaredButNotAssigned = true;
    }
    ```

  <a name="hoisting--anon-expressions"></a><a name="14.2"></a>
  - [14.2](#hoisting--anon-expressions) 익명함수의 경우 함수가 할당되기 전의 변수가 호이스트됩니다.

    ```javascript
    function example() {
      console.log(anonymous); // => undefined

      anonymous(); // => TypeError anonymous is not a function

      var anonymous = function () {
        console.log('anonymous function expression');
      };
    }
    ```

  <a name="hoisting--named-expresions"></a><a name="hoisting--named-expressions"></a><a name="14.3"></a>
  - [14.3](#hoisting--named-expressions) 명명함수의 경우에도 똑같이 변수가 호이스트됩니다. 함수의 이름이나 본체는 호이스트되지 않습니다. 

    ```javascript
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      superPower(); // => ReferenceError superPower is not defined

      var named = function superPower() {
        console.log('Flying');
      };
    }

    // 함수 이름이 변수 이름과 동일할 때도 마찬가지다.
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      var named = function named() {
        console.log('named');
      };
    }
    ```

  <a name="hoisting--declarations"></a><a name="14.4"></a>
  - [14.4](#hoisting--declarations) 함수선언은 함수명과 함수본체가 호이스트됩니다.

    ```javascript
    function example() {
      superPower(); // => Flying

      function superPower() {
        console.log('Flying');
      }
    }
    ```

  - 더 자세한 정보는 이곳을 참고해주세요 [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting/) by [Ben Cherry](http://www.adequatelygood.com/).

**[⬆ back to top](#목차)**

## 비교 연산자 (Comparison Operators & Equality)

  <a name="comparison--eqeqeq"></a><a name="15.1"></a>
  - [15.1](#comparison--eqeqeq) `==`와 `!=` 대신 `===`와 `!==`를 사용하세요. eslint: [`eqeqeq`](https://eslint.org/docs/rules/eqeqeq.html)

  <a name="comparison--if"></a><a name="15.2"></a>
  - [15.2](#comparison--if) `if`문과 같은 조건식은 `ToBoolean` 메소드에 의한 강제형변환으로 평가되어 항상 다음과 같은 간단한 규칙을 따릅니다:

    - **Objects**는 **true**로 평가됩니다.
    - **Undefined**는 **false**로 평가됩니다.
    - **Null**는 **false**로 평가됩니다.
    - **Booleans**는 **boolean형의 값**으로 평가됩니다.
    - **Numbers**는 **true**로 평가됩니다. 하지만 **+0, -0, NaN**의 경우 **false**로 평가됩니다. 
    - **Strings**는 **true**로 평가됩니다. 하지만 빈 문자열 `''`은, **false**로 평가됩니다.

    ```javascript
    if ([0] && []) {
      // true
      // 배열(빈 배열 포함)은 객체이며, 객체는 참으로 평가됩니다.
    }
    ```

  <a name="comparison--shortcuts"></a><a name="15.3"></a>
  - [15.3](#comparison--shortcuts) 불리언 비교에는 단축형을 사용하세요. 단, 숫자나 문자열은 명시적으로 비교하세요.

    ```javascript
    // bad
    if (isValid === true) {
      // ...
    }

    // good
    if (isValid) {
      // ...
    }

    // bad
    if (name) {
      // ...
    }

    // good
    if (name !== '') {
      // ...
    }

    // bad
    if (collection.length) {
      // ...
    }

    // good
    if (collection.length > 0) {
      // ...
    }
    ```

  <a name="comparison--moreinfo"></a><a name="15.4"></a>
  - [15.4](#comparison--moreinfo) 더 자세한 정보는 이곳을 참고해주세요. [Truth Equality and JavaScript](https://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) by Angus Croll.

  <a name="comparison--switch-blocks"></a><a name="15.5"></a>
  - [15.5](#comparison--switch-blocks) 렉시컬 선언 (e.g. `let`, `const`, `function`, and `class`)을 포함하는 `case`와 `default` 구문 안에 블록을 만들 때는 괄호를 사용하세요. eslint: [`no-case-declarations`](https://eslint.org/docs/rules/no-case-declarations.html)

    > 왜? 렉시컬 선언은 `switch` 블록 전체에서 접근할 수 있지만, 할당된 경우에만 초기화됩니다. `case`에 다다랐을 때 말이죠. 이것은 여러 `case` 구문이 같은 것을 정의하려 할 때 문제를 일으킵니다. 

    ```javascript
    // bad
    switch (foo) {
      case 1:
        let x = 1;
        break;
      case 2:
        const y = 2;
        break;
      case 3:
        function f() {
          // ...
        }
        break;
      default:
        class C {}
    }

    // good
    switch (foo) {
      case 1: {
        let x = 1;
        break;
      }
      case 2: {
        const y = 2;
        break;
      }
      case 3: {
        function f() {
          // ...
        }
        break;
      }
      case 4:
        bar();
        break;
      default: {
        class C {}
      }
    }
    ```

  <a name="comparison--nested-ternaries"></a><a name="15.6"></a>
  - [15.6](#comparison--nested-ternaries) 삼항 연산자를 중첩해서는 안되며, 일반적으로 한줄에 표현해야 합니다. eslint: [`no-nested-ternary`](https://eslint.org/docs/rules/no-nested-ternary.html)

    ```javascript
    // bad
    const foo = maybe1 > maybe2
      ? "bar"
      : value1 > value2 ? "baz" : null;

    // split into 2 separated ternary expressions
    const maybeNull = value1 > value2 ? 'baz' : null;

    // better
    const foo = maybe1 > maybe2
      ? 'bar'
      : maybeNull;

    // best
    const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
    ```

  <a name="comparison--unneeded-ternary"></a><a name="15.7"></a>
  - [15.7](#comparison--unneeded-ternary) 불필요한 삼항 연산자를 사용하지 마세요. eslint: [`no-unneeded-ternary`](https://eslint.org/docs/rules/no-unneeded-ternary.html)

    ```javascript
    // bad
    const foo = a ? a : b;
    const bar = c ? true : false;
    const baz = c ? false : true;

    // good
    const foo = a || b;
    const bar = !!c;
    const baz = !c;
    ```

  <a name="comparison--no-mixed-operators"></a>
  - [15.8](#comparison--no-mixed-operators) 연산자를 섞어 사용할 때 해당 연산자들을 괄호로 둘러싸세요. 유일한 예외는 산술 연산자 (`+`, `-`, `**`)입니다. 이들의 우선순위는 상식적으로 이해할 수 있습니다. `/`와 `*`은 섞일 경우 순서가 모호할 수 있으므로 괄호로 감싸는 것을 추천합니다. eslint: [`no-mixed-operators`](https://eslint.org/docs/rules/no-mixed-operators.html)

    > 왜? 이렇게 하면 코드가 더 읽기 쉬워지며, 개발자의 의도가 명확해집니다.

    ```javascript
    // bad
    const foo = a && b < 0 || c > 0 || d + 1 === 0;

    // bad
    const bar = a ** b - 5 % d;

    // bad
    // (a || b) && c 으로 혼동할 수 있습니다.
    if (a || b && c) {
      return d;
    }

    // good
    const foo = (a && b < 0) || c > 0 || (d + 1 === 0);

    // good
    const bar = (a ** b) - (5 % d);

    // good
    if (a || (b && c)) {
      return d;
    }

    // good
    const bar = a + b / c * d;
    ```

**[⬆ back to top](#목차)**

## 블록 (Blocks)

  <a name="blocks--braces"></a><a name="16.1"></a>
  - [16.1](#blocks--braces) 여러 줄의 블록에는 중괄호를 사용하세요. eslint: [`nonblock-statement-body-position`](https://eslint.org/docs/rules/nonblock-statement-body-position)

    ```javascript
    // bad
    if (test)
      return false;

    // good
    if (test) return false;

    // good
    if (test) {
      return false;
    }

    // bad
    function foo() { return false; }

    // good
    function bar() {
      return false;
    }
    ```

  <a name="blocks--cuddled-elses"></a><a name="16.2"></a>
  - [16.2](#blocks--cuddled-elses) 여러 줄의 `if`와 `else`문을 사용할 때는 `else`를 `if` 블록의 닫는 중괄호와 같은 줄에 두세요. eslint: [`brace-style`](https://eslint.org/docs/rules/brace-style.html)

    ```javascript
    // bad
    if (test) {
      thing1();
      thing2();
    }
    else {
      thing3();
    }

    // good
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```

  <a name="blocks--no-else-return"></a><a name="16.3"></a>
  - [16.3](#blocks--no-else-return) 만약 `if` 블록이 항상 `return` 구문을 실행시킨다면, `else` 블록은 불필요합니다. `return`을 포함한 `if`블록을 잇는 `else if` 블록 안에 `return` 구문이 있으면 여러 `if` 블록으로 나눠질 수 있습니다. eslint: [`no-else-return`](https://eslint.org/docs/rules/no-else-return)

    ```javascript
    // bad
    function foo() {
      if (x) {
        return x;
      } else {
        return y;
      }
    }

    // bad
    function cats() {
      if (x) {
        return x;
      } else if (y) {
        return y;
      }
    }

    // bad
    function dogs() {
      if (x) {
        return x;
      } else {
        if (y) {
          return y;
        }
      }
    }

    // good
    function foo() {
      if (x) {
        return x;
      }

      return y;
    }

    // good
    function cats() {
      if (x) {
        return x;
      }

      if (y) {
        return y;
      }
    }

    // good
    function dogs(x) {
      if (x) {
        if (z) {
          return y;
        }
      } else {
        return z;
      }
    }
    ```

**[⬆ back to top](#목차)**

## 제어문 (Control Statements)

  <a name="control-statements"></a>
  - [17.1](#control-statements) 제어문 (`if`, `while` 등)이 너무 길거나 최대 길이를 넘긴 경우, 각 조건을 새로운 줄에 두세요. 논리 연산자는 줄의 시작부분에 있어야 합니다.

    > 왜? 줄의 맨 처음에 연산자를 두면 연산자의 정렬을 유지하고, 메소드 체이닝과 비슷한 패턴을 따를 수 있습니다. 또, 이렇게 하면 복잡한 로직을 쉽게 볼 수 있도록 만들어 가독성을 높입니다.

    ```javascript
    // bad
    if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
      thing1();
    }

    // bad
    if (foo === 123 &&
      bar === 'abc') {
      thing1();
    }

    // bad
    if (foo === 123
      && bar === 'abc') {
      thing1();
    }

    // bad
    if (
      foo === 123 &&
      bar === 'abc'
    ) {
      thing1();
    }

    // good
    if (
      foo === 123
      && bar === 'abc'
    ) {
      thing1();
    }

    // good
    if (
      (foo === 123 || bar === 'abc')
      && doesItLookGoodWhenItBecomesThatLong()
      && isThisReallyHappening()
    ) {
      thing1();
    }

    // good
    if (foo === 123 && bar === 'abc') {
      thing1();
    }
    ```

  <a name="control-statement--value-selection"></a>
  - [17.2](#control-statements--value-selection). 선택 연산자를 제어 구문 대신 쓰지 마세요.

    ```javascript
    // bad
    !isRunning && startRunning();

    // good
    if (!isRunning) {
      startRunning();
    }
    ```

**[⬆ back to top](#목차)**

## 주석 (Comments)

  <a name="comments--multiline"></a><a name="17.1"></a>
  - [18.1](#comments--multiline) 여러 줄에 걸친 주석을 쓸 때는 `/** ... */`을 사용하세요.

    ```javascript
    // bad
    // make()는 전달된 태그명을 기반으로
    // 새로운 요소를 반환한다. 
    //
    // @param {String} tag
    // @return {Element} element
    function make(tag) {

      // ...

      return element;
    }

    // good
    /**
     * make()는 전달된 태그명을 기반으로
     * 새로운 요소를 반환한다.
     */
    function make(tag) {

      // ...

      return element;
    }
    ```

  <a name="comments--singleline"></a><a name="17.2"></a>
  - [18.2](#comments--singleline) 한줄 주석을 쓸 때는 `//`을 사용하세요. 주석 전에는 빈 행을 넣어주세요.

    ```javascript
    // bad
    const active = true;  // is current tab

    // good
    // is current tab
    const active = true;

    // bad
    function getType() {
      console.log('fetching type...');
      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }

    // good
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }

    // also good
    function getType() {
      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }
    ```

  <a name="comments--spaces"></a>
  - [18.3](#comments--spaces) 모든 주석은 공백으로 시작해야 합니다. eslint: [`spaced-comment`](https://eslint.org/docs/rules/spaced-comment)

    ```javascript
    // bad
    //is current tab
    const active = true;

    // good
    // is current tab
    const active = true;

    // bad
    /**
     *make()는 전달된 태그명을 기반으로
     *새로운 요소를 반환한다.
     */
    function make(tag) {

      // ...

      return element;
    }

    // good
    /**
     * make()는 전달된 태그명을 기반으로
     * 새로운 요소를 반환한다.
     */
    function make(tag) {

      // ...

      return element;
    }
    ```

  <a name="comments--actionitems"></a><a name="17.3"></a>
  - [18.4](#comments--actionitems) 문제를 지적하고 재고를 촉구하는 경우나 문제의 해결책을 제안하는 경우 등에는 주석 앞에 `FIXME` 나 `TODO` 를 붙임으로써 다른 개발자의 빠른 이해를 도울수 있습니다. 이런 것들은 어떤 행동을 따른다는 의미로 통상의 주석와는 다릅니다. 행동이라는 것은 `FIXME -- 해결이 필요` 또는 `TODO -- 구현이 필요` 를 뜻합니다.

  <a name="comments--fixme"></a><a name="17.4"></a>
  - [18.5](#comments--fixme) 문제에 대한 주석으로 `// FIXME:`를 사용하세요.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // FIXME: 전역 변수를 사용해서는 안 됨
        total = 0;
      }
    }
    ```

  <a name="comments--todo"></a><a name="17.5"></a>
  - [18.6](#comments--todo) 문제의 해결책에 대한 주석으로 `// TODO:`를 사용하세요.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // TODO: total은 옵션 파라메터로 설정해야함
        this.total = 0;
      }
    }
    ```

**[⬆ back to top](#목차)**

## 공백 (Whitespace)

  <a name="whitespace--spaces"></a><a name="18.1"></a>
  - [19.1](#whitespace--spaces) 탭은 공백문자 2개로 설정하세요. eslint: [`indent`](https://eslint.org/docs/rules/indent.html)

    ```javascript
    // bad
    function foo() {
    ∙∙∙∙let name;
    }

    // bad
    function bar() {
    ∙let name;
    }

    // good
    function baz() {
    ∙∙let name;
    }
    ```

  <a name="whitespace--before-blocks"></a><a name="18.2"></a>
  - [19.2](#whitespace--before-blocks) 주요 중괄호 앞에는 공백을 1개 넣으세요. eslint: [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks.html)

    ```javascript
    // bad
    function test(){
      console.log('test');
    }

    // good
    function test() {
      console.log('test');
    }

    // bad
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });

    // good
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    ```

  <a name="whitespace--around-keywords"></a><a name="18.3"></a>
  - [19.3](#whitespace--around-keywords) 제어문 (`if`, `while` 등)의 소괄호 앞에는 공백을 1개 넣으세요. 함수선언이나 함수호출시 인자 리스트 앞에는 공백을 넣지 마세요. eslint: [`keyword-spacing`](https://eslint.org/docs/rules/keyword-spacing.html)

    ```javascript
    // bad
    if(isJedi) {
      fight ();
    }

    // good
    if (isJedi) {
      fight();
    }

    // bad
    function fight () {
      console.log ('Swooosh!');
    }

    // good
    function fight() {
      console.log('Swooosh!');
    }
    ```

  <a name="whitespace--infix-ops"></a><a name="18.4"></a>
  - [19.4](#whitespace--infix-ops) 연산자 사이에 공백을 넣으세요. eslint: [`space-infix-ops`](https://eslint.org/docs/rules/space-infix-ops.html)

    ```javascript
    // bad
    const x=y+5;

    // good
    const x = y + 5;
    ```

  <a name="whitespace--newline-at-end"></a><a name="18.5"></a>
  - [19.5](#whitespace--newline-at-end) 파일 끝에는 개행문자를 1개 넣으세요. eslint: [`eol-last`](https://github.com/eslint/eslint/blob/master/docs/rules/eol-last.md)  

    ```javascript
    // bad
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;
    ```

    ```javascript
    // bad
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;↵
    ↵
    ```

    ```javascript
    // good
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;↵
    ```

  <a name="whitespace--chains"></a><a name="18.6"></a>
  - [19.6](#whitespace--chains) 길게 메소드를 체이닝하는 경우 (2개 메소드 이상) 들여쓰기를 하세요. 또한 해당 줄이 새로운 구문이 아니라 메소드 호출임을 강조하는 마침표를 맨 앞에 두세요. eslint: [`newline-per-chained-call`](https://eslint.org/docs/rules/newline-per-chained-call) [`no-whitespace-before-property`](https://eslint.org/docs/rules/no-whitespace-before-property)

    ```javascript
    // bad
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // bad
    $('#items').
      find('.selected').
        highlight().
        end().
      find('.open').
        updateCount();

    // good
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();

    // bad
    const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
        .attr('width', (radius + margin) * 2).append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    // good
    const leds = stage.selectAll('.led')
        .data(data)
      .enter().append('svg:svg')
        .classed('led', true)
        .attr('width', (radius + margin) * 2)
      .append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    // good
    const leds = stage.selectAll('.led').data(data);
    ```

  <a name="whitespace--after-blocks"></a><a name="18.7"></a>
  - [19.7](#whitespace--after-blocks) 구문의 앞과 블록의 뒤에는 빈 행을 두세요.

    ```javascript
    // bad
    if (foo) {
      return bar;
    }
    return baz;

    // good
    if (foo) {
      return bar;
    }

    return baz;

    // bad
    const obj = {
      foo() {
      },
      bar() {
      },
    };
    return obj;

    // good
    const obj = {
      foo() {
      },

      bar() {
      },
    };

    return obj;

    // bad
    const arr = [
      function foo() {
      },
      function bar() {
      },
    ];
    return arr;

    // good
    const arr = [
      function foo() {
      },

      function bar() {
      },
    ];

    return arr;
    ```

  <a name="whitespace--padded-blocks"></a><a name="18.8"></a>
  - [19.8](#whitespace--padded-blocks) 블록에 빈 행을 끼워 넣지 마세요. eslint: [`padded-blocks`](https://eslint.org/docs/rules/padded-blocks.html)

    ```javascript
    // bad
    function bar() {

      console.log(foo);

    }

    // bad
    if (baz) {

      console.log(qux);
    } else {
      console.log(foo);

    }

    // bad
    class Foo {

      constructor(bar) {
        this.bar = bar;
      }
    }

    // good
    function bar() {
      console.log(foo);
    }

    // good
    if (baz) {
      console.log(qux);
    } else {
      console.log(foo);
    }
    ```

  <a name="whitespace--no-multiple-blanks"></a>
  - [19.9](#whitespace--no-multiple-blanks) 여러 빈 행을 두지 마세요. eslint: [`no-multiple-empty-lines`](https://eslint.org/docs/rules/no-multiple-empty-lines)

    <!-- markdownlint-disable MD012 -->
    ```javascript
    // bad
    class Person {
      constructor(fullName, email, birthday) {
        this.fullName = fullName;


        this.email = email;


        this.setAge(birthday);
      }


      setAge(birthday) {
        const today = new Date();


        const age = this.getAge(today, birthday);


        this.age = age;
      }


      getAge(today, birthday) {
        // ..
      }
    }

    // good
    class Person {
      constructor(fullName, email, birthday) {
        this.fullName = fullName;
        this.email = email;
        this.setAge(birthday);
      }

      setAge(birthday) {
        const today = new Date();
        const age = getAge(today, birthday);
        this.age = age;
      }

      getAge(today, birthday) {
        // ..
      }
    }
    ```

  <a name="whitespace--in-parens"></a><a name="18.9"></a>
  - [19.10](#whitespace--in-parens) 소괄호 안쪽에 공백을 두지 마세요. eslint: [`space-in-parens`](https://eslint.org/docs/rules/space-in-parens.html)

    ```javascript
    // bad
    function bar( foo ) {
      return foo;
    }

    // good
    function bar(foo) {
      return foo;
    }

    // bad
    if ( foo ) {
      console.log(foo);
    }

    // good
    if (foo) {
      console.log(foo);
    }
    ```

  <a name="whitespace--in-brackets"></a><a name="18.10"></a>
  - [19.11](#whitespace--in-brackets) 대괄호 안쪽에 공백을 두지 마세요. eslint: [`array-bracket-spacing`](https://eslint.org/docs/rules/array-bracket-spacing.html)

    ```javascript
    // bad
    const foo = [ 1, 2, 3 ];
    console.log(foo[ 0 ]);

    // good
    const foo = [1, 2, 3];
    console.log(foo[0]);
    ```

  <a name="whitespace--in-braces"></a><a name="18.11"></a>
  - [19.12](#whitespace--in-braces) 중괄호 안쪽에 공백을 두세요. eslint: [`object-curly-spacing`](https://eslint.org/docs/rules/object-curly-spacing.html)

    ```javascript
    // bad
    const foo = {clark: 'kent'};

    // good
    const foo = { clark: 'kent' };
    ```

  <a name="whitespace--max-len"></a><a name="18.12"></a>
  - [19.13](#whitespace--max-len) 한줄의 코드가 100자를 넘기는 것을 피하세요. (공백 포함) 주의: [앞의 규칙](#strings--line-length)에 따르면, 긴 문자열은 이 규칙에서 제외되며, 분리되어서는 안 됩니다. eslint: [`max-len`](https://eslint.org/docs/rules/max-len.html)

    > 왜? 가독성과 유지보수성을 보장해주기 때문입니다.

    ```javascript
    // bad
    const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

    // bad
    $.ajax({ method: 'POST', url: 'https://airbnb.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

    // good
    const foo = jsonData
      && jsonData.foo
      && jsonData.foo.bar
      && jsonData.foo.bar.baz
      && jsonData.foo.bar.baz.quux
      && jsonData.foo.bar.baz.quux.xyzzy;

    // good
    $.ajax({
      method: 'POST',
      url: 'https://airbnb.com/',
      data: { name: 'John' },
    })
      .done(() => console.log('Congratulations!'))
      .fail(() => console.log('You have failed this city.'));
    ```

    <a name="whitespace--block-spacing"></a>
  - [19.14](#whitespace--block-spacing) 여는 블록 토큰과 같은 행의 다음 토큰 내의 공백을 일관성있게 하세요. 이 규칙은 닫는 블록 토큰과 같은 행의 이전 토큰에도 적용됩니다. eslint: [`block-spacing`](https://eslint.org/docs/rules/block-spacing)

    ```javascript
    // bad
    function foo() {return true;}
    if (foo) { bar = 0;}

    // good
    function foo() { return true; }
    if (foo) { bar = 0; }
    ```

  <a name="whitespace--comma-spacing"></a>
  - [19.15](#whitespace--comma-spacing) 쉼표 이전에는 공백을 넣지 말고, 쉼표 이후에는 공백을 넣으세요. eslint: [`comma-spacing`](https://eslint.org/docs/rules/comma-spacing)

    ```javascript
    // bad
    var foo = 1,bar = 2;
    var arr = [1 , 2];

    // good
    var foo = 1, bar = 2;
    var arr = [1, 2];
    ```

  <a name="whitespace--computed-property-spacing"></a>
  - [19.16](#whitespace--computed-property-spacing) 계산된 속성 내에는 공백을 넣으세요. eslint: [`computed-property-spacing`](https://eslint.org/docs/rules/computed-property-spacing)

    ```javascript
    // bad
    obj[foo ]
    obj[ 'foo']
    var x = {[ b ]: a}
    obj[foo[ bar ]]

    // good
    obj[foo]
    obj['foo']
    var x = { [b]: a }
    obj[foo[bar]]
    ```

  <a name="whitespace--func-call-spacing"></a>
  - [19.17](#whitespace--func-call-spacing) 함수를 호출할 때는 공백을 넣지 마세요. eslint: [`func-call-spacing`](https://eslint.org/docs/rules/func-call-spacing)

    ```javascript
    // bad
    func ();

    func
    ();

    // good
    func();
    ```

    <a name="whitespace--key-spacing"></a>
  - [19.18](#whitespace--key-spacing) 객체 리터럴 속성의 키와 값 사이에는 공백을 넣으세요. eslint: [`key-spacing`](https://eslint.org/docs/rules/key-spacing)

    ```javascript
    // bad
    var obj = { foo : 42 };
    var obj2 = { foo:42 };

    // good
    var obj = { foo: 42 };
    ```

    <a name="whitespace--no-trailing-spaces"></a>
  - [19.19](#whitespace--no-trailing-spaces) 행의 마지막에 공백을 남겨두지 마세요. eslint: [`no-trailing-spaces`](https://eslint.org/docs/rules/no-trailing-spaces)

  <a name="whitespace--no-multiple-empty-lines"></a>
  - [19.20](#whitespace--no-multiple-empty-lines) 여러 빈 행을 쓰지 마세요. 단, 파일의 마지막 행에는 빈 행을 두세요. 파일의 시작에는 빈 행을 두지 마세요. eslint: [`no-multiple-empty-lines`](https://eslint.org/docs/rules/no-multiple-empty-lines)

    <!-- markdownlint-disable MD012 -->
    ```javascript
    // bad - 여러 개의 빈 줄
    var x = 1;


    var y = 2;

    // bad - 파일 끝에 2개 이상의 빈 줄
    var x = 1;
    var y = 2;


    // bad - 파일 시작에 1개 이상의 빈 줄 

    var x = 1;
    var y = 2;

    // good
    var x = 1;
    var y = 2;

    ```
    <!-- markdownlint-enable MD012 -->

**[⬆ back to top](#목차)**

## 쉼표 (Commas)

  <a name="commas--leading-trailing"></a><a name="19.1"></a>
  - [20.1](#commas--leading-trailing) 맨 앞의 쉼표: **안 됩니다.** eslint: [`comma-style`](https://eslint.org/docs/rules/comma-style.html)

    ```javascript
    // bad
    const story = [
        once
      , upon
      , aTime
    ];

    // good
    const story = [
      once,
      upon,
      aTime,
    ];

    // bad
    const hero = {
        firstName: 'Ada'
      , lastName: 'Lovelace'
      , birthYear: 1815
      , superPower: 'computers'
    };

    // good
    const hero = {
      firstName: 'Ada',
      lastName: 'Lovelace',
      birthYear: 1815,
      superPower: 'computers',
    };
    ```

  <a name="commas--dangling"></a><a name="19.2"></a>
  - [20.2](#commas--dangling) 끝의 쉼표: **좋아요.** eslint: [`comma-dangle`](https://eslint.org/docs/rules/comma-dangle.html)

    > 왜? 이것은 깨끗한 git의 diffs로 이어집니다. 또한 Babel과 같은 트랜스파일러는 트랜스파일하는 사이에 쓸데없는 끝의 쉼표를 제거합니다. 이것은 레거시 브라우저에서의 [불필요한 쉼표 문제](es5-deprecated/README.md#commas)를 고민할 필요가 없는 것을 의미합니다.

    ```diff
    // bad - 마지막에 쉼표가 없는 경우 git diff
    const hero = {
         firstName: 'Florence',
    -    lastName: 'Nightingale'
    +    lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing']
    };

    // good - 마지막에 쉼표가 있는 경우 git diff
    const hero = {
         firstName: 'Florence',
         lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing'],
    };
    ```

    ```javascript
    // bad
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully'
    };

    const heroes = [
      'Batman',
      'Superman'
    ];

    // good
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully',
    };

    const heroes = [
      'Batman',
      'Superman',
    ];

    // bad
    function createHero(
      firstName,
      lastName,
      inventorOf
    ) {
      // does nothing
    }

    // good
    function createHero(
      firstName,
      lastName,
      inventorOf,
    ) {
      // does nothing
    }

    // good ("나머지" 요소 뒤에 쉼표가 없다는 점에 주의하세요)
    function createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    ) {
      // does nothing
    }

    // bad
    createHero(
      firstName,
      lastName,
      inventorOf
    );

    // good
    createHero(
      firstName,
      lastName,
      inventorOf,
    );

    // good ("나머지" 요소 뒤에 쉼표가 없다는 점에 주의하세요)
    createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    );
    ```

**[⬆ back to top](#목차)**

## 세미콜론 (Semicolons)

  <a name="semicolons--required"></a><a name="20.1"></a>
  - [21.1](#semicolons--required) **씁시다.** eslint: [`semi`](https://eslint.org/docs/rules/semi.html)

    > 왜? 자바스크립트가 세미콜론이 없는 줄바꿈을 만났을 때, [자동 세미콜론 삽입](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion) 규칙에 따라 그 줄바꿈을 구문의 끝으로 간주할지 여부를 결정하고, (이름이 암시하듯) 세미콜론을 줄바꿈 이전에 삽입합니다. ASI는 몇가지 별난 동작을 포함하고 있지만, 만약 자바스크립트가 줄바꿈을 잘못 해석한다면 코드가 망가져버릴 것입니다. 이 규칙은 새로운 기능이 자바스크립트의 일부가 되면서 더 복잡해집니다. 구문의 끝을 명시하고, 빠뜨린 세미콜론을 잡도록 linter를 설정하면 문제가 발생하는 것을 막을 수 있습니다.

    ```javascript
    // bad - 예외 발생
    const luke = {}
    const leia = {}
    [luke, leia].forEach(jedi => jedi.father = 'vader')

    // bad - 예외 발생
    const reaction = "No! That's impossible!"
    (async function meanwhileOnTheFalcon() {
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }())

    // bad - returns `undefined` instead of the value on the next line - always happens when `return` is on a line by itself because of ASI!
    function foo() {
      return
        'search your feelings, you know it to be foo'
    }

    // good
    const luke = {};
    const leia = {};
    [luke, leia].forEach((jedi) => {
      jedi.father = 'vader';
    });

    // good
    const reaction = "No! That's impossible!";
    (async function meanwhileOnTheFalcon() {
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }());

    // good
    function foo() {
      return 'search your feelings, you know it to be foo';
    }
    ```

    [Read more](https://stackoverflow.com/questions/7365172/semicolon-before-self-invoking-function/7365214#7365214).

**[⬆ back to top](#목차)**

## 형변환과 강제 (Type Casting & Coercion)

  <a name="coercion--explicit"></a><a name="21.1"></a>
  - [22.1](#coercion--explicit) 구문의 선두에서 형을 강제합니다.

  <a name="coercion--strings"></a><a name="21.2"></a>
  - [22.2](#coercion--strings)  문자열: eslint: [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    ```javascript
    // => this.reviewScore = 9;

    // bad
    const totalScore = new String(this.reviewScore); // typeof totalScore is "object" not "string"

    // bad
    const totalScore = this.reviewScore + ''; // invokes this.reviewScore.valueOf()

    // bad
    const totalScore = this.reviewScore.toString(); // isn’t guaranteed to return a string

    // good
    const totalScore = String(this.reviewScore);
    ```

  <a name="coercion--numbers"></a><a name="21.3"></a>
  - [22.3](#coercion--numbers) 숫자: 형변환을 하는 경우 `Number`를 사용하고, 문자열을 파싱하는 경우에는 기수를 인자로 넘겨 `parseInt`를 사용하세요. eslint: [`radix`](https://eslint.org/docs/rules/radix) [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    > 왜? `parseInt` 함수는 특정 기수(radix)에 따른 문자열 인자의 내용을 해석하고, 이에 따라 판단되는 정수 값을 만듭니다. 이때 문자열 맨앞의 공백은 무시됩니다. 만약 기수가 `undefined` 또는 `0`이라면 `10`으로 취급되며, 숫자가 `0x` 또는 `0X` 문자로 시작하는 경우엔 16진수로 취급됩니다. ECMAScript 3와의 차이는 8진수 해석을 허용하는가에 있습니다. 많은 구현체들이 2013부터 이러한 동작을 채택하지 않았는데, 오래된 브라우저들을 지원해야 하므로 기수를 항상 명시해야 합니다.

    ```javascript
    const inputValue = '4';

    // bad
    const val = new Number(inputValue);

    // bad
    const val = +inputValue;

    // bad
    const val = inputValue >> 0;

    // bad
    const val = parseInt(inputValue);

    // good
    const val = Number(inputValue);

    // good
    const val = parseInt(inputValue, 10);
    ```

  <a name="coercion--comment-deviations"></a><a name="21.4"></a>
  - [22.4](#coercion--comment-deviations) 어떤 이유로 인해 `parseInt`가 병목현상을 일으켜 [성능적인 이유](https://jsperf.com/coercion-vs-casting/3)로 비트 시프트를 사용해야 하는 경우 하려고 했던 것을 왜(why)와 무엇(what)으로 설명해 주석으로 남겨주세요.  

    ```javascript
    // good
    /**
     * parseInt was the reason my code was slow.
     * Bitshifting the String to coerce it to a
     * Number made it a lot faster.
     * 코드가 느린 원인은 parseInt였음.
     * 비트 시프트를 통해 문자열을 강제 형변환하여
     * 성능을 개선시킴.
     */
    const val = inputValue >> 0;
    ```

  <a name="coercion--bitwise"></a><a name="21.5"></a>
  - [22.5](#coercion--bitwise) **주의:** 비트 연산자를 사용하는 경우. 숫자는 [64비트 값](https://es5.github.io/#x4.3.19)으로 표현되어 있으나, 비트 시프트 연산을 한 경우 32비트 정수로 넘겨집니다. ([소스](https://es5.github.io/#x11.7)). 32비트 이상의 정수를 비트 시프트하는 경우 예기치못한 현상을 야기할 수 있습니다. [토론](https://github.com/airbnb/javascript/issues/109). 부호가 포함된 32비트 정수의 최대치는 2,147,483,647입니다:

    ```javascript
    2147483647 >> 0; // => 2147483647
    2147483648 >> 0; // => -2147483648
    2147483649 >> 0; // => -2147483647
    ```

  <a name="coercion--booleans"></a><a name="21.6"></a>
  - [22.6](#coercion--booleans) 불리언: eslint: [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    ```javascript
    const age = 0;

    // bad
    const hasAge = new Boolean(age);

    // good
    const hasAge = Boolean(age);

    // best
    const hasAge = !!age;
    ```

**[⬆ back to top](#목차)**

## 명명규칙 (Naming Conventions)

  <a name="naming--descriptive"></a><a name="22.1"></a>
  - [23.1](#naming--descriptive) 한 문자로 된 이름은 피하세요. 이름으로부터 의도가 읽혀질 수 있게 해주세요. eslint: [`id-length`](https://eslint.org/docs/rules/id-length)

    ```javascript
    // bad
    function q() {
      // ...
    }

    // good
    function query() {
      // ...
    }
    ```

  <a name="naming--camelCase"></a><a name="22.2"></a>
  - [23.2](#naming--camelCase) 객체, 함수, 인스턴스에는 캐멀케이스(camelCase)를 사용하세요. eslint: [`camelcase`](https://eslint.org/docs/rules/camelcase.html)

    ```javascript
    // bad
    const OBJEcttsssss = {};
    const this_is_my_object = {};
    function c() {}

    // good
    const thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

  <a name="naming--PascalCase"></a><a name="22.3"></a>
  - [23.3](#naming--PascalCase) 클래스나 생성자에는 파스칼케이스(PascalCase)를 사용하세요. eslint: [`new-cap`](https://eslint.org/docs/rules/new-cap.html)

    ```javascript
    // bad
    function user(options) {
      this.name = options.name;
    }

    const bad = new user({
      name: 'nope',
    });

    // good
    class User {
      constructor(options) {
        this.name = options.name;
      }
    }

    const good = new User({
      name: 'yup',
    });
    ```

  <a name="naming--leading-underscore"></a><a name="22.4"></a>
  - [23.4](#naming--leading-underscore) 언더스코어를 사용하지 마세요. eslint: [`no-underscore-dangle`](https://eslint.org/docs/rules/no-underscore-dangle.html)

    > 왜? 자바스크립트는 속성이나 메소드 측면에서 은닉된 정보라는 개념을 가지고 있지 않습니다. 언더스코어는 일반적으로 “private”을 의미하지만, 사실 자바스크립트에서 해당 속성은 완전히 public하며, 이는 공공 API의 일부입니다. 이 관례는 개발자들로 하여금 변화가 깨지지 않는 것으로 간주하거나 테스트가 필요하지 않다고 잘못 생각하게 만듭니다. 요약: 만약 뭔가를 “private”하게 사용하고 싶다면, 그것은 있을 수 없는 일입니다.

    ```javascript
    // bad
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';
    this._firstName = 'Panda';

    // good
    this.firstName = 'Panda';

    // good, in environments where WeakMaps are available
    // see https://kangax.github.io/compat-table/es6/#test-WeakMap
    const firstNames = new WeakMap();
    firstNames.set(this, 'Panda');
    ```

  <a name="naming--self-this"></a><a name="22.5"></a>
  - [23.5](#naming--self-this) 참조를 `this`에 저장하지 마세요. 화살표 함수나 [Function#bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)를 사용하세요.

    ```javascript
    // bad
    function foo() {
      const self = this;
      return function () {
        console.log(self);
      };
    }

    // bad
    function foo() {
      const that = this;
      return function () {
        console.log(that);
      };
    }

    // good
    function foo() {
      return () => {
        console.log(this);
      };
    }
    ```

  <a name="naming--filename-matches-export"></a><a name="22.6"></a>
  - [23.6](#naming--filename-matches-export) 파일 이름은 default export의 이름과 일치해야 합니다.  

    ```javascript
    // 파일 1 내용
    class CheckBox {
      // ...
    }
    export default CheckBox;

    // 파일 2 내용
    export default function fortyTwo() { return 42; }

    // 파일 3 내용
    export default function insideDirectory() {}

    // 다른 파일
    // bad
    import CheckBox from './checkBox'; // PascalCase import/export, camelCase filename
    import FortyTwo from './FortyTwo'; // PascalCase import/filename, camelCase export
    import InsideDirectory from './InsideDirectory'; // PascalCase import/filename, camelCase export

    // bad
    import CheckBox from './check_box'; // PascalCase import/export, snake_case filename
    import forty_two from './forty_two'; // snake_case import/filename, camelCase export
    import inside_directory from './inside_directory'; // snake_case import, camelCase export
    import index from './inside_directory/index'; // requiring the index file explicitly
    import insideDirectory from './insideDirectory/index'; // requiring the index file explicitly

    // good
    import CheckBox from './CheckBox'; // PascalCase export/import/filename
    import fortyTwo from './fortyTwo'; // camelCase export/import/filename
    import insideDirectory from './insideDirectory'; // camelCase export/import/directory name/implicit "index"
    // ^ supports both insideDirectory.js and insideDirectory/index.js
    ```

  <a name="naming--camelCase-default-export"></a><a name="22.7"></a>
  - [23.7](#naming--camelCase-default-export) 함수를 export-default할 때 캐멀케이스(camelCase)를 사용하세요. 파일 이름은 함수 이름과 같아야 합니다.

    ```javascript
    function makeStyleGuide() {
      // ...
    }

    export default makeStyleGuide;
    ```

  <a name="naming--PascalCase-singleton"></a><a name="22.8"></a>
  - [23.8](#naming--PascalCase-singleton) 생성자 / 클래스 / 싱글톤 / 함수 라이브러리 / 단순 객체를 export할 때 파스칼케이스(PascalCase)를 사용하세요.

    ```javascript
    const AirbnbStyleGuide = {
      es6: {
      },
    };

    export default AirbnbStyleGuide;
    ```

  <a name="naming--Acronyms-and-Initialisms"></a>
  - [23.9](#naming--Acronyms-and-Initialisms) 두문자어와 이니셜은 모두 대문자이거나 모두 소문자이어야 합니다.

    > 왜? 이름은 가독성을 위한 것이지 컴퓨터 알고리즘을 위한 것이 아니기 때문입니다.

    ```javascript
    // bad
    import SmsContainer from './containers/SmsContainer';

    // bad
    const HttpRequests = [
      // ...
    ];

    // good
    import SMSContainer from './containers/SMSContainer';

    // good
    const HTTPRequests = [
      // ...
    ];

    // also good
    const httpRequests = [
      // ...
    ];

    // best
    import TextMessageContainer from './containers/TextMessageContainer';

    // best
    const requests = [
      // ...
    ];
    ```

  <a name="naming--uppercase"></a>
  - [23.10](#naming--uppercase) 상수 이름을 대문자로 짓는 것은 해당 상수가 (1) 내보내기 될 때, (2) `const` 타입일 때 (값이 재할당되지 못할 때), (3) 그 상수와 상수가 중첩된 속성이 절대 변하지 않는다는 것을 신뢰할 수 있을 때만 하세요.

    > 왜? 이것은 변수가 영원히 변하지 않는다는 것을 확신할 수 없을 때 도움을 주기 위한 추가적인 도구입니다. 대문자 변수는 변수와 변수의 속성이 변하지 않는다는 것을 프로그래머에게 알려줍니다.

    - 모든 `const` 변수 이름을 대문자로 짓나요? - 이것은 필수사항이 아니며, 파일 내 상수 이름을 꼭 대문자로 지을 필요는 없습니다. 하지만 내보내기되는 상수 이름은 대문자로 지어야 합니다.

    - 내보내기 되는 객체 이름을 대문자로 짓나요? - 최상위 수준의 내보내기를 할 때 대문자로 이름짓고 (예시: `EXPORTED_OBJECT.key`) 모든 중첩된 속성이 변경되지 않도록 유지합니다.

    ```javascript
    // bad
    const PRIVATE_VARIABLE = 'should not be unnecessarily uppercased within a file';

    // bad
    export const THING_TO_BE_CHANGED = 'should obviously not be uppercased';

    // bad
    export let REASSIGNABLE_VARIABLE = 'do not use let with uppercase variables';

    // ---

    // allowed but does not supply semantic value
    export const apiKey = 'SOMEKEY';

    // better in most cases
    export const API_KEY = 'SOMEKEY';

    // ---

    // bad - unnecessarily uppercases key while adding no semantic value
    export const MAPPING = {
      KEY: 'value'
    };

    // good
    export const MAPPING = {
      key: 'value'
    };
    ```

**[⬆ back to top](#목차)**

## 접근자 (Accessors)

  <a name="accessors--not-required"></a><a name="23.1"></a>
  - [24.1](#accessors--not-required) 속성을 위한 접근자 함수는 필수가 아닙니다.

  <a name="accessors--no-getters-setters"></a><a name="23.2"></a>
  - [24.2](#accessors--no-getters-setters) 자바스크립트 getters/setters를 사용하지 마세요. 예기치못한 사이드 이펙트를 일으키고 테스트와 유지보수를 어렵게 만듭니다. 접근자 함수를 만들고 싶다면 대신, `getVal()`과 `setVal('hello')`를 사용하세요.

    ```javascript
    // bad
    class Dragon {
      get age() {
        // ...
      }

      set age(value) {
        // ...
      }
    }

    // good
    class Dragon {
      getAge() {
        // ...
      }

      setAge(value) {
        // ...
      }
    }
    ```

  <a name="accessors--boolean-prefix"></a><a name="23.3"></a>
  - [24.3](#accessors--boolean-prefix) 속성이나 메소드가 `boolean`이라면, `isVal()`이나 `hasVal()`을 사용하세요.

    ```javascript
    // bad
    if (!dragon.age()) {
      return false;
    }

    // good
    if (!dragon.hasAge()) {
      return false;
    }
    ```

  <a name="accessors--consistent"></a><a name="23.4"></a>
  - [24.4](#accessors--consistent) `get()`과 `set()` 함수를 만들되, 일관성있게 만드세요.

    ```javascript
    class Jedi {
      constructor(options = {}) {
        const lightsaber = options.lightsaber || 'blue';
        this.set('lightsaber', lightsaber);
      }

      set(key, val) {
        this[key] = val;
      }

      get(key) {
        return this[key];
      }
    }
    ```

**[⬆ back to top](#목차)**

## 이벤트 (Events)

  <a name="events--hash"></a><a name="24.1"></a>
  - [25.1](#events--hash) (DOM이벤트나 Backbone 이벤트와 같은) 이벤트로 payload의 값을 넘길 경우 raw값 보다는 해시값을 넘겨주세요. 이렇게하면 이후 기여자가 이벤트에 관련한 모든 핸들러를 찾아서 바꾸는 대신 이벤트 payload에 값을 추가할 수 있습니다. 예를 들면 이렇게요:

    ```javascript
    // bad
    $(this).trigger('listingUpdated', listing.id);

    // ...

    $(this).on('listingUpdated', (e, listingID) => {
      // do something with listingID
    });
    ```

    이쪽이 더 좋습니다:

    ```javascript
    // good
    $(this).trigger('listingUpdated', { listingID: listing.id });

    // ...

    $(this).on('listingUpdated', (e, data) => {
      // do something with data.listingID
    });
    ```

  **[⬆ back to top](#목차)**

## 제이쿼리 (jQuery)

  <a name="jquery--dollar-prefix"></a><a name="25.1"></a>
  - [26.1](#jquery--dollar-prefix) 제이쿼리 객체 변수의 앞에는 `$`를 붙여주세요.

    ```javascript
    // bad
    const sidebar = $('.sidebar');

    // good
    const $sidebar = $('.sidebar');

    // good
    const $sidebarBtn = $('.sidebar-btn');
    ```

  <a name="jquery--cache"></a><a name="25.2"></a>
  - [26.2](#jquery--cache) 제이쿼리의 검색결과를 캐시하세요.

    ```javascript
    // bad
    function setSidebar() {
      $('.sidebar').hide();

      // ...

      $('.sidebar').css({
        'background-color': 'pink',
      });
    }

    // good
    function setSidebar() {
      const $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...

      $sidebar.css({
        'background-color': 'pink',
      });
    }
    ```

  <a name="jquery--queries"></a><a name="25.3"></a>
  - [26.3](#jquery--queries) DOM 검색에는 `$('.sidebar ul')`이나 parent > child `$('.sidebar > ul')`와 같은 캐스케이딩를 사용하세요. [jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)

  <a name="jquery--find"></a><a name="25.4"></a>
  - [26.4](#jquery--find) 한정된 제이쿼리 객체 쿼리에는 `find`를 사용하세요.

    ```javascript
    // bad
    $('ul', '.sidebar').hide();

    // bad
    $('.sidebar').find('ul').hide();

    // good
    $('.sidebar ul').hide();

    // good
    $('.sidebar > ul').hide();

    // good
    $sidebar.find('ul').hide();
    ```

**[⬆ back to top](#목차)**

## ES5 호환성 (ECMAScript 5 Compatibility)

  <a name="es5-compat--kangax"></a><a name="26.1"></a>
  - [27.1](#es5-compat--kangax) [Kangax](https://twitter.com/kangax/)의 ES5 [호환성 표](https://kangax.github.io/es5-compat-table/)를 참고하세요.

**[⬆ back to top](#목차)**

<a name="ecmascript-6-styles"></a>
## ECMAScript 6+ (ES 2015+) 스타일

  <a name="es6-styles"></a><a name="27.1"></a>
  - [28.1](#es6-styles) 여러 ES6+ 기능과 관련된 링크 모음입니다.

1. [화살표 함수 (Arrow Functions)](#화살표-함수-arrow-functions)
1. [클래스 (Classes)](#클래스와-&-생성자-classes--constructors)
1. [객체 단축형 (Object Shorthand)](#es6-object-shorthand)
1. [객체 속성 단축형 (Object Concise)](#es6-object-concise)
1. [객체 속성 계산 (Object Computed Properties)](#es6-computed-properties)
1. [템플릿 문자열 (Template Strings)](#es6-template-literals)
1. [비구조화 (Destructuring)](#비구조화-destructuring)
1. [기본 매개변수 (Default Parameters)](#es6-default-parameters)
1. [나머지 구문 (Rest)](#es6-rest)
1. [배열 전개 (Array Spreads)](#es6-array-spreads)
1. [Let과 Const (Let and Const)](#참조-references)
1. [제곱 연산자 (Exponentiation Operator)](#es2016-properties--exponentiation-operator)
1. [이터레이터와 제너레이터 (Iterators and Generators)](#이터레이터와-제너레이터-iterators-and-generators)
1. [모듈 (Modules)](#모듈-modules)

  <a name="tc39-proposals"></a>
  - [28.2](#tc39-proposals) 스테이지3에 이르지 못하는 [TC39 proposals](https://github.com/tc39/proposals)를 사용하지 마세요.

    > 왜? [그것들은 확정되지 않았습니다](https://tc39.github.io/process-document/). 그리고 이들은 변경되거나 완전히 폐기될 수도 있습니다. 우리는 자바스크립트를 사용하기를 원하지만, proposals는 아직 자바스크립트가 아닙니다.

**[⬆ back to top](#목차)**

## 표준 라이브러리 (Standard Library)

  [표준 라이브러리](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects)는 기능적으로 문제가 있지만 레거시 이유로 아직 남아있는 유틸리티들을 포함하고 있습니다.

  <a name="standard-library--isnan"></a>
  - [29.1](#standard-library--isnan) 전역 `isNaN` 대신 `Number.isNaN`을 사용하세요.
    eslint: [`no-restricted-globals`](https://eslint.org/docs/rules/no-restricted-globals)

    > 왜? 전역 `isNaN`은 숫자가 아닌 것을 숫자로 강제하고, NaN으로 간주되는 모든 것을 true로 반환합니다.
    > 만약 이것을 사용해야 한다면 명시적으로 사용하세요.

    ```javascript
    // bad
    isNaN('1.2'); // false
    isNaN('1.2.3'); // true

    // good
    Number.isNaN('1.2.3'); // false
    Number.isNaN(Number('1.2.3')); // true
    ```

  <a name="standard-library--isfinite"></a>
  - [29.2](#standard-library--isfinite) 전역 `isFinite` 대신 `Number.isFinite`을 사용하세요.
    eslint: [`no-restricted-globals`](https://eslint.org/docs/rules/no-restricted-globals)

    > 왜? 전역 `isFinite`은 숫자가 아닌 것을 숫자로 강제하고, 유한한 숫자로 간주되는 모든 것을 true로 반환합니다.
    > 만약 이것을 사용해야 한다면 명시적으로 사용하세요.

    ```javascript
    // bad
    isFinite('2e3'); // true

    // good
    Number.isFinite('2e3'); // false
    Number.isFinite(parseInt('2e3', 10)); // true
    ```

**[⬆ back to top](#목차)**

## 테스트 (Testing)

  <a name="testing--yup"></a><a name="28.1"></a>
  - [30.1](#testing--yup) **합시다.**

    ```javascript
    function foo() {
      return true;
    }
    ```

  <a name="testing--for-real"></a><a name="28.2"></a>
  - [30.2](#testing--for-real) **진지하게 생각해보죠**:
    - 어떤 테스트 프레임워크를 사용하든 테스트를 작성하세요!
    - 작고 순수한 기능을 쓰도록 노력하고, 조작이 일어나는 곳을 최소화하세요.
    - stubs과 mocks에 주의하세요 - 테스트를 더 다루기 힘들게 만들 수 있습니다.
    - Airbnb에서는 [`mocha`](https://www.npmjs.com/package/mocha)와 [`jest`](https://www.npmjs.com/package/jest)를 주로 사용합니다. [`tape`](https://www.npmjs.com/package/tape)도 때때로 작은 개별 모듈에 사용됩니다.
    - 100% 테스트 적용 범위에 도달하는 것이 항상 실용적이지는 않지만, 좋은 목표입니다.
    - 버그를 고칠 때마다 _회귀 테스트_ 를 작성하세요. 회귀 테스트 없이 고쳐진 버그는 미래에 거의 분명히 문제를 다시 일으킵니다. 

**[⬆ back to top](#목차)**

## 성능 (Performance)

  - [On Layout & Web Performance](https://www.kellegous.com/j/2013/01/26/layout-performance/)
  - [String vs Array Concat](https://jsperf.com/string-vs-array-concat/2)
  - [Try/Catch Cost In a Loop](https://jsperf.com/try-catch-in-loop-cost)
  - [Bang Function](https://jsperf.com/bang-function)
  - [jQuery Find vs Context, Selector](https://jsperf.com/jquery-find-vs-context-sel/13)
  - [innerHTML vs textContent for script text](https://jsperf.com/innerhtml-vs-textcontent-for-script-text)
  - [Long String Concatenation](https://jsperf.com/ya-string-concat)
  - [Are Javascript functions like `map()`, `reduce()`, and `filter()` optimized for traversing arrays?](https://www.quora.com/JavaScript-programming-language-Are-Javascript-functions-like-map-reduce-and-filter-already-optimized-for-traversing-array/answer/Quildreen-Motta)
  - Loading...

**[⬆ back to top](#목차)**

## 자료 (Resources)

**Learning ES6+**

  - [Latest ECMA spec](https://tc39.github.io/ecma262/)
  - [ExploringJS](http://exploringjs.com/)
  - [ES6 Compatibility Table](https://kangax.github.io/compat-table/es6/)
  - [Comprehensive Overview of ES6 Features](http://es6-features.org/)

**Read This**

  - [Standard ECMA-262](http://www.ecma-international.org/ecma-262/6.0/index.html)

**Tools**

  - Code Style Linters
    - [ESlint](https://eslint.org/) - [Airbnb Style .eslintrc](https://github.com/airbnb/javascript/blob/master/linters/.eslintrc)
    - [JSHint](http://jshint.com/) - [Airbnb Style .jshintrc](https://github.com/airbnb/javascript/blob/master/linters/.jshintrc)
  - Neutrino Preset - [@neutrinojs/airbnb](https://neutrinojs.org/packages/airbnb/)

**Other Style Guides**

  - [Google JavaScript Style Guide](https://google.github.io/styleguide/javascriptguide.xml)
  - [jQuery Core Style Guidelines](https://contribute.jquery.org/style-guide/js/)
  - [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js)
  - [StandardJS](https://standardjs.com)

**Other Styles**

  - [Naming this in nested functions](https://gist.github.com/cjohansen/4135065) - Christian Johansen
  - [Conditional Callbacks](https://github.com/airbnb/javascript/issues/52) - Ross Allen
  - [Popular JavaScript Coding Conventions on GitHub](http://sideeffect.kr/popularconvention/#javascript) - JeongHoon Byun
  - [Multiple var statements in JavaScript, not superfluous](http://benalman.com/news/2012/05/multiple-var-statements-javascript/) - Ben Alman

**Further Reading**

  - [Understanding JavaScript Closures](https://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/) - Angus Croll
  - [Basic JavaScript for the impatient programmer](http://www.2ality.com/2013/06/basic-javascript.html) - Dr. Axel Rauschmayer
  - [You Might Not Need jQuery](http://youmightnotneedjquery.com/) - Zack Bloom & Adam Schwartz
  - [ES6 Features](https://github.com/lukehoban/es6features) - Luke Hoban
  - [Frontend Guidelines](https://github.com/bendc/frontend-guidelines) - Benjamin De Cock

**Books**

  - [JavaScript: The Good Parts](https://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742) - Douglas Crockford
  - [JavaScript Patterns](https://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) - Stoyan Stefanov
  - [Pro JavaScript Design Patterns](https://www.amazon.com/JavaScript-Design-Patterns-Recipes-Problem-Solution/dp/159059908X)  - Ross Harmes and Dustin Diaz
  - [High Performance Web Sites: Essential Knowledge for Front-End Engineers](https://www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309) - Steve Souders
  - [Maintainable JavaScript](https://www.amazon.com/Maintainable-JavaScript-Nicholas-C-Zakas/dp/1449327680) - Nicholas C. Zakas
  - [JavaScript Web Applications](https://www.amazon.com/JavaScript-Web-Applications-Alex-MacCaw/dp/144930351X) - Alex MacCaw
  - [Pro JavaScript Techniques](https://www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273) - John Resig
  - [Smashing Node.js: JavaScript Everywhere](https://www.amazon.com/Smashing-Node-js-JavaScript-Everywhere-Magazine/dp/1119962595) - Guillermo Rauch
  - [Secrets of the JavaScript Ninja](https://www.amazon.com/Secrets-JavaScript-Ninja-John-Resig/dp/193398869X) - John Resig and Bear Bibeault
  - [Human JavaScript](http://humanjavascript.com/) - Henrik Joreteg
  - [Superhero.js](http://superherojs.com/) - Kim Joar Bekkelund, Mads Mobæk, & Olav Bjorkoy
  - [JSBooks](http://jsbooks.revolunet.com/) - Julien Bouquillon
  - [Third Party JavaScript](https://www.manning.com/books/third-party-javascript) - Ben Vinegar and Anton Kovalyov
  - [Effective JavaScript: 68 Specific Ways to Harness the Power of JavaScript](http://amzn.com/0321812182) - David Herman
  - [Eloquent JavaScript](http://eloquentjavascript.net/) - Marijn Haverbeke
  - [You Don’t Know JS: ES6 & Beyond](http://shop.oreilly.com/product/0636920033769.do) - Kyle Simpson

**Blogs**

  - [JavaScript Weekly](http://javascriptweekly.com/)
  - [JavaScript, JavaScript...](https://javascriptweblog.wordpress.com/)
  - [Bocoup Weblog](https://bocoup.com/weblog)
  - [Adequately Good](http://www.adequatelygood.com/)
  - [NCZOnline](https://www.nczonline.net/)
  - [Perfection Kills](http://perfectionkills.com/)
  - [Ben Alman](http://benalman.com/)
  - [Dmitry Baranovskiy](http://dmitry.baranovskiy.com/)
  - [nettuts](http://code.tutsplus.com/?s=javascript)

**Podcasts**

  - [JavaScript Air](https://javascriptair.com/)
  - [JavaScript Jabber](https://devchat.tv/js-jabber/)

**[⬆ back to top](#목차)**

## In the Wild

  아래 목록은 이 스타일 가이드를 사용하고 있는 단체들입니다. 우리에게 풀 리퀘스트를 보내면 리스트에 추가해드리겠습니다.

  - **123erfasst**: [123erfasst/javascript](https://github.com/123erfasst/javascript)
  - **4Catalyzer**: [4Catalyzer/javascript](https://github.com/4Catalyzer/javascript)
  - **Aan Zee**: [AanZee/javascript](https://github.com/AanZee/javascript)
  - **Airbnb**: [airbnb/javascript](https://github.com/airbnb/javascript)
  - **AltSchool**: [AltSchool/javascript](https://github.com/AltSchool/javascript)
  - **Apartmint**: [apartmint/javascript](https://github.com/apartmint/javascript)
  - **Ascribe**: [ascribe/javascript](https://github.com/ascribe/javascript)
  - **Avant**: [avantcredit/javascript](https://github.com/avantcredit/javascript)
  - **Axept**: [axept/javascript](https://github.com/axept/javascript)
  - **Billabong**: [billabong/javascript](https://github.com/billabong/javascript)
  - **Bisk**: [bisk](https://github.com/Bisk/)
  - **Bonhomme**: [bonhommeparis/javascript](https://github.com/bonhommeparis/javascript)
  - **Brainshark**: [brainshark/javascript](https://github.com/brainshark/javascript)
  - **CaseNine**: [CaseNine/javascript](https://github.com/CaseNine/javascript)
  - **Cerner**: [Cerner](https://github.com/cerner/)
  - **Chartboost**: [ChartBoost/javascript-style-guide](https://github.com/ChartBoost/javascript-style-guide)
  - **ComparaOnline**: [comparaonline/javascript](https://github.com/comparaonline/javascript-style-guide)
  - **Compass Learning**: [compasslearning/javascript-style-guide](https://github.com/compasslearning/javascript-style-guide)
  - **DailyMotion**: [dailymotion/javascript](https://github.com/dailymotion/javascript)
  - **DoSomething**: [DoSomething/eslint-config](https://github.com/DoSomething/eslint-config)
  - **Digitpaint** [digitpaint/javascript](https://github.com/digitpaint/javascript)
  - **Drupal**: [www.drupal.org](https://git.drupalcode.org/project/drupal/blob/8.6.x/core/.eslintrc.json)
  - **Ecosia**: [ecosia/javascript](https://github.com/ecosia/javascript)
  - **Evernote**: [evernote/javascript-style-guide](https://github.com/evernote/javascript-style-guide)
  - **Evolution Gaming**: [evolution-gaming/javascript](https://github.com/evolution-gaming/javascript)
  - **EvozonJs**: [evozonjs/javascript](https://github.com/evozonjs/javascript)
  - **ExactTarget**: [ExactTarget/javascript](https://github.com/ExactTarget/javascript)
  - **Flexberry**: [Flexberry/javascript-style-guide](https://github.com/Flexberry/javascript-style-guide)
  - **Gawker Media**: [gawkermedia](https://github.com/gawkermedia/)
  - **General Electric**: [GeneralElectric/javascript](https://github.com/GeneralElectric/javascript)
  - **Generation Tux**: [GenerationTux/javascript](https://github.com/generationtux/styleguide)
  - **GoodData**: [gooddata/gdc-js-style](https://github.com/gooddata/gdc-js-style)
  - **Grooveshark**: [grooveshark/javascript](https://github.com/grooveshark/javascript)
  - **Grupo-Abraxas**: [Grupo-Abraxas/javascript](https://github.com/Grupo-Abraxas/javascript)
  - **Honey**: [honeyscience/javascript](https://github.com/honeyscience/javascript)
  - **How About We**: [howaboutwe/javascript](https://github.com/howaboutwe/javascript-style-guide)
  - **HubSpot**: [HubSpot/javascript](https://github.com/HubSpot/javascript)
  - **Hyper**: [hyperoslo/javascript-playbook](https://github.com/hyperoslo/javascript-playbook/blob/master/style.md)
  - **InterCity Group**: [intercitygroup/javascript-style-guide](https://github.com/intercitygroup/javascript-style-guide)
  - **Jam3**: [Jam3/Javascript-Code-Conventions](https://github.com/Jam3/Javascript-Code-Conventions)
  - **JSSolutions**: [JSSolutions/javascript](https://github.com/JSSolutions/javascript)
  - **Kaplan Komputing**: [kaplankomputing/javascript](https://github.com/kaplankomputing/javascript)
  - **KickorStick**: [kickorstick](https://github.com/kickorstick/)
  - **Kinetica Solutions**: [kinetica/javascript](https://github.com/kinetica/Javascript-style-guide)
  - **LEINWAND**: [LEINWAND/javascript](https://github.com/LEINWAND/javascript)
  - **Lonely Planet**: [lonelyplanet/javascript](https://github.com/lonelyplanet/javascript)
  - **M2GEN**: [M2GEN/javascript](https://github.com/M2GEN/javascript)
  - **Mighty Spring**: [mightyspring/javascript](https://github.com/mightyspring/javascript)
  - **MinnPost**: [MinnPost/javascript](https://github.com/MinnPost/javascript)
  - **MitocGroup**: [MitocGroup/javascript](https://github.com/MitocGroup/javascript)
  - **Muber**: [muber](https://github.com/muber/)
  - **National Geographic**: [natgeo](https://github.com/natgeo/)
  - **Nulogy**: [nulogy/javascript](https://github.com/nulogy/javascript)
  - **Orange Hill Development**: [orangehill/javascript](https://github.com/orangehill/javascript)
  - **Orion Health**: [orionhealth/javascript](https://github.com/orionhealth/javascript)
  - **OutBoxSoft**: [OutBoxSoft/javascript](https://github.com/OutBoxSoft/javascript)
  - **Peerby**: [Peerby/javascript](https://github.com/Peerby/javascript)
  - **Pier 1**: [Pier1/javascript](https://github.com/pier1/javascript)
  - **Qotto**: [Qotto/javascript-style-guide](https://github.com/Qotto/javascript-style-guide)
  - **React**: [facebook.github.io/react/contributing/how-to-contribute.html#style-guide](https://facebook.github.io/react/contributing/how-to-contribute.html#style-guide)
  - **REI**: [reidev/js-style-guide](https://github.com/rei/code-style-guides/)
  - **Ripple**: [ripple/javascript-style-guide](https://github.com/ripple/javascript-style-guide)
  - **Sainsbury's Supermarkets**: [jsainsburyplc](https://github.com/jsainsburyplc)
  - **Shutterfly**: [shutterfly/javascript](https://github.com/shutterfly/javascript)
  - **Sourcetoad**: [sourcetoad/javascript](https://github.com/sourcetoad/javascript)
  - **Springload**: [springload](https://github.com/springload/)
  - **StratoDem Analytics**: [stratodem/javascript](https://github.com/stratodem/javascript)
  - **SteelKiwi Development**: [steelkiwi/javascript](https://github.com/steelkiwi/javascript)
  - **StudentSphere**: [studentsphere/javascript](https://github.com/studentsphere/guide-javascript)
  - **SwoopApp**: [swoopapp/javascript](https://github.com/swoopapp/javascript)
  - **SysGarage**: [sysgarage/javascript-style-guide](https://github.com/sysgarage/javascript-style-guide)
  - **Syzygy Warsaw**: [syzygypl/javascript](https://github.com/syzygypl/javascript)
  - **Target**: [target/javascript](https://github.com/target/javascript)
  - **TheLadders**: [TheLadders/javascript](https://github.com/TheLadders/javascript)
  - **The Nerdery**: [thenerdery/javascript-standards](https://github.com/thenerdery/javascript-standards)
  - **T4R Technology**: [T4R-Technology/javascript](https://github.com/T4R-Technology/javascript)
  - **UrbanSim**: [urbansim](https://github.com/urbansim/)
  - **VoxFeed**: [VoxFeed/javascript-style-guide](https://github.com/VoxFeed/javascript-style-guide)
  - **WeBox Studio**: [weboxstudio/javascript](https://github.com/weboxstudio/javascript)
  - **Weggo**: [Weggo/javascript](https://github.com/Weggo/javascript)
  - **Zillow**: [zillow/javascript](https://github.com/zillow/javascript)
  - **ZocDoc**: [ZocDoc/javascript](https://github.com/ZocDoc/javascript)

**[⬆ back to top](#목차)**

## Translation

  이 스타일 가이드는 다른 언어로도 제공됩니다:

  - ![br](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Brazilian Portuguese**: [armoucar/javascript-style-guide](https://github.com/armoucar/javascript-style-guide)
  - ![bg](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Bulgaria.png) **Bulgarian**: [borislavvv/javascript](https://github.com/borislavvv/javascript)
  - ![ca](https://raw.githubusercontent.com/fpmweb/javascript-style-guide/master/img/catala.png) **Catalan**: [fpmweb/javascript-style-guide](https://github.com/fpmweb/javascript-style-guide)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [yuche/javascript](https://github.com/yuche/javascript)
  - ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Chinese (Traditional)**: [jigsawye/javascript](https://github.com/jigsawye/javascript)
  - ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **French**: [nmussy/javascript-style-guide](https://github.com/nmussy/javascript-style-guide)
  - ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **German**: [timofurrer/javascript-style-guide](https://github.com/timofurrer/javascript-style-guide)
  - ![it](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**: [sinkswim/javascript-style-guide](https://github.com/sinkswim/javascript-style-guide)
  - ![jp](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [mitsuruog/javascript-style-guide](https://github.com/mitsuruog/javascript-style-guide)
  - ![kr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [ParkSB/javascript-style-guide](https://github.com/ParkSB/javascript-style-guide)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**: [leonidlebedev/javascript-airbnb](https://github.com/leonidlebedev/javascript-airbnb)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [paolocarrasco/javascript-style-guide](https://github.com/paolocarrasco/javascript-style-guide)
  - ![th](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Thailand.png) **Thai**: [lvarayut/javascript-style-guide](https://github.com/lvarayut/javascript-style-guide)
  - ![tr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Turkey.png) **Turkish**: [eraycetinay/javascript](https://github.com/eraycetinay/javascript)
  - ![ua](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Ukraine.png) **Ukrainian**: [ivanzusko/javascript](https://github.com/ivanzusko/javascript)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnam**: [hngiang/javascript-style-guide](https://github.com/hngiang/javascript-style-guide)

## The JavaScript Style Guide Guide

  - [Reference](https://github.com/airbnb/javascript/wiki/The-JavaScript-Style-Guide-Guide)

## Chat With Us About JavaScript

  - Find us on [gitter](https://gitter.im/airbnb/javascript).

## Contributors

  - [View Contributors](https://github.com/airbnb/javascript/graphs/contributors)

## License

(The MIT License)

Copyright (c) 2012 Airbnb

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ back to top](#목차)**

## Amendments

우리는 당신이 이 가이드를 포크해서 당신의 팀에 알맞도록 고쳐 쓰기를 바랍니다. 아래에 스타일 가이드의 수정 사항을 나열하세요. 이렇게 하면 병합 충돌(marge conflicts)을 신경쓰지 않고 스타일 가이드를 정기적으로 업데이트 할 수 있습니다. 

# };
