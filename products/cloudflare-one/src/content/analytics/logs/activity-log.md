---
order: 2
---

# Activity logs

<Aside>

Activity log will only show the public Source IP address. Private IP addresses are NAT-ed behind a public IP address. 

</Aside>

The Activity log allows you to see individual DNS queries made from your locations or, for paid subscribers, HTTP requests made from WARP clients. You can use the Activity log to investigate anomalies in your network. You can search by the DNS query or HTTP request and investigate each by clicking on a row.

## DNS
![Gateway activity log](../../static/documentation/logs/teams-dash-activity-log.png)

When you click on the row, you can see information related to the identity that is making the DNS request and attributes relevant to the DNS queries.

![Gateway activity log expanded](../../static/documentation/logs/teams-dash-activity-log-expanded.png)

### Explanation of the fields


<TableWrap>

| Field | Description |
| ----- | ----------- |
| **Request** | The name of the domain that was queried. |
| **Request type** | The DNS query type. [This page](https://en.wikipedia.org/wiki/List_of_DNS_record_types) contains a list of all the DNS query types. |
| **Action** | What Action Gateway applied. For example: Allowed, Blocked etc. |
| **Source IP** | The public source IP of the DNS request. |
| **Time** | The timestamp of the DNS query. |
| **Location** | The location from where the DNS query was made. |
| **Protocol type** | The protocol that was used to make the DNS query. |
| **Port** | The port that was used to make the DNS request. |
| **Policies** | The name of the policy if it applies to the DNS request. |
| **Categories** | Category or categories associated with the DNS request. |

</TableWrap>

## HTTP

### Explanation of the fields

<TableWrap>

| Field | Description |
| ----- | ----------- |
| **Host** | The hostname in the HTTP header for the HTTP request. |
| **Method** | The HTTP method used for the request (e.g., GET, POST, etc.) |
| **Decision** | The Gateway action taken based on the first rule that matched. For example: Allowed, Blocked, Bypass, etc. |
| **Time** | The timestamp of the HTTP request |
| **URL** | The full URL of the HTTP request |
| **Device** | The ID of the device that made the request. This is generated by the WARP client on the device that created the request. |
| **Referer** | The Referer request header contains the address of the page making the request. |
| **User Agent** | The user agent header sent in the request by the originating device. |
| **File Name** | File name string if a file transfer occurred or was attempted. |
| **HTTP version** | The HTTP version of the origin that Gateway connected to on behalf of the user. |
| **Policy details** | The policy corresponding to the decision Gateway made based on the traffic criteria of the request. |

</TableWrap>

### Isolate requests

When a user creates a policy to isolate traffic, the initial request that triggers isolation will be logged as an `Isolate` decision and the `is_isolated` field will return `false`. This is because that initial request is not isolated yet — but it initiates an isolated session.

Since the request is generated in an isolated browser, the result is rendered in the isolated browser and rendered back to the user securely. This request and all subsequent requests in the isolated browser are logged to include the terminal Gateway action that gets applied (e.g. Allow / Block) and the `is_isolated` field as `true`. 