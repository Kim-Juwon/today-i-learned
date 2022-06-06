# JVM

## JVM(Java Virtual Machine)이란?
- Java 프로그램을 실행시켜주는 가상 기계
- 바이트 코드 파일(.class)을 OS에 최적화된 기계어로 번역하여 실행해준다.
	- 바이트 코드 파일(byte code file)이란?
		- 자바 소스 파일(.java)을 자바 컴파일러(javac)가 컴파일하여 산출된 파일
- 바이트 코드와 OS 사이의 중계자이다.

## JVM 구조
- class loader, runtime data area, execution engine, garbage collector로 나뉜다.
	1. 바이트 코드 파일을 class loader가 runtime data area에 배치한다.
	2. execution engine이 runtime data area에 있는 내용들을 명령어 단위로 읽어 실행한다.
	3. 프로그램 실행 도중에 heap area에 있는 오브젝트중 JVM Stack에서 도달할 수 없는 오브젝트들을 메모리에서 해제한다.
		- 메모리 누수 방지를 위해서이다.
		- C++과의 가장 큰 차이점이라고 할 수 있다.

		


