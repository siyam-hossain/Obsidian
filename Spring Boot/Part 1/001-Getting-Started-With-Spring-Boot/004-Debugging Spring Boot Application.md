#debugging

```java
package com.sh.debuggingspringbootapplication;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class HomeController {
    @RequestMapping("/")
    public String index(){
        String viewName = getViewName();
        System.out.println(viewName);
        return viewName;
    }

    private String getViewName() {
        return "index";
    }
}
```

> [!bug]
> White label Error Page
> This application has no explicit mapping for /error, so you can seeing this as a fallback.

Here,

- With the help of `java System.out.println(viewName);` we can debug the issues
- Most popular debugging technique is, debugging with the help of ==break point==.
