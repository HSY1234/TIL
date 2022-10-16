# XML 네임스페이스(namespace)

XML 네임스페이스는 XML 요소 간의 이름에 대한 충돌을 방지해 주는 방법을 제공합니다.

XML 네임스페이스는 요소의 이름과 속성의 이름을 하나의 그룹으로 묶어주어 이름에 대한 충돌을 해결합니다.

이러한 XML 네임스페이스는 URI(Uniform Resource Identifiers)로 식별됩니다.

## XML 요소 간의 이름 충돌

XML에서는 사용자가 XML 요소의 이름을 직접 정의합니다.

따라서 서로 다른 XML 문서를 통합하려고 할 때 같은 이름을 가진 요소로 인해 충돌이 발생할 수 있습니다.

```xml
<body>

    <h1>html에서의 제목</h1>

    <p>html에서의 단락</p>

</body>

<body>

    <arm>70</arm>

    <leg>110</leg>

</body>
```

위의 두 예제에서 `<body>`요소는 서로 완전히 다른 의미로 사용됩니다.

예제 1에서는 HTML 문서의 `<body>`태그로 사용되었습니다.

예제 2에서는 실제 몸을 의미하여, 각 신체 부위의 치수를 기록하기 위해 사용되었습니다.

하지만 사용자나 XML 응용 프로그램은 두 `<body>`요소의 이러한 차이점을 어떻게 다뤄야 하는지 알지 못합니다.

## XML 네임스페이스의 선언

XML에서는 접두사(prefix)를 이용하여 위와 같은 이름의 충돌을 방지하고 있습니다.

서로 같은 이름에 요소마다 서로 다른 접두사를 붙이면 이름의 충돌을 방지할 수 있게 됩니다.

XML에서 이러한 접두사를 사용하려면, 반드시 먼저 접두사에 대한 네임스페이스를 선언해야 합니다.

XML에서 네임스페이스를 선언하는 문법은 다음과 같습니다.

```xml
<요소이름 xmlns:prefix="URI">
```

XML 네임스페이스의 선언은 xmlns나 xmlns:로 시작합니다.

prefix 속성값에는 이름 앞에 붙게 되는 네임스페이스 접두사(namespace prefix)를 명시합니다.

접두사로 사용되는 URI는 네임스페이스 식별자를 의미합니다.

참고: 네임스페이스 URI는 구문 분석기가 정보를 조회하는 데 사용하지 않습니다.

URI를 사용하는 목적은 네임스페이스에 고유한 이름을 부여하는 것입니다.

그러나 회사에서는 종종 네임스페이스를 네임스페이스 정보가 포함된 웹 페이지에 대한 포인터로 사용합니다.

예시

```xml
<root>

    <a:body xmlns:a="https://www.w3.org/TR/html5/">

        <a:h1>html에서의 제목</a:h1>

        <a:p>html에서의 단락</a:p>

    </a:body>

    <b:body xmlns:b="http://codingsam.com/xml/physical/">

        <b:arm>70</b:arm>

        <b:leg>110</b:leg>

    </b:body>

</root>
```

위의 예제에서 첫 번째 <body>요소의 xmlns 속성은 a:라는 접두사를 선언합니다.

두 번째 <body>요소의 xmlns 속성은 b:라는 접두사를 선언합니다.

이렇게 XML 요소에 네임스페이스가 선언되면, 해당 요소의 모든 자식(child) 요소에도 같은 네임스페이스가 선언됩니다.

이러한 네임스페이스 선언은 XML 루트(root) 요소에서도 선언할 수 있습니다.

```xml
<root

    xmlns:a="https://www.w3.org/TR/html5/"

    xmlns:b="http://codingsam.com/xml/physical/">

    <a:body>

        <a:h1>html에서의 제목</a:h1>

        <a:p>html에서의 단락</a:p>

    </a:body>

    <b:body>

        <b:arm>70</b:arm>

        <b:leg>110</b:leg>

    </b:body>

</root>
```
