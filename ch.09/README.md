# 🧷 9장 | 단위 테스트

### 📘 TDD 법칙 세 가지

1. 실패하는 단위 테스트를 작성할 때까지 실제 코드를 작성하지 않는다.
2. 컴파일은 실패하지 않으면서 실행이 실패하는 정도로만 단위 테스트를 작성한다.
3. 현재 실패하는 테스트를 통과할 정도로만 실제 코드를 작성한다.

##

### 📘 깨끗한 테스트 코드 유지하기

> 테스트 코드는 실제 코드 못지 않게 중요하다. 깨끗한 단위 테스트가 성공한다.

- '지저분해도 빨리' 작성한 테스트 코드는 결국 오히려 테스트를 안하느니만 못한 결과를 내놓는다.
- 테스트 코드는 실제 코드 못지 않게 중요하다. 실제 코드 못지 않게 깨끗하게 짜야 한다.
- 테스트는 유연성, 유지보수성, 재사용성을 제공한다.
- 테스트 케이스가 있으면 잠정적인 버그가 없을 것이라는 확신 하에 코드 변경이 쉬워진다.

##

### 📘 깨끗한 테스트 코드

> 가독성은 실제 코드보다 테스트 코드에 더더욱 중요하다.

**테스트 코드는 진짜 필요한 자료 유형과 함수만 사용한다.**

1. 테스트 자료 만들기
2. 테스트 자료 조작하기
3. 조작한 결과가 올바른지 확인하기

```java
public void testGetPageHierarchyAsWml() throws Exception {
	makePages("PageOne", "PageOne.ChildOne", "PageTwo");

	submitRequest("root", "type:pages");

	assertResponseIsXML();
	assertResponseContains(
		"<name>PageOne</name>", "<name>PageTwo</name>", "<name>ChildOne</name>"
	);
}
```

*BUILD-OPERATE-CHECK* 패턴이 적합한 테스트 구조다.  
각 테스트는 명확히 세 부분으로 나눠진다.  
첫 부분은 테스트 자료를 만든다. 두 번째 부분은 테스트 자료를 조작하며, 세 번째 부분은 조작한 결과가 올바른지 확인한다.  
> *API 위에다 함수와 유틸리티를 구현* 한 후 그 함수와 유틸리티를 사용하므로 테스트 코드를 짜기도, 읽기도 쉽다.

- **이중 표준**

> 테스트 API에 적용하는 표준은 실제 코드에 적용하는 표준과 다르다.

단순하고, 간결하고, 표현력이 풍부해야 하지만, 실제 코드만큼 효율적일 필요는 없다. 

실제 환경과 테스트 환경은 요구사항이 다르기 때문이다.

```java
@Test
	public void turnOnCoolerAndBlowerIfTooHot() throws Exception {
		tooHot();
		assertEquals("hBChl", hw.getState();
	}

@Test
	public void turnOnHeaterAndBlowerIfTooCold() throws Exception {
		wayTooCold();
		assertEquals("HBchl", hw.getState();
	}

@Test
	public void turnOnHiTempAlarmAtThreshold() throws Exception {
		wayTooHot();
		assertEquals("hBCHl", hw.getState();
	}

@Test
	public void turnOnLoTempAlarmAtThreshold() throws Exception {
		wayTooCold();
		assertEquals("HBchL", hw.getState();
	}
```

이상한 문자열에서 대문자는 켜짐, 소문자는 꺼짐을 나타낸다.   
'그릇된 정보를 피하라' 규칙의 위반에 가깝지만, **의미만 안다면 결과를 재빨리 판단할 수 있다.**  
테스트 코드를 이해하기 너무도 쉽다는 사실이 드러난다.


