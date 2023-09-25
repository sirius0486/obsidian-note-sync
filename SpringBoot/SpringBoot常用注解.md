

@Controller     声明Controller类

@RestController  = @Controller + @ResponseBody 的组合

@RequestMapping 声明请求处理方法， 将HTTP请求映射到Controller方法


@ResponseBody  将方法返回值视为HTTP响应体，框架自动序列化成JSON

@RequestBody 将HTTP请求体映射成一个对象， 框架自动从JSON解析

@ResponseStatus 设置响应码

@PathVariable 将URL路径变量绑定到方法参数

@RequestParam 将HTTP请求参数绑定到方法参数


lombok
@data    生成getter 和 setter

@NoArgsConstructor 生成无参构造

@RequiredArgsConstructor 生成有参构造


自定义注解
@Tag(name = "Resource Management API")
