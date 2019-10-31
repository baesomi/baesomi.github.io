---
layout: page
title: 시큐어 코딩 검출유형 - Path Manipulation
tags: 시큐어코딩
key: page-single

---
## Path Manipulation  

**검출 이유**
  - 파일경로와 관련된 변수 (path, filepath 등..)에 경로값을 할당하여 validation check없이 바로 사용할 경우에 검출된다. 공격자가 경로를 제어할 가능성있기 때문!
  - 사용자가 지정한 내용만 허용되도록 하는 _화이트리스트_ 기법 과 사용자가 지정한 내용에 대해서 불허하도록 하는 _블랙리스트_ 기법이 있는데 보통 블랙리스트 기법을 사용한다.
  - 해당 이슈가 여러번 검출되었다면, util로 빼서 검출된 부분에서 호출하여 처리하는 것이 좋은방법(!?)
  
**예시**    
{% highlight ruby %}
String path = "C:/Users/test/files.txt"
File file = new File(path); // path를 바로 사용!!
{% endhighlight %}
  
**해결방법**
{% highlight ruby %}
String path = "C:/Users/test/files.txt"
String validPath = getValidPath(path);
File file = new File(validPath); 

// validation check method 예시
public String getValidPath(String path) throws Exception {
  if(path == null || "".equals(path)) {
    throw new Exception("path is null");
  }
	if(path.indexOf("..") > -1) {
		throw new Exception("path contains ..");
	}
	if(path.indexOf("//") > -1) {
		throw new Exception("path contains // :" + path);
	}
  return path;
}

{% endhighlight %}
  
이런 식으로 사용자가 허용하지 않은 문자열에 대해서 체크하여
새로운 path를 return하는 형식의 과정이 있어야한다. 
  
  
  

<!--more-->