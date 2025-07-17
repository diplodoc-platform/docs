# Integration for ad networks within SKAdNetwork

AppMetrica can accept postbacks from ad networks received from Apple as a part of SKAdNetwork. This solution allows:

- Advertising partners to scale a single solution to all mobile measurement partners (MMP) without additional adjustments on their side.
- Advertisers to evaluate campaign results based on users who prohibit tracking.

## How it works {#operation-principle}

1. Apple sends a SKAd postback to the advertising network.
2. The advertising network sends the postback to AppMetrica without changes or enriched with internal parameters (for example, the campaign name or id).
3. AppMetrica displays the data in the User Acquisition SKAdNetwork report.

## Request format {#query-format}

Authorization token isn't required.

Providing IP addresses for inclusion in the whitelist isn't required.

`POST https://skadnet-postback.yandex.net/postback`

`Content-Type: application/json`

## Request parameters {#params}

The request parameters for integrating ad networks with AppMetrica using SkAdNetwork are described below.

| Parameter | Required | Format | Description / Example | Source |
| -------- | ------------ | ------ | ----------------- | -------- |
| `version` | Yes | string | 2.0 | SKAd |
| `ad-network-id` | Yes | string | Abc123.skadnetwork | SKAd |
| `campaign-id` | Yes | Integer | 42 | SKAd |
| `transaction-id` | Yes | string | 68eb3d91-15f5-44ee-9267-25c7655c20b6 | SKAd |
| `app-id` | Yes | Integer | 472650686 | SKAd |
| `attribution-signature` | Yes | string |  | SKAd |
| `redownload` | No | Boolean |  | SKAd |
| `source-app-id` | No | Integer | 1050704155 | SKAd |
| `conversion-value` | No | Integer | 0-63 | SKAd |
| `fidelity-type` | No | Integer | 0 or 1, required since version 2.2 | SKAd |
| `ad-network-campaign-id` | No | string | Internal campaign id | Network |
| `ad-network-campaign-name` | No | string | Internal campaign name | Network |
| `ad-network-adset-id` | No | string | Internal adset id | Network |
| `ad-network-adset-name` | No | string | Internal adset name | Network |
| `ad-network-ad-id` | No | string | Internal ad id | Network |
| `ad-network-ad-name` | No | string | Internal ad name | Network |
| `ip` | No | string | IP of device, may be used for location (ipv4 / ipv6) | Network |
| `timestamp` | No | string | Time the network received postback from Apple (unix timestamp) | Network |
| `timestamp` | No | string | Time the network received postback from Apple (unix timestamp) | Network |

You can pass additional parameters that are not in the table, but they won't be displayed in the User Acquisition SKAdNetwork report.

## HTTP response code {#responce}

`200 OK`: The request was completed successfully.

`400 Bad request`: One of the request parameters has an invalid value or data format.

## AppMetrica ad partners {#partners-list}

AppMetrica supports SKAdNetwork and is integrated with the following ad partners:

- AdColony
- Hybrid
- Spyke Media
- Yandex
- AdTiming
- Unity Ads
- {% if locale == "ru" %}VK Ads{% else %}VK Ads{% endif %}

If you didn't find the necessary ad partner, you can configure the transfer of all SKAdNetwork postbacks to AppMetrica by following the [instructions](ios15-tracking.md).

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
