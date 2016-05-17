# spring-boot に circuit-breaker を適用した話

---

## サーキットブレーカーとは？

xxxxxxxxxxxxxxxxx

---

## Sample code

[github BookService.java](https://github.com/horiga/gs-circuit-breaker/blob/study/cb-example-1/complete/reading/src/main/java/hello/BookService.java#L14-L31)

    !java
    @HystrixCommand(fallbackMethod = "reliable")
	public String readingList() {
		try {
			final String reading = new RestTemplate().getForObject(
                    URI.create("http://localhost:8090/recommended"),
                        String.class);
			log.info("(Success in reading list)");
			return reading;
		} catch (Throwable e) {
			log.error("<<Failed>> Reading lists in Book service");
			throw e;
		}
	}

	public String reliable() {
		log.error("(In fallback method)");
		return "Cloud Native Java (O'Reilly)";
	}

---

## @HystrixCommand

	!java
	@HystrixCommand(
		commandKey="hoge", 
		groupKey="hoge",
		fallbackMethod="fallback"
		commandProperties={
			@HystrixProperty(name="", value="")
		},
		threadProperties={
		}
		ignoreExceptions={}
	)
	public String execute(String str, int num) throws Exception {
		// do something
	}

	public String fallback(String str, int num) throws Exception {
		return "fallback";
	}

---

## @HystrixCommand - fallbackMethod

例外が発生された場合かつCircuitBreakerがOPEN状態の場合に迂回するmethodの名前. メソッドの引数、返却値は対象のメソッドと合わせることが必要.

	!java
	fallbackMethod="fallback"

---

## @HystrixCommand - ignoreExceptions

Circuitbreakerの対象外とするExceptionを設定する.

	!java
	ignoreExceptions = {IllegalArgumentException.class, HogeException.class}

---
## command / thread properties with property file



