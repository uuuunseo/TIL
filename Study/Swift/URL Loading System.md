# <b> URL Loading System </b>
https 같은 표준 프로토콜이나 직접 만든 커스텀 프로토콜을 사용한 URL로 구별되는 리소스에 접근하는 것을 제공  
데이터나 오류가 도착하는대로 처리할 수 있다.

<br>

### <b> URLSessionTask </b>
데이터를 가져와서 앱에 반환하거나 파일을 다운로드 하고, 데이터 및 파일을 업로드 할 수 있는 인스턴스  
URLSession 인스턴스를 통해서 URLSessionTask 인스턴스를 여러 개 만들 수 있다.

<br>

### <b> URLSessionConfiguration </b>
Session을 사용할 때 사용하는 객체
캐시나 쿠키를 어떻게 사용할지, 셀룰러 네트워크 연결을 허용할 것인지 같은 옵션을 구성할 수 있다.

Task를 생성하기 위해 하나의 세션을 계속해서 사용하는 것도 가능하다.