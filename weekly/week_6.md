# Project Progress Report - Week 6

## Project Overview

This week, I wrote the functions of the 'create_project' and 'create_cluster' operations using the MongoDB Atlas Administration API endpoints that I obtained as a result of my research in the past weeks. Apart from this, there were repetitive structures found in all HTTP functions. I made a big simplification in my code by collecting these structures in a function I called 'base_http_request'.

- **base_http_request:** Base function for MongoDB Atlas HTTP requests.

```
def base_http_function(
    self,
    function_name,
    http_method,
    url,
    data,
    desired_response,
    username=None,
    password=None,
):
    """
    Base function for MongoDB Atlas HTTP requests.

    Parameters
    ----------
    function_name: str
        Name of the function.
    http_method: str
        HTTP method for the request.
    url: str
        URL for the request.
    data: str
        Data for the request.
    desired_response: str
        Desired response for the request.

    Returns
    -------
    dict
        Result dictionary that contains "status" and "response" keys.
    """

    step_network_reg = Step(
        function=self.network.register_network,
        name="register_network",
        success="get_pdp_ready",
        fail="failure",
    )

    step_get_pdp_ready = Step(
        function=self.network.get_pdp_ready,
        name="get_pdp_ready",
        success="set_server_url",
        fail="failure",
    )

    step_set_server_url = Step(
        function=self.http.set_server_url,
        name="set_server_url",
        success=(
            "http_request" if username is None or password is None else "set_auth"
        ),
        fail="failure",
        function_params={"url": url},
    )

    step_set_auth = Step(
        function=self.http.set_auth,
        name="set_auth",
        success="http_request",
        fail="failure",
        function_params={"username": username, "password": password},
    )

    if http_method == "GET":
        step_http_request = Step(
            function=self.http.get,
            name="http_request",
            success="read_response",
            fail="failure",
            function_params={
                "header_mode": 1,
                "data": data,
            },
        )
    elif http_method == "POST":
        step_http_request = Step(
            function=self.http.post,
            name="http_request",
            success="read_response",
            fail="failure",
            function_params={
                "header_mode": 1,
                "data": data,
            },
        )
    elif http_method == "PUT":
        step_http_request = Step(
            function=self.http.put,
            name="http_request",
            success="read_response",
            fail="failure",
            function_params={
                "header_mode": 1,
                "data": data,
            },
        )
    else:
        return {"status": Status.ERROR, "response": "Invalid HTTP method."}

    step_read_response = Step(
        function=self.http.read_response,
        name="read_response",
        success="success",
        fail="failure",
        function_params={"desired_response": desired_response},
    )

    sm = StateManager(first_step=step_network_reg, function_name=function_name)

    sm.add_step(step_network_reg)
    sm.add_step(step_get_pdp_ready)
    sm.add_step(step_set_server_url)
    sm.add_step(step_set_auth)
    sm.add_step(step_http_request)
    sm.add_step(step_read_response)

    while True:
        result = sm.run()
        if result["status"] == Status.SUCCESS:
            return result
        elif result["status"] == Status.ERROR:
            return result
        time.sleep(result["interval"])
```

- **Create Project:** Function for creating a project in MongoDB Atlas.

```
Endpoint: https://cloud.mongodb.com/api/atlas/v2/groups
Auth: DigestAuth
Accept: application/vnd.atlas.2023-02-01+json
```

- **Create Cluster:** Function for creating a cluster in MongoDB Atlas.

```
Endpoint: https://cloud.mongodb.com/api/atlas/v2/groups/{groupId}/clusters (groupId is also known as projectId)
Auth: DigestAuth
Accept: application/vnd.atlas.2023-02-01+json
```

**Note:** To use the Administration API functions, it is necessary to disable the IP List requirement or register the device's IP address in the IP List.

## References

1. [Pico LTE MicroPython SDK](https://github.com/sixfab/pico_lte_micropython-sdk)

2. [Sixfab Pico LTE](https://docs.sixfab.com/docs/sixfab-pico-lte-introduction)

3. [MongoDB Atlas Administration API](https://www.mongodb.com/docs/atlas/reference/api-resources-spec/v2)

## Conclusion

I added 'create_project' and 'create_cluster' operations to my project for the management API. I will finish my project by adding a few more functions to the project and writing examples next week, provided that I solve the +CME ERROR: 701 error I receive.
