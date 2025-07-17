# Anti-fraud solution

Anti-fraud solution is a system designed to detect and prevent fraudulent activity.

Fraudulent actions, such as generating fake clicks or installs, reduce ad effectiveness. As a result, return on investment (ROI) decreases and advertisers are exposed to financial losses. Fraud also distorts analytical data so it's hard to make informed business decisions.

## Fraud types {#fraud-types}

According to FraudScore, a leading provider of solutions for analyzing and detecting fraud in mobile traffic, about 30% of iOS traffic and 40% of Android traffic is fraudulent.

The most common fraud types are:

- Click spam: Generating lots of clicks without actual ad interaction. Fraudsters use this technique to intercept organic traffic and attribute it to specific publishers.
- Click injection: Sending a fake ad engagement between an app download and its first launch. Using this method, fraudsters steal attributions from other sources.
- Device farms: Generating user actions by bots to simulate user activity and boost traffic.
- SDK spoofing: Sending fake requests from an SDK to the analytical system's servers. Fraudsters use this technique to generate fake installs and user events.

AppMetrica is integrated with the FraudScore system, which helps you detect click spam, click injection, and bots that mimic real users. To combat SDK spoofing, AppMetrica offers [event verification](../data-collection/index.md#verification-events) solutions.

## How to enable the anti-fraud solution {#setup}

Our anti-fraud solution is a paid feature. For pricing information, see [{#T}](pricing/ru-currency.md#pro-upgrade).

To enable the anti-fraud feature:

1. From the side panel, go to **Organization**.
1. Select a pricing plan and click **Settings**.
1. Go to the **FraudScore antifraud** tab and select the amount of installs you need.
1. Click **Proceed to purchase**.

    {% note info "Payment" %}

    Instead of being charged for the entire month at once, you are charged daily. If the number of installs per month exceeds the limit you selected, fraud detection stops automatically.

    {% endnote %}

1. Once you enable the feature, new and existing trackers will have the **Antifraud by FraudScore** option. Enable this option in the trackers where you want to check installations for fraud. While the option is active, all the installations recorded by those tracker are sent to FraudScore.

    {% note warning "Restrictions" %}

    The anti-fraud option is not availabe in trackers with media sources Google Ads, Google Search, and Yandex.Direct.

    {% endnote %}

Assessment scores are available in 24 hours after the first install is sent for assessment. You can view them in the **{{ dimension-sources }}** → **{{ fraud-assessment }}** grouping in the [User Acquisition](../mobile-reports/user-acquisition-report.md) report.

We recommend using as many parameters provided by the ad network as possible, including:

- Platform ID
- Keywords
- Group ID
- Ad ID

This information helps analyze fraud in greater detail and address fraudulent activity in a more targeted manner (for example, only disable individual platforms when needed).

## How the fraud risk is assessed {#assessment}

FraudScore analyzes traffic using more than [150 metrics](http://help.fraudscore.ai/article/6038245564547072/3-4-1-what-are-fraud-reasons) that are divided into 33 groups called [extended fraud reasons](#extended-fraud-reasons). In each group, several metrics are analyzed using different algorithms.

There's also a higher-level division into [fraud reasons](http://help.fraudscore.ai/section/5864674745712640/3-4-fraud-reasons), but the system primarily uses extended fraud reasons for analysis.

For each extended fraud reason identified, the conversion gets a fraud score. If multiple anomalies are detected for the same conversion, its fraud scores for these anomalies are summed up. Depending on its total fraud score, the conversion is assigned a [fraud level](https://help.fraudscore.ai/article/5629807400321024/5-1-4-fraud-score-levels):

- `Not fraud`: Non-suspicious traffic.
- `Likely not fraud`: Low fraud risk level (1–2 violations), the fraud score is no more than 33.
- `Likely fraud`: Medium fraud risk level (2–4 violations), the fraud score is between 33 and 66.
- `Fraud`: High fraud risk level (4 or more non-critical violations, 3 or more critical violations), the fraud score is over 66.

AppMetrica reports only include resources classified as `fraud` and `likely fraud`.

For more information on using fraud assessments, see [How to use "Extended Fraud Reasons" slice](http://help.fraudscore.ai/article/6576232228519936/3-4-14-how-to-use-extended-fraud-reasons-slice).

## Descriptions for extended fraud reasons {#extended-fraud-reasons}

#|
|| **No.** | **Name** | **Description** ||
|| 1 | OS | Suspicious distribution of devices (including device models, browser versions, and operating systems) within traffic. ||
|| 2 | Duplicate IP | Multiple conversions from the same IP or subnet. ||
|| 3 | Duplicate device | Multiple conversions originating from the same or very similar device. ||
|| 4 | Dynamic IP | Multiple conversions from dynamic IP addresses. ||
|| 5 | IP distribution | Abnormal distribution of IP addresses. ||
|| 6 | Emulator | Using device emulators like Bluestacks. ||
|| 7 | Fake device | Fake device parameters (including user agent, IDFA/Android ID, or MAC address) or their combinations. ||
|| 8 | Click spamming | App install attributed to a click but discovered to be an organic install claimed by an ad network using spam fingerprinting algorithms. ||
|| 9 | Refer host | Click from a suspicious site. ||
|| 10 | Low TTI | Abnormally short period between a click and a conversion. In case of Android conversions, this is indicative of click injection. ||
|| 11 | E-mail disposable | User specified a disposable email address. ||
|| 12 | Flat TTI | Abnormal distribution of times between clicks and corresponding conversions, indicative of click spamming. ||
|| 13 | Overall Flat TTI | Important metric for detecting TTI (time to install) deviations. It allows processing traffic across wider slices and can be used either in combination with Flat TTI or independently. ||
|| 14 | Low Variance TTI | TTI metric is suspicious because of the low variance of actual installation time for the large number of conversions. ||
|| 15 | TOR | IP is an exit point for the Tor network. ||
|| 16 | Datacenter | Traffic originating from servers belonging to data centers or popular cloud service providers rather than from home or corporate networks. In such cases, the likelihood of real human user interaction is very low. ||
|| 17 | Geo mismatch | Signs of user location spoofing detected. ||
|| 18 | Proxy context | Too many IP addresses marked as PROXY in the current segment. ||
|| 19 | Proxy dynamic | Dynamic IP addresses. ||
|| 20 | Proxy | IP addresses act as proxies but aren't directly linked to fraud. ||
|| 21 | Blacklist | IP addresses linked to suspicious activity or recently used by a potentially compromised device linked to fraudulent activity. ||
|| 22 | Blacklist dynamic | For IP addresses directly linked to fraudulent activity similar to Blacklist, but in this case conversions originate from IP addresses belonging to mobile carriers. ||
|| 23 | Old Browser version | Old browser version is used. The user's browser version must be newer/up to date. ||
|| 24 | Outdated browser version | Very old browser version. ||
|| 25 | Crawler | Symptom that indicates the use of a web crawler (for example, used by a search engine). ||
|| 26 | Duplicate build | Large number of conversions originating from the same Android build. ||
|| 27 | Regional Specific Device | Abnormal location of a device intended for a specific region or market. ||
|| 28 | No events | Huge share of conversions has no associated in-app activity. ||
|| 29 | ISP anomaly | Prevailing number of conversions originate from the same provider. ||
|| 30 | Bad events | Suspicious in-app activity, abnormal metrics for most events. ||
|| 31 | Lowcr | Abnormally low click-to-install conversion rate, typically indicative of click spamming. ||
|| 32 | Highcr | Abnormally high click-to-install or click-to-registration conversion rate.  This is typical for sources with bot devices and may indicate the presence of incentivized traffic. ||
|| 33 | Multiple attribution | Multiple conversions with the abnormal distribution of attribution metrics. ||
|#

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
