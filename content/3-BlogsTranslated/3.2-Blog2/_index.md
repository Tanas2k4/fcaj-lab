---
title: "Blog 2"
date: 2026-07-02
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Introducing the AWS WAF traffic overview dashboard

For many network security operators, protecting application uptime can be a time-consuming challenge of baselining network traffic, investigating suspicious senders, and determining how best to mitigate risks. Simplifying this process and understanding network security posture at all times is the goal of most IT organizations that are trying to scale their applications without also needing to scale their security operations center staff. To help you with this challenge, AWS WAF introduced traffic overview dashboards so that you can make informed decisions about your security posture when your application is protected by AWS WAF.

In this post, we introduce the new dashboards and delve into a few use cases to help you gain better visibility into the overall security of your applications using AWS WAF and make informed decisions based on insights from the dashboards.

---

## Introduction to traffic overview dashboards

The traffic overview dashboard in AWS WAF displays an overview of security-focused metrics so that you can identify and take action on security risks in a few clicks, such as adding rate-based rules during distributed denial of service (DDoS) events. The dashboards include near real-time summaries of the Amazon CloudWatch metrics that AWS WAF collects when it evaluates your application web traffic.

These dashboards are available by default and require no additional setup. They show metrics—total requests, blocked requests, allowed requests, bot compared to non-bot requests, bot categories, CAPTCHA solve rate, top 10 matched rules, and more—for each web access control list (web ACL) that you monitor with AWS WAF.

You can access default metrics such as the total number of requests, blocked requests, and common attacks blocked, or you can customize your dashboard with the metrics and visualizations that are most important to you.

These dashboards provide enhanced visibility and help you answer questions such as these:
- What percent of the traffic that AWS WAF inspected is getting blocked?
- What are the top originating countries for the traffic that’s getting blocked?
- What are common attacks that AWS WAF detects and protects me from?
- How do my traffic patterns from this week compare with last week?

The dashboard has native and out-of-the-box integration with CloudWatch. Using this integration, you can navigate back and forth between the dashboard and CloudWatch; for example, you can get a more granular metric overview by viewing the dashboard in CloudWatch. You can also add existing CloudWatch widgets and metrics to the traffic overview dashboard, bringing your tried-and-tested visibility structure into the dashboard.

With the introduction of the traffic overview dashboard, one AWS WAF tool—Sampled requests—is now a standalone tab inside a web ACL. In this tab, you can view a graph of the rule matches for web requests that AWS WAF has inspected. Additionally, if you have enabled request sampling, you can see a table view of a sample of the web requests that AWS WAF has inspected.

The sample of requests contains up to 100 requests that matched the criteria for a rule in the web ACL and another 100 requests for requests that didn’t match rules and thus had the default action for the web ACL applied. The requests in the sample come from the protected resources that have received requests for your content in the previous three hours.

The following figure shows a typical layout for the traffic overview dashboard. It categorizes inspected requests with a breakdown of each of the categories that display actionable insights, such as attack types, client device types, and countries. Using this information and comparing it with your expected traffic profile, you can decide whether to investigate further or block the traffic right away. For the example in Figure 1, you might want to block France-originating requests from mobile devices if your web application isn’t supposed to receive traffic from France and is a desktop-only application.

### AWS WAF Traffic Overview Dashboard

![AWS WAF Traffic Overview Dashboard](/images/blogs/blog2-Picture1.png)
*Figure 1: Dashboard with sections showing multiple categories serves as a single pane of glass*

---

## Use case 1: Analyze traffic patterns with the dashboard

In addition to visibility into your web traffic, you can use the new dashboard to analyze patterns that could indicate potential threats or issues. By reviewing the dashboard’s graphs and metrics, you can spot unusual spikes or drops in traffic that deserve further investigation.

The top-level overview shows the high-level traffic volume and patterns. From there, you can drill down into the web ACL metrics to see traffic trends and metrics for specific rules and rule groups. The dashboard displays metrics such as allowed requests, blocked requests, and more.

Notifications or alerts about a deviation from expected traffic patterns provide you a signal to explore the event. During your exploration, you can use the dashboard to understand the broader context and not just the event in isolation. This makes it simpler to detect a trend in anomalies that could signify a security event or misconfigured rules. For example, if you normally get 2,000 requests per minute from a particular country, but suddenly see 10,000 requests per minute from it, you should investigate. Using the dashboard, you can look at the traffic across various dimensions. The spike in requests alone might not be a clear indication of a threat, but if you see an additional indicator, such as an unexpected device type, this could be a strong reason for you to take follow-up action.

### Next steps after you analyze traffic

- **Tune your AWS WAF rules** to better match legitimate or malicious traffic based on your findings. You might be able to fine-tune rules to reduce false positives or false negatives. Tune rules that are blocking legitimate traffic by adjusting regular expressions or conditions.
- **Configure AWS WAF logging**, and if you have a dedicated security information and event management (SIEM) solution, integrate the logging to enable automated alerting for anomalies.
- **Set up AWS WAF to automatically block known malicious IPs**. You can maintain an IP block list based on identified threat actors. Additionally, you can use the Amazon IP reputation list managed rule group, which the Amazon Threat Research Team regularly updates.
- **If you see spikes in traffic to specific pages**, check that your web applications are functioning properly to rule out application issues driving unusual patterns.
- **Add new rules to block new attack patterns** that you spot in the traffic flows. Then review the metrics to help confirm the impact of the new rules.
- **Monitor source IPs for DDoS events** and other malicious spikes. Use AWS WAF rate-based rules to help mitigate these spikes.
- **If you experience traffic floods**, implement additional layers of protection by using CloudFront with DDoS protection.

---

## Use case 2: Understand bot traffic during onboarding and fine-tune your bot control rule group

With AWS WAF Bot Control, you can monitor, block, or rate limit bots such as scrapers, scanners, crawlers, status monitors, and search engines. If you use the targeted inspection level of the rule group, you can also challenge bots that don’t self-identify, making it harder and more expensive for malicious bots to operate against your website.

On the traffic overview dashboard, under the Bot Control overview tab, you can see how much of your current traffic is coming from bots, based on request sampling (if you don’t have Bot Control enabled) and real-time CloudWatch metrics (if you do have Bot Control enabled).

During your onboarding phase, use this dashboard to monitor your traffic and understand how much of it comes from various types of bots. You can use this as a starting point to customize your bot management. For example, you can enable common bot control rule groups in count mode and see if desired traffic is being mislabeled. Then you can add rule exceptions, as described in AWS WAF Bot Control example: Allow a specific blocked bot.

The following figure shows a collection of widgets that visualize various dimensions of requests detected as generated by bots. By understanding categories and volumes, you can make an informed decision to either investigate by further delving into logs or block a specific category if it’s clear that it’s unwanted traffic.

### Bot-related metrics on the Dashboard

![Bot-related metrics on the Dashboard](/images/blogs/blog2-Picture2.png)
*Figure 2: Collection of bot-related metrics on the dashboard*

After you get started, you can use the same dashboard to monitor your bot traffic and evaluate adding targeted detection for sophisticated bots that don’t self-identify. Targeted protections use detection techniques such as browser interrogation, fingerprinting, and behavior heuristics to identify bad bot traffic. AWS WAF tokens are an integral part of these enhanced protections.

AWS WAF creates, updates, and encrypts tokens for clients that successfully respond to silent challenges and CAPTCHA puzzles. When a client with a token sends a web request, it includes the encrypted token, and AWS WAF decrypts the token and verifies its contents.

---

## Comparison with CloudFront security dashboard

The AWS WAF traffic overview dashboard provides enhanced overall visibility into web traffic reaching resources that are protected with AWS WAF. In contrast, the CloudFront security dashboard brings AWS WAF visibility and controls directly to your CloudFront distribution. If you want the detailed visibility and analysis of patterns that could indicate potential threats or issues, then the AWS WAF traffic overview dashboard is the best fit. However, if your goal is to manage application delivery and security in one place without navigating between service consoles and to gain visibility into your application’s top security trends, allowed and blocked traffic, and bot activity, then the CloudFront security dashboard could be a better option.

---

## Availability and pricing

The new dashboards are available in the AWS WAF console, and you can use them to better monitor your traffic. These dashboards are available by default, at no cost, and require no additional setup. CloudWatch logging has a separate pricing model and if you have full logging enabled you will incur CloudWatch charges. You can customize the dashboards if you want to tailor the displayed data to the needs of your environment.

---

## Conclusion

With the AWS WAF traffic overview dashboard, you can get actionable insights on your web security posture and traffic patterns that might need your attention to improve your perimeter protection.

**Source:** [AWS Security Blog](https://aws.amazon.com/blogs/security/introducing-the-aws-waf-traffic-overview-dashboard/)

**Post on AWS Study group:** [AWS Security Blog](https://www.facebook.com/groups/awsstudygroupfcj/posts/2202070817224545/)