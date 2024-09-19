定义：XML用于将数据从Html中分离出来， 并用于存储和传输数据，使数据具有结构性，易
读易处理

XML的语法：
- 头标签：\<?xml version="1.0" encoding="UTF-8"?\>（可写可不写）
- 标签：XML数据并不使用预定义的标签，任何标签都可以是用户自定义的，
- 分级：XML支持root—child—subchild分级
- 注：
	- XML文档必须至少有一个root元素，
	- 且XML标签必须要有结束标签，
	- XML标签大小写敏感，
	- XML不会自动删节空格，
- 属性：用以描述标签自身的额外属性
- CDATA标签使用<![CDATA["文字内容"]]>：用以原封不动的打印内容
- 命名空间：为避免不同调用不同XML的命名冲突，可使用前缀，并在root中引入头标签：xmlns="_namespaceURI_"

XML创建实例流程：
- function loadXMLDoc() {
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById("demo").innerHTML =
      this.responseText;
    }
  };
  xhttp.open("GET", "xmlhttp_info.txt", true);
  xhttp.send();
}

XML解释器及XML文件读取：
- 创建实例：parser = new DOMParser();  
xmlDoc = parser.parseFromString(text,"text/xml");
- 获取信息：xmlDoc.getElementsByTagName("title")\[0\].childNodes\[0\].nodeValue;
- 