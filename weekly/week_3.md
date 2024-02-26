# Project Progress Report - Week 3

## Project Overview

This week, I started coding the "MongoDB Atlas App" application allocated to me for PicoLTE. First, I researched MongoDB Atlas. Then I looked at the endpoints of the MongoDB Atlas API that I would use directly in my application and what I could do. I tested the API via Postman, but when I wrote it as code in the application I developed, I received an error during the post request. Even though I tried for hours to solve this problem, I could not find a solution.

```
header = "\n".join(
    [
        f"POST /{query} HTTP/1.1",
        f"Host: {host}",
        "Custom-Header-Name: Custom-Data",
        "Content-Type: application/json",
        f"Content-Length: {len(payload)+1}",
        "\n\n",
    ]
)

step_post_request = Step(
    function=self.http.post,
    name="post_request",
    success="read_response",
    fail="failure",
    function_params={
        "header_mode": 1,
        "data": header + payload,
    },
)

sm.add_step(step_post_request)
```

```
+CME ERROR: 701 # Unknown Error
```

## References

1. [Pico LTE MicroPython SDK](https://github.com/sixfab/pico_lte_micropython-sdk)

2. [Sixfab Pico LTE](https://docs.sixfab.com/docs/sixfab-pico-lte-introduction)

3. [MongoDB](https://www.mongodb.com)

## Conclusion

Since I encountered a problem, I could not make much progress in the application, but if the problem is solved, I have prepared the knowledge and infrastructure that will allow me to finish the application in a very short time.
