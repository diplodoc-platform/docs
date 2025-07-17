---

noIndex: true
metadata:

- name: robots
  content: noindex

---

# Changes to postback sending

Please be aware of the upcoming change to RCPA postback submission for the **{{ send-postback-on-first-target-event-only }}** option, effective June 15, 2025.

## 🔄 How it worked previously {#how-it-was}

With the **{{ send-postback-on-first-target-event-only }}** option enabled, a postback used to be sent once when a conversion occurred within the tracker's attribution window. This factored in the current status: it didn't matter whether or not there were other conversions before the tracker activation — only the first event following the tracker activation mattered.

## 🆕 How it will work {#how-it-will-be}

The **{{ send-postback-on-first-target-event-only }}** option's behavior will change: a postback will only be sent for the very first conversion that occured after an install (the *once per install* rule). If the user takes conversion actions before the tracker is activated, no postback is sent.

In the future, we'll update the option's name to better reflect its new behavior.

{% note info "" %}

This change only applies to RCPA postbacks, which are postbacks sent in response to a user's in-app actions.

{% endnote %}

## 🧩 What changes for previously created trackers {#trackers}

The change only affects remarketing trackers with the **{{ send-postback-on-first-target-event-only }}** option enabled. We'll disable this setting in the interface: RCPA postbacks will be sent for all conversions within the attribution window. This will happen automatically on June 15, 2025.

The change won't affect install trackers: their behavior already complies with the *once per install* rule, because no conversion can occur before an install.

If you need to maintain the *once per install* behavior, after the changes take effect, edit the tracker settings manually and re-enable the updated **{{ send-postback-on-first-target-event-only }}** option.

{% note info "" %}

Enabling the updated option will completely skip sending a postback if the user had taken conversion actions before the tracker was activated.

{% endnote %}

## ✅ Reasons for the change {#why}

- Higher transparency: All conversions within the attribution window will be visible to the partner.
- Consolidation: The system will be compatible with the new conversion model.
- Easier analysis and debugging: A predictable behavior with no hidden filters on the tracker's side.

If you have any questions, reach out to the support team — we'll help you adapt to the changes.

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

