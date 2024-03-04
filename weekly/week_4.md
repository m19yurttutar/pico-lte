# Project Progress Report - Week 4

## Project Overview

This week, I tried to fix the "+CME ERROR: 701" error I received as a result of the work I did last week. I reviewed my "steps" one by one, but I could not find any problems in the code part. Then I looked at the MongoDB Atlas Data API side, but again, I did not come across any requirements that the application did not meet. In addition, while continuing my research on MongoDB Atlas, I realized that MongoDB Atlas has an API that supports various administration operations such as adding clusters. I noted this API somewhere because I was thinking of adding various administration functions to my project after I fixed the error. I also corrected the naming errors I had made before by reading the `CONTRIBUTING.md`, `Developer Guideline.md` and `create_your_own_method.py` files.

```
# Note: All operations are carried out through "steps" and the code is simplified to avoid clutter.

# self.network.register_network() # OK
# self.network.get_pdp_ready() # OK

region = get_parameter(["mongodb_atlas", "region"])
cloud_provider = get_parameter(["mongodb_atlas", "cloud_provider"])
app_id = get_parameter(["mongodb_atlas", "app_id"])
api_key = get_parameter(["mongodb_atlas", "api_key"])

if not (
    region is None
    and cloud_provider is None
    and app_id is None
    and api_key is None
):
    host = f"{region}.{cloud_provider}.data.mongodb-api.com"
    query = f"app/{app_id}/endpoint/data/v1/action/findOne"
    url = f"https://{host}/{query}"
else:
    debug.error("There are missing parameters for MongoDB Atlas.")

# self.http.set_server_url(url=url) # OK

payload = {
    "dataSource": "PicoLTE",
    "database": "sample_guides",
    "collection": "planets",
    "filter": {"_id": {"$oid": "621ff30d2a3e781873fcb660"}},
}

payload = json.dumps(payload)

header = "\n".join(
    [
        f"POST /{query} HTTP/1.1",
        f"Host: {host}",
        "Content-Type: application/json",
        f"Content-Length: {len(payload)+1}",
        f"apiKey: {api_key}",
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
) # +CME ERROR: 701 (Unknown Error)

# Note: When I enter another url instead of the MongoDB Atlas API endpoint (for example, webhook.site url), the code works without errors.
```

## References

1. [Pico LTE MicroPython SDK](https://github.com/sixfab/pico_lte_micropython-sdk)

2. [Sixfab Pico LTE](https://docs.sixfab.com/docs/sixfab-pico-lte-introduction)

3. [MongoDB Atlas Administration API 2.0](https://www.mongodb.com/docs/atlas/reference/api-resources-spec/v2)

4. [MongoDB Atlas Data API](https://www.mongodb.com/docs/atlas/app-services/data-api/openapi)

## Conclusion

In short, I had sufficient preliminary information about the project I wanted to do. However, due to an error that I still could not fix, I could not fully start the product's development process.
