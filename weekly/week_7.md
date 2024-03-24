# Project Progress Report - Week 7

## Project Overview

This week, I integrated the "Server Name Indication" configuration, which is the solution to the "+CME ERROR: 701" error, into my code. After I resolved the error, I tried to finalize my project. As a result of these efforts, functions were added to the final version of my project to use CRUD operations from the MongoDB Atlas Data API, and sample codes were written for each function.I also refactored the "base_http_function" function that I wrote last week.

- **Server Name Indication(SNI) Configuration**

```
# AT command of SNI configuration

AT+QSSLCFG="sni",{ssl_context_id},{sni}
```

```
# Integrating configuration code by steps

step_http_ssl_configuration = Step(
    function=self.http.set_ssl_context_id,
    name="http_ssl_configuration",
    success="set_sni",
    fail="failure",
    function_params={"cid": 1},
)

step_set_sni = Step(
    function=self.ssl.set_sni,
    name="set_sni",
    success="set_server_url",
    fail="failure",
    function_params={"ssl_context_id": 1, "sni": 1},
)
```

## References

1. [Sixfab Pico LTE](https://docs.sixfab.com/docs/sixfab-pico-lte-introduction)

2. [Pico LTE MicroPython SDK](https://github.com/sixfab/pico_lte_micropython-sdk)

3. [MongoDB Atlas Data API](https://www.mongodb.com/docs/atlas/app-services/data-api/openapi)

## Conclusion

Starting next week, I plan to fulfill correction requests that may come from the pull request that I will open while writing the document of my project. In this way, I will prepare my project for the users.
