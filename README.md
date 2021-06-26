# 스프링 메시지 및 국제화 기능 정리

------
## 스프링 메시지 기능
~~~
  @Bean
  public MessageSource messageSource() {
      ResourceBundleMessageSource messageSource = new
  ResourceBundleMessageSource();
      messageSource.setBasenames("messages", "errors");
      messageSource.setDefaultEncoding("utf-8");
      return messageSource;
} 
~~~
스프링 부트에서는 위와 같은 MessageSource 빈을 자동 등록해주기 때문에 별 다른 설정 없이 사용 가능


Resources 폴더 내에 messages.properties 생성하여 메시지 기능 사용
~~~
label.item.id=상품 ID
label.item.itemName=상품명
label.item.price=가격
label.item.quantity=수량

page.items=상품 목록
page.item=상품 상세
page.addItem=상품 등록
page.updateItem=상품 수정

button.save=저장
button.cancel=취소
~~~

타임 리프를 이용해 아래와 같이 사용 가능
~~~
<label for="itemName" th:text="#{item.itemName}"></label>
~~~


### 스프링 국제화 기능

메시지 기능을 응용하여 다국어 대응 가능
영어의 경우 Resources 폴더 내에 messages_en.properties 생성하여 적용

~~~
label.item=Item
label.item.id=Item ID
label.item.itemName=Item Name
label.item.price=price
label.item.quantity=quantity

page.items=Item List
page.item=Item Detail
page.addItem=Item Add
page.updateItem=Item Update

button.save=Save
button.cancel=Cancel
~~~

국제화 기능을 위해 LocalResolver 를 통해 Locale 정보를 MessageSource로 읽어옴
스프링 부트에서는 기본으로 AcceptHeaderLocaleResolver 를 사용하기 때문에 HTTP Header에 있는 Accept-Language 값을 이용함
