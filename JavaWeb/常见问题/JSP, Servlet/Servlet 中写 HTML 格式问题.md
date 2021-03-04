# Servlet 中写 HTML

若不作特别指定，在`out.print()`中写 HTML 标签，`<html><body>`标签的输出必须在其他输出的前面：★

```java
PrintWriter out = request.getWriter();

// 只能写在它们前面，不能写在其他地方，否则会直接输出文本，而不是以 HTML 的格式输出。★
// 后两句的位置可以互换。★
// 经自己尝试，HTML 中的文本是可以写在任何地方的，但是这里不支持。★
out.println("<html><body bgcolor='cyan'>");
out.print("Output: " + k);
out.println("</html></body>");
```

另一种解决方案：

在所有输出的前面添加这样一语句，即：`res.setContentType("text/html")`，此时就不限制输出语句的顺序（可以随意安排输出语句的顺序）：

```java
PrintWriter out = request.getWriter();

res.setContentType("text/html");

// 此时该输出就可以放在任意位置了，当然也可以放在最前面。★
out.print("Output: " + k);
out.println("<html><body bgcolor='cyan'>");
out.println("</html></body>");
```



