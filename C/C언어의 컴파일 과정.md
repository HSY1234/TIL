# C언어의 컴파일 과정

순서

- 전처리기 (preprocessor)
- 컴파일러 (compiler)
- 어셈블러 (assembler)
- 링커 (linker)

## gcc 컴파일러

```
// gcc에게 컴파일 명령 내리기
gcc a.c

// 실행파일 실행
gcc ./a.out
```

## 전처리기

- 전처리 과정(preprocess)
- test.c => test.i
- 본격적으로 컴파일을 하기전에 처리해야할 작업들
- 외부에서 선언된 다양한 소스 코드, 라이브러리 포함 (#include)
- 프로그래밍 편의를 위해 작성된 매크로 변환 (#define)
- 컴파일할 영역 명시 (#if, #ifdef)
- 간단한 printf문 작성시 stdio.h 라이브러리를 가져온것을 볼수있다

```
gcc -E a.c -o a.i
```

## 컴파일러

- 컴파일 과정(compile)
- test.i => test.s
- 전처리가 완료되어도 여전히 C언어로 된 소스코드
- 전처리 완료된 소스코드를 저급 언어(어셈블리 언어)로 변환

```
gcc -S a.i -o a.s
```

## 어셈블러

- 어셈블 과정(assemble)
- test.s => test.o
- 어셈블리어를 기계어로 변환
- 목적 코드(object file)를 포함하는 목적 파일이 됨

```
gcc -o a.o a.s
```

## 목적 파일 VS 실행파일

- 목적파일과 실행파일 둘다 기계어로 이루어진 파일
- 목적 파일과 실행파일은 다르다
- 목적 파일은 링킹을 거친 이후에야 실행파일이 된다

## 링커

- a.o + c.o => a.exe
- 링킹(linking) 과정
- 서로 다른 소스 코드를 오브젝트 파일로 만들었을때 소스 코드끼리 관련이 있을 경우 서로의 정보가 없다
- 링커가 두 오브젝트 파일을 이어서 실행파일을 생성
